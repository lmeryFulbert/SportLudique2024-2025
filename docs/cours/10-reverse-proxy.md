# 06 - Reverse Proxy

Un reverse proxy est un serveur qui agit en tant qu'intermédiaire entre les clients et les serveurs. Son rôle principal est de recevoir les requêtes des clients et de les rediriger vers les serveurs appropriés, puis de renvoyer les réponses des serveurs aux clients.

Dans le contexte de votre infrastructure, vous avez un serveurs web (Apache) avec des sites différents (vhosts) et une application Docker sur une VM. Vous souhaitez utiliser Nginx comme reverse proxy sur le serveur avec l'IP 192.168.1.10 pour gérer les requêtes vers les différents serveurs en fonction des noms de domaine.

Voici un exemple de configuration Nginx pour cela :

### Installation de Nginx (si ce n'est pas déjà fait) :

```bash
sudo apt-get update
sudo apt-get install nginx
```

### Configuration de Nginx :

1. Créer un fichier pour chaque site dans **/etc/nginx/sites-available** :

```bash
sudo nano /etc/nginx/sites-available/site1
```

2. Ajoutez une section pour chaque site, en remplaçant les valeurs par les vôtres :

```nginx

    server {
        listen 80;
        server_name site1.domaine.org;

        location / {
            proxy_pass http://site1.domaine.org;   //avec une resolution donnant l'IP interne par le resolver
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }
```
```bash
sudo nano /etc/nginx/sites-available/site2
```
```nginx
    server {
        listen 80;
        server_name site2.domaine.org;

        location / {
            proxy_pass http://192.168.1.20:88; // avec un port d'écoute spécifique à un vhost
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }
```
etc...
```nginx
    server {
        listen 80;
        server_name site3.domaine.org;

        location / {
            proxy_pass http://192.168.1.30:unport;  #
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }
```

Créer un lien symbolique pour chaque site référencé dans **sites-available** pour les activer dans **sites-enabled** 

```bash
# Create symbolic links for all sites in sites-available
sudo ln -s /etc/nginx/sites-available/site1 /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/site2 /etc/nginx/sites-enabled/
# Repeat the above command for each site configuration file

# Test Nginx configuration
sudo nginx -t

# If the configuration test is successful, reload Nginx
sudo systemctl reload nginx
```

Les directives `proxy_set_header` dans la configuration Nginx sont utilisées pour définir les en-têtes HTTP qui seront envoyés au serveur backend lorsqu'une requête est transmise par le reverse proxy. Ces en-têtes sont généralement utilisés pour transférer des informations sur la requête ou le client d'origine au serveur backend. Voici une explication des directives que vous trouverez dans l'exemple fourni :

1. **`proxy_set_header Host $host;`**:
   - Cette directive définit l'en-tête `Host` qui est envoyé au serveur backend. Elle prend la valeur de `$host`, qui est la valeur de l'en-tête `Host` de la requête initiale du client. Cela est important pour que le serveur backend puisse distinguer entre différents domaines virtuels (vhosts) s'il en gère plusieurs.

2. **`proxy_set_header X-Real-IP $remote_addr;`**:
   - Cette directive définit l'en-tête `X-Real-IP`, qui est souvent utilisé pour transmettre l'adresse IP réelle du client au serveur backend. Cela peut être utile lorsque Nginx est placé derrière un autre proxy.

3. **`proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;`**:
   - Cette directive définit l'en-tête `X-Forwarded-For`. Il s'agit d'un en-tête standard utilisé pour transmettre l'adresse IP du client d'origine au serveur backend. La valeur `$proxy_add_x_forwarded_for` ajoute l'adresse IP du client à la liste existante de adresses IP déjà présentes dans l'en-tête.

4. **`proxy_set_header X-Forwarded-Proto $scheme;`**:
   - Cette directive définit l'en-tête `X-Forwarded-Proto`. Cet en-tête indique au serveur backend le protocole utilisé par le client pour accéder à Nginx (HTTP ou HTTPS). La valeur `$scheme` prend la valeur du schéma de la requête (http ou https).

L'utilisation de ces en-têtes est importante lorsqu'un reverse proxy est utilisé, car elle permet de fournir au serveur backend des informations cruciales sur la requête initiale du client. Cela est particulièrement important dans les architectures où plusieurs serveurs interagissent les uns avec les autres, et où certaines informations de la requête d'origine peuvent être perdues lors du passage par le proxy.


3. Sauvegardez et fermez le fichier.

4. Testez la configuration Nginx :

```bash
sudo nginx -t
```

5. Redémarrez Nginx pour appliquer les modifications :

```bash
sudo systemctl restart nginx
```

Maintenant, Nginx agira en tant que reverse proxy et dirigera les requêtes en fonction des noms de domaine vers les serveurs appropriés.

Assurez-vous de remplacer les valeurs comme `192.168.1.20`, `192.168.1.30`, `unport` par les valeurs spécifiques à votre configuration. Vous pouvez également personnaliser les options de proxy en fonction de vos besoins.

## Gestion de TLS

La gestion du HTTPS avec Nginx implique la configuration d'un certificat SSL/TLS pour sécuriser les connexions entre les clients et le serveur Nginx. Voici comment vous pouvez ajouter la prise en charge du HTTPS à votre configuration existante :

2. **Modifiez la configuration Nginx :**
   - Ajoutez les directives SSL dans chaque bloc `server` pour activer le support HTTPS.

     ```nginx
     server {
         listen 80;
         server_name site1.domaine.org;
         return 301 https://$host$request_uri; // forcer la redirection en https
     }

     server {
         listen 443 ssl;
         server_name site1.domaine.org;

         ssl_certificate /etc/ssl/certificat.pem;
         ssl_certificate_key /etc/ssl/privkey.pem;

         # ... autres directives SSL (comme ssl_protocols, ssl_ciphers, etc.)
         
         location / {
             proxy_pass http://192.168.1.20;
             include /etc/nginx/proxy_params;
         }
     }
     ```

     - Répétez le même processus pour les autres serveurs virtuels (`site2.domaine.org` et `site3.domaine.org`).

3. **Redémarrez Nginx :**
   - Une fois que vous avez configuré les certificats et ajusté la configuration Nginx, redémarrez Nginx pour appliquer les changements.

     ```bash
     sudo systemctl restart nginx
     ```

Maintenant, votre serveur Nginx devrait être configuré pour gérer les connexions HTTPS. Assurez-vous de remplacer les chemins des certificats (`ssl_certificate` et `ssl_certificate_key`) avec les chemins réels de vos certificats.

N'oubliez pas de maintenir vos certificats SSL à jour. Vous pouvez configurer un renouvellement automatique avec Certbot en ajoutant une tâche planifiée (cron job).

Dans le scénario de configuration qci dessus, les certificats SSL/TLS sont généralement nécessaires uniquement sur le serveur Nginx, qui agit en tant que reverse proxy. Les serveurs d'origine (Apache, serveurs Docker, etc.) ne nécessitent pas de certificats SSL/TLS propres, car la communication entre le serveur Nginx et les serveurs d'origine peut souvent se faire en interne via des connexions non chiffrées.

Le trafic chiffré SSL/TLS entre les clients et Nginx s'arrête au niveau du serveur Nginx, et la communication entre Nginx et les serveurs d'origine peut être non chiffrée (HTTP) ou chiffrée séparément (par exemple, si les serveurs d'origine prennent en charge HTTPS et ont leurs propres certificats).

Assurez-vous que le trafic entre Nginx et les serveurs d'origine est sécurisé en fonction de vos exigences de sécurité. Si nécessaire, vous pouvez activer HTTPS entre Nginx et les serveurs d'origine, mais cela impliquera la configuration de certificats sur ces serveurs d'origine également. Dans de nombreux cas, cette couche de chiffrement supplémentaire n'est pas nécessaire si le réseau interne est considéré comme sécurisé.