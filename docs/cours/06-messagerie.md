# 06 - Messagerie

## Enregistrement MX et Serveurs DNS

L'enregistrement MX (Mail Exchange) dans le système de noms de domaine (DNS) est essentiel pour diriger le courrier électronique vers le serveur de messagerie approprié. Cela s'effectue en spécifiant une priorité (le chiffre avant le nom du serveur MX) et le nom du serveur de messagerie. Voici un exemple plus détaillé :

````bash
MX 10 mail.example.com
mail.example.com   IN   A   203.0.113.1
````
Cet enregistrement indique que le serveur de messagerie pour le domaine example.com est mail.example.com avec une priorité de 10. La priorité est utilisée pour déterminer l'ordre de préférence des serveurs MX lorsque plusieurs sont disponibles.

Cet enregistrement associe l'adresse IP 203.0.113.1 au nom de domaine mail.example.com. Ainsi, lorsque quelqu'un envoie un courrier à user@example.com, le système de messagerie consulte l'enregistrement MX pour déterminer le serveur de messagerie de destination (mail.example.com), puis utilise l'enregistrement A pour obtenir son adresse IP (203.0.113.1).

Ces enregistrements, présents dans la zone DNS du domaine, permettent au courrier électronique d'être correctement dirigé vers le serveur de messagerie associé au domaine cible.

## Protocoles de Messagerie

### SMTP (Simple Mail Transfer Protocol)

Le protocole SMTP (Simple Mail Transfer Protocol) est utilisé pour l'envoi de courriers électroniques. Il opère sur le port TCP 25 par défaut. Cependant, il est important de noter que le port 25 n'est pas sécurisé.

#### Port TCP 25 (Non sécurisé) :

Le port 25 est traditionnellement utilisé pour la transmission non sécurisée des courriers électroniques. Cependant, en raison de problèmes de sécurité potentiels, de nombreux fournisseurs de services de messagerie et ISP (Fournisseurs d'Accès Internet) bloquent parfois le trafic sortant sur ce port pour prévenir le spam.

#### Port TCP 587 (STARTTLS) :

Pour surmonter les limitations de sécurité liées au port 25, le port 587 est souvent utilisé comme alternative. Ce port est dédié à la transmission sécurisée des courriers électroniques en utilisant le mécanisme STARTTLS. Lorsqu'un client se connecte au serveur SMTP sur le port 587 et indique qu'il souhaite utiliser STARTTLS, une connexion sécurisée est établie avant le transfert du courrier électronique.

Le mécanisme STARTTLS permet d'ajouter une couche de sécurité (chiffrement) à la communication SMTP, rendant difficile l'interception des informations sensibles, telles que le contenu du courrier électronique et les informations d'identification.

### POP (Post Office Protocol)

Le protocole POP (Post Office Protocol) est utilisé pour récupérer les courriers électroniques d'un serveur et les télécharger sur l'appareil local de l'utilisateur. Deux versions couramment utilisées sont POP3 (non sécurisé) et POP3S (sécurisé).

#### Port TCP 110 (Non sécurisé - POP3) :

Le port 110 est traditionnellement associé à la communication POP3 non sécurisée. Lorsqu'un client de messagerie se connecte au serveur POP3 sur ce port, les courriers électroniques sont téléchargés du serveur vers l'appareil local. Cependant, le transfert d'informations sur le port 110 est effectué en texte brut, sans chiffrement, ce qui expose les données à des risques potentiels d'interception.

#### Port TCP 995 (Sécurisé - POP3S) :

Pour remédier aux vulnérabilités de sécurité liées à la transmission non sécurisée sur le port 110, le port 995 est réservé au protocole POP3 avec une couche de sécurité (SSL/TLS) ajoutée. Cette version sécurisée est appelée POP3S. Lorsqu'un client se connecte au serveur POP3 sur le port 995, la communication est chiffrée, garantissant une transmission sécurisée des courriers électroniques entre le serveur et l'appareil local.

### IMAP (Internet Message Access Protocol)

Le protocole IMAP (Internet Message Access Protocol) est conçu pour permettre une gestion plus avancée des courriers électroniques en synchronisant les messages entre le client de messagerie et le serveur. Deux versions couramment utilisées sont IMAP (non sécurisé) et IMAPS (sécurisé).

#### Port TCP 143 (Non sécurisé - IMAP) :

Le port 143 est associé à la communication IMAP non sécurisée. Lorsqu'un client de messagerie se connecte au serveur IMAP sur ce port, il peut afficher les en-têtes des courriers électroniques et choisir les messages à télécharger. Cependant, le transfert d'informations sur le port 143 est effectué en texte brut, sans chiffrement, exposant potentiellement les données à des risques d'interception.

#### Port TCP 993 (Sécurisé - IMAPS) :

Pour renforcer la sécurité des communications IMAP, le port 993 est réservé au protocole IMAP avec une couche de sécurité (SSL/TLS) ajoutée. L'utilisation de ce port sécurisé, appelé IMAPS, garantit que la transmission des données entre le client et le serveur est chiffrée, préservant ainsi la confidentialité des informations.

La caractéristique principale d'IMAP par rapport à POP est la conservation des messages sur le serveur. Les actions effectuées sur le client (marquer comme lu/non lu, déplacer vers un dossier, etc.) sont reflétées sur le serveur, assurant une synchronisation entre les différents appareils connectés au même compte de messagerie.
IMAP permet de gérer les courriels sur plusieurs appareils.
POP télécharge les courriels, les retirant du serveur, ce qui est moins pratique dans un monde multi-appareils.

## Positionnement du Serveur de Messagerie

### Zone Réseau Protégée :

Le positionnement du serveur de messagerie au sein d'une zone réseau protégée est crucial pour garantir la sécurité des données et la disponibilité des services. Cette zone, souvent appelée le "réseau de périmètre", est configurée avec des pare-feu, des systèmes de détection d'intrusion et d'autres mécanismes de sécurité pour contrôler et filtrer le trafic réseau.

### Pare-feu :

Un pare-feu est déployé pour surveiller et filtrer le trafic entrant et sortant du serveur de messagerie. Cela aide à prévenir les attaques malveillantes, telles que les tentatives d'intrusion ou les attaques par déni de service.

### Détection d'Intrusion :

Les systèmes de détection d'intrusion sont mis en place pour détecter les activités suspectes ou malveillantes. Cela inclut la surveillance des journaux d'événements, l'analyse du trafic réseau, et l'identification des tentatives d'accès non autorisées.

### Stockage des Boîtes aux Lettres sur un Serveur de Base de Données Sécurisé :

Le stockage des boîtes aux lettres sur un serveur de base de données sécurisé offre plusieurs avantages en termes de sécurité et de gestion des données.

#### Chiffrement des Données :

Les données des boîtes aux lettres peuvent être chiffrées pour garantir que même en cas d'accès non autorisé, les informations restent illisibles sans la clé de chiffrement appropriée.

**Gestion Centralisée :**

La centralisation des données sur un serveur de base de données facilite la gestion des boîtes aux lettres, les sauvegardes régulières, et la mise en œuvre de politiques de sécurité cohérentes.

**Contrôle d'Accès :**

Des mécanismes de contrôle d'accès stricts peuvent être appliqués pour garantir que seules les personnes autorisées ont accès aux données sensibles des boîtes aux lettres.

En intégrant ces pratiques dans l'infrastructure, le serveur de messagerie peut opérer de manière sécurisée, réduisant les risques potentiels liés à la confidentialité et à l'intégrité des données.

## Obligations Légales et Confidentialité dans le Contexte Français

### Accès aux Boîtes aux Lettres :

En France, l'accès aux boîtes aux lettres des utilisateurs est soumis à des obligations légales strictes visant à protéger la vie privée des individus et à garantir la confidentialité des communications électroniques. Voici quelques points importants à considérer :

#### RGPD (Règlement Général sur la Protection des Données) :

Depuis mai 2018, le RGPD est également applicable en France. Il établit des règles strictes concernant la protection des données personnelles des citoyens de l'Union européenne, y compris les données contenues dans les boîtes aux lettres électroniques. Les entreprises et les administrateurs sont tenus de se conformer aux exigences du RGPD, notamment en matière de consentement, de notification des violations de données, et de respect des droits individuels.

##### Secret des Correspondances :

En vertu de l'article 226-15 du Code pénal français, le secret des correspondances est protégé. Tout accès non autorisé aux communications électroniques, y compris les boîtes aux lettres, peut être passible de sanctions pénales.

##### Autorisation Préalable :

Dans de nombreux cas, l'administrateur système doit obtenir une autorisation préalable avant d'accéder aux boîtes aux lettres des utilisateurs. Cette autorisation peut être déterminée par les politiques internes de l'entreprise et doit être conforme aux lois en vigueur.

##### Conservation des Données :

Les administrateurs doivent être conscients des obligations de conservation des données, définies par la loi, et s'assurer que les politiques de conservation sont respectées.

##### Droit à l'Oubli :

Le RGPD accorde également aux individus le droit à l'oubli, permettant aux utilisateurs de demander la suppression de leurs données personnelles. Les administrateurs doivent être prêts à répondre à de telles demandes de manière conforme à la loi.

En résumé, l'accès aux boîtes aux lettres en France est soumis à un cadre juridique rigoureux visant à protéger les droits fondamentaux à la vie privée et à la protection des données personnelles. Les administrateurs doivent opérer dans le respect de ces lois et mettre en place des mécanismes appropriés pour garantir la confidentialité des communications électroniques. Violations de ces lois peuvent entraîner des sanctions sévères.

## Serveurs de messageries connus

### Sous Windows

- Microsoft Exchange
- hmailserver

### Sous Linux

- Postfix (smtp)
- Dovecot (imap)

### Solution complètes (agenda, contacts etc..)

- Microsoft Exchange
- Zimbra
- IBM Notes (Lotus Notes)

## Clients de messagerie

- Microsoft Outlook
- Mozilla Thunderbird
- Apple Mail
- Evolution (Linux)
