# 13 Authentification - 802.1X

## Qu'est-ce que 802.1X ?

802.1X est un protocole d’authentification réseau utilisé pour contrôler l’accès aux réseaux filaires et sans fil. Il repose sur trois composants :

- **Supplicant** : Le client (PC, téléphone, imprimante) qui veut accéder au réseau.
- **Authenticator** : Le switch ou le point d'accès Wi-Fi qui intercepte la connexion et demande une authentification.
- **Authentication Server** : Généralement un serveur RADIUS, qui vérifie les identifiants et renvoie une autorisation ou un refus. On parle aussi de serveur Triple A (AAA)

Le protocole **EAP (Extensible Authentication Protocol)** est utilisé pour transporter les informations d’authentification.

## Pourquoi utiliser 802.1X ?

-  Contrôle d’accès strict pour les utilisateurs et appareils.
-  Évite les accès non autorisés au réseau (ex. : un inconnu branchant un câble RJ45).
-  Permet l’authentification par certificat, identifiants (MS-CHAPv2), ou carte à puce.
-  Peut être intégré avec un VLAN dynamique pour assigner des droits réseau en fonction du profil utilisateur.

## Authentification sur un réseau WIFI WPA2-Entreprise avec NPS de microsoft

Le service **Network Policy Server (NPS)** est le rôle Windows Server qui gère l’authentification RADIUS.

## Authentification des tiers

### Authentification du Serveur

- Le serveur NPS doit posséder un certificat SSL/TLS pour prouver son identité au supplicant.
- Ce certificat doit être signé par une autorité de certification (CA) reconnue par les clients.
- Le certificat peut être auto-signé (test) ou issu d’une PKI interne ou publique.

!!! danger "Important"
    Il est vivement recommandé de gérer la PKI sur un serveur dédié même s'il est "pratique" d'installer le role Active Directory Certificate Services (ADCS)

### Authentification des clients

- Soit par identifiant/mot de passe (ex: EAP-PEAP, qui encapsule MSCHAPv2)
- Soit par certificat client (ex: EAP-TLS, qui nécessite un certificat par utilisateur ou machine)

### Ajouter l'équipement l'Access Point comme client RADIUS

Ajouter un nouveau client en précisant son nom, son IP et la clé secrète partagée.
Type de client: RADIUS Standard

#### Configurer une stratégie de demande de connexion

Définir le nom de la stratégie.

Pour du WIFI:
    Type de port NAS : Sans fil IEEE 802.11

#### Configurer une strategie réseau

Définir la condition en spécifiant le groupe d'utilisateur concerné par la stratégie (via l'annuaire Active Directory).

Définir la contrainte en précisant la methode d'authentification:
- PEAP + MSChapov2 (identifiants + mot de passe)
- ou Carte à Puce ou autre certificat (Authentification forte par certificats x509)

Définir les paramètres suivants:

- Framed-Protocol : PPP
- Service-Type: Framed
- Tunnel-Medium-Type : 802 (include all 802 media...)
- Tunnel-Pvt-Group-ID : Numéro de VLAN souhaité pour cette stratégie
- Tunnel-Type: Virtual LANs (VLAN)

## Informations complémentaires

### Historique de RADIUS et son lien avec la facturation des communications (AAA)

Le protocole RADIUS (Remote Authentication Dial-In User Service) a été développé en 1991 par Livingston Enterprises. Son objectif initial était de gérer l'authentification, l’autorisation et le comptage (accounting) (AAA) des utilisateurs accédant aux réseaux via des modems et des connexions dial-up (RTC).

À cette époque, les fournisseurs d’accès à Internet (FAI) et les entreprises de télécommunications facturaient les connexions à Internet en fonction de :
- La durée de connexion (en minutes ou en heures)
- Le volume de données transféré (dans certains cas)

Il fallait donc un système robuste pour :

- **Authentifier** l’utilisateur avant qu’il puisse se connecter
- **Authorisation** : Contrôler son accès (quota, services autorisés, priorités, etc.)
- **Accounting**: Enregistrer sa consommation pour la facturation

C’est dans ce contexte que RADIUS a été conçu pour gérer les accès des abonnés en mode dial-up.

Le protocole **TACACS (Terminal Access Controller Access-Control System)** a été développé dans les années 1980 par le Département de la Défense des États-Unis pour l’authentification des accès aux équipements réseau. Il a ensuite évolué avec des versions améliorées, dont XTACACS et TACACS+, aujourd’hui principalement utilisé chez Cisco.

C’est dans ce contexte que TACACS a été conçu, initialement pour les terminaux des militaires et des opérateurs télécoms.

802.1X (avec RADIUS) et TACACS+ sont deux protocoles utilisés pour contrôler l'accès au réseau, mais ils ont des usages et des fonctionnements différents. Voici les principales différences :

 RADIUS utilise UDP, ce qui le rend plus rapide mais moins fiable que TACACS+ qui fonctionne en TCP.



### Protocole et Port utilisé
| Protocole       | 802.1X avec RADIUS                        | TACACS+      |
|-----------------|------------------------------------------|--------------|
| **Port**        | UDP 1812 (Auth) / 1813 (Accounting) ou 1645/1646 | TCP 49      |
| **Encapsulation** | UDP (moins fiable)                     | TCP (fiable, retransmission garantie) |
| **Standard**    | Ouvert, RFC 2865                         | Propriétaire (Cisco) |


### Objectif et cas d’usage
| Usage                                            | 802.1X (RADIUS)         | TACACS+     |
|--------------------------------------------------|-------------------------|-------------|
| **Contrôle d’accès aux équipements réseau (administration CLI)** | ❌ Non              | ✅ Oui      |
| **Contrôle d’accès des utilisateurs au réseau (filaire/Wi-Fi)** | ✅ Oui              | ❌ Non      |
| **Authentification sur VPN, Wi-Fi, réseau filaire** | ✅ Oui              | ❌ Non      |
| **Authentification, Autorisation et Comptabilité (AAA)** | ✅ (Mais moins granulaire) | ✅        |


