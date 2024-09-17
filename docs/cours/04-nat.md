# 03-NAT Dynamique (Masquerade) version Cisco

Le NAT dynamique est une technique utilisée pour permettre à plusieurs dispositifs d'une réseau local (IP inside) de partager une seule adresse IP publique (IP outside) pour accéder à Internet ou d'autres réseaux externes.

**Éléments du NAT dynamique :**

1. **IP Inside (Adresse privée)** : L'adresse IP inside est l'adresse IP attribuée aux dispositifs du réseau local. Dans votre exemple, l'adresse IP inside est en 172.28.x.254/24. Ces adresses IP sont généralement privées et ne sont pas routables sur Internet.

2. **IP Outside (Adresse publique)** : L'adresse IP outside est l'adresse IP attribuée au routeur ou au pare-feu qui relie le réseau local au réseau externe, généralement Internet. Dans votre exemple, l'adresse IP outside est en 183.44.x.1/30. Cette adresse IP est publique et utilisée pour communiquer avec des ressources sur Internet.

3. **Table de traduction (Translation Table)** : La table de traduction est une table gérée par le routeur ou le pare-feu NAT qui associe les adresses IP inside aux adresses IP outside. Chaque fois qu'un dispositif du réseau local initie une connexion vers l'extérieur, une entrée est créée dans la table de traduction pour suivre la correspondance entre l'adresse IP inside et l'adresse IP outside.

4. **Port Mapping (Port Mapping)** : Dans le cas du NAT dynamique, les numéros de port sont également modifiés. Cela permet à plusieurs dispositifs à l'intérieur du réseau local d'utiliser la même adresse IP publique en attribuant un numéro de port unique à chaque connexion. Ainsi, le routeur peut rediriger le trafic vers le dispositif approprié en fonction du numéro de port.

**Configuration du NAT dynamique avec Cisco :**

Voici un exemple de configuration du NAT dynamique avec Cisco :

```bash
interface GigabitEthernet0/0
 ip address 183.44.x.1 255.255.255.252
 ip nat outside

interface GigabitEthernet0/1
 ip address 172.28.x.254 255.255.255.0
 ip nat inside

ip nat inside source list 1 interface GigabitEthernet0/0 overload

access-list 1 permit 172.28.x.0 0.0.0.255
```

Explications :

- La commande `ip nat outside` est appliquée à l'interface connectée à l'extérieur (GigabitEthernet0/0), tandis que `ip nat inside` est appliqué à l'interface connectée au réseau local (GigabitEthernet0/1).

- La commande `ip nat inside source list 1 interface GigabitEthernet0/0 overload` définit la règle de translation NAT dynamique. Elle indique que toutes les adresses IP du réseau local (définies dans l'access-list 1) seront traduites en utilisant l'adresse IP publique de l'interface GigabitEthernet0/0, avec la surcharge (overload) pour gérer plusieurs connexions simultanées en utilisant le mappage de ports.

- L'access-list 1 spécifie les adresses IP à l'intérieur du réseau local qui sont autorisées à être traduites.

Ainsi, avec cette configuration, les dispositifs du réseau local avec des adresses IP en 172.28.x.x pourront accéder à Internet en partageant l'adresse IP publique 183.44.x.1 grâce au NAT dynamique. Chaque connexion sortante se verra attribuer un numéro de port unique pour permettre la correspondance correcte entre les dispositifs internes et l'adresse IP publique.

## Verification du contenu de la table de NAT

Pour vérifier la table de translation NAT et la vider sur un routeur Cisco, vous pouvez utiliser les commandes suivantes :

Pour vérifier la table de translation NAT, utilisez la commande suivante :
```bash
show ip nat translations
```

Cette commande affichera une liste des entrées dans la table de translation NAT, montrant les adresses IP inside, les ports source, les adresses IP outside, les ports de destination, ainsi que le protocole utilisé.

Pour vider la table de translation NAT, utilisez la commande suivante :
```bash
clear ip nat translation *
```

Cette commande supprimera toutes les entrées de la table de translation NAT, réinitialisant ainsi les associations entre les adresses IP inside et outside. Assurez-vous d'utiliser cette commande avec précaution, car elle peut interrompre les connexions en cours.

## Gestion avec une interface de management

Vous pouvez configurer le NAT avec une sous-interface dédiée au management qui n'est pas routée. Voici un exemple de configuration NAT avec une sous-interface sur un routeur Cisco, en supposant que vous avez déjà configuré une interface principale :

Configuration de la sous-interface pour le NAT :

```bash
interface GigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 172.28.x.254 255.255.255.0
 ip nat inside

interface GigabitEthernet0/0.20
 encapsulation dot1Q 20
 ip address 192.168.1.1 255.255.255.0
 no ip route-cache
```

Dans cet exemple :

- Nous avons créé deux sous-interfaces, "GigabitEthernet0/0.10" et "GigabitEthernet0/0.20", chacune avec son propre VLAN (10 et 20).
- "GigabitEthernet0/0.10" est configuré comme une interface NAT inside, avec une adresse IP de 172.28.x.254/24. Cette sous-interface sera utilisée pour le trafic NAT.
- "GigabitEthernet0/0.20" est configuré avec une adresse IP de gestion de 192.168.1.1/24, mais nous avons ajouté "no ip route-cache" pour empêcher cette interface d'être routée. Ainsi, cette sous-interface est dédiée au management et ne participera pas au processus de routage.

Ensuite, vous pouvez configurer le NAT de la même manière que dans l'exemple précédent, en utilisant "GigabitEthernet0/0.10" comme interface NAT inside. Cette configuration permettra aux dispositifs du réseau VLAN 10 (sous-interface 10) d'utiliser NAT pour accéder à Internet, tandis que la sous-interface 20 est réservée au management et n'est pas routée.

## Configuration du switch pour assurer la liaison.

Pour connecter le routeur à un commutateur (switch), vous pouvez configurer une connexion trunk(802.1q) entre le routeur et le commutateur si vous avez plusieurs VLANs sur le routeur (comme dans l'exemple précédent). Voici comment configurer un port du commutateur pour une connexion trunk vers le routeur Cisco.

Supposons que vous ayez deux VLANs spécifiques, VLAN 10 et VLAN 20, que vous souhaitez autoriser à communiquer avec le routeur. Vous avez déjà configuré les sous-interfaces correspondantes sur le routeur (comme dans l'exemple précédent).

Configuration du port du commutateur en mode trunk avec les VLANs autorisés :

```bash
interface GigabitEthernet0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20
 ```

Dans cette configuration :

- switchport mode trunk configure le port du commutateur en mode trunk.
- switchport trunk allowed vlan 10,20 spécifie que seuls les VLANs 10 et 20 sont autorisés à traverser le port trunk. Vous pouvez ajouter d'autres numéros de VLAN séparés par des virgules si nécessaire.

Assurez-vous que la configuration de l'interface du commutateur est compatible avec la configuration des sous-interfaces sur le routeur. Cela garantira que le trafic VLAN entre le commutateur et le routeur est correctement étiqueté et routé.