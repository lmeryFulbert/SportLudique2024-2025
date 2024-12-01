# Resolver Unbound

Unbound est un résolveur DNS récursif rapide et sécurisé développé par l'organisation NLnet Labs. Il est principalement utilisé pour répondre aux requêtes DNS de manière récursive tout en assurant la confidentialité, l'intégrité, et la validation des réponses à l'aide de DNSSEC (Domain Name System Security Extensions).

## Fonctionnement d'Unbound

Unbound peut fonctionner comme :

- Un résolveur récursif : Il effectue la résolution DNS complète en interrogeant directement les serveurs DNS depuis les racines jusqu'aux serveurs faisant autorité.
- Un validateur DNSSEC : Il assure que les réponses DNS n'ont pas été modifiées en chemin en vérifiant les signatures cryptographiques des enregistrements DNS.

!!! info "Attention"
    Les fonctionnalité DNSSEC ne peuvent être mise en place au sein du projet sportludique qui est un projet simulé. Le nom de domaine n'existe pas reelement et est géré par un serveur DNS spécifiquement mis en place par votre enseignant.

## Principales fonctionnalités d'Unbound

- Résolution récursive : Il effectue les requêtes DNS en partant du serveur racine jusqu'à la source autoritaire.
- Validation DNSSEC : Garantit que les données DNS n'ont pas été altérées ou falsifiées.
- Cache DNS : Il stocke les réponses des requêtes pour améliorer les performances en évitant des résolutions répétées pour les mêmes requêtes.
- Vie privée : Unbound permet de minimiser les informations envoyées dans les requêtes DNS (via QNAME minimisation), ce qui améliore la confidentialité de l'utilisateur.
- Support pour IPv6 : Il supporte les requêtes et résolutions d'adresses IPv6. (On ne travaillera qu'avec IPv4)

## Resolution de problème courants

Toujours vérifier votre configuration avec :

```bash
sudo unbound-checkconf
```

Si on obtient ceci:

```bash
[1728294345] unbound-checkconf[7516:0] error: failed to read /var/lib/unbound/root.key
[1728294345] unbound-checkconf[7516:0] error: error reading auto-trust-anchor-file: /var/lib/unbound/root.key
[1728294345] unbound-checkconf[7516:0] error: validator: error in trustanchors config
[1728294345] unbound-checkconf[7516:0] error: validator: could not apply configuration settings.
[1728294345] unbound-checkconf[7516:0] fatal error: bad config for validator module
```

Le problème est liée à la configuration des trust anchors DNSSEC (ancrages de confiance) dans Unbound. 

Si besoin on peux réinitialiser ce fichier

```bash
sudo unbound-anchor -a /var/lib/unbound/root.key
```

Verification:

```bash
sudo unbound-checkconf
```

Redemarrage du service:

```bash
sudo systemctl restart unbound
```

