# 13 Portail Captif avec Stormshield

## Introduction

Un portail captif est une page web qui s'affiche automatiquement lorsqu'un utilisateur se connecte à un réseau public ou restreint (en general en Wi-FI). Il oblige l'utilisateur à s'authentifier, accepter des conditions d'utilisation ou effectuer une action spécifique (comme entrer un code, payer un accès, ou s'inscrire) avant de pouvoir accéder à Internet.

## Pourquoi est-ce nécessaire légalement ?

En France et dans de nombreux pays, un opérateur de réseau public (y compris les entreprises, écoles, cafés, hôtels) est tenu de conserver un journal des connexions (logs) pour des raisons de traçabilité et de cybersécurité. Ces obligations sont encadrées par des lois comme :

- La loi anti-terrorisme et la loi HADOPI en France, qui exigent que l'accès Internet public ne soit pas anonyme.
- Le RGPD, qui impose d'informer les utilisateurs sur la collecte de leurs données et d'obtenir leur consentement.
- Le Code des postes et communications électroniques, qui tient le fournisseur d'accès responsable si son réseau est utilisé pour des activités illégales.

## Implémentation avec Stormshield

Stormshield prévoit trois modes d’authentification via un portail captif pour la gestion des accès invités :

### Mode Guest (Autoregistration)

- L’utilisateur s’inscrit lui-même via le portail captif en renseignant ses informations (nom, email, etc.). Cela est paramétrable.
- Un administrateur peut valider la demande ou l'accès peut être automatique après inscription.
- Utile pour les visiteurs occasionnels dans une entreprise ou un établissement public.

### Mode Vouchers (Comptes Temporaires)

- L’accès est basé sur des codes d’accès temporaires (vouchers) générés par un administrateur.
- Chaque code peut être limité en durée et en nombre d’utilisations.
- Adapté aux événements, conférences, ou accès temporaires pour des clients.

### Mode Parrainage (Sponsoring)

- Un utilisateur déjà authentifié (employé, responsable, etc.) doit valider la demande d’accès d’un invité.
- Permet un contrôle plus strict, car un sponsor est responsable de l’accès accordé.
- Idéal pour les entreprises souhaitant une traçabilité accrue des connexions des visiteurs.

La manière de configuré le portail captif est toujours similaire.


