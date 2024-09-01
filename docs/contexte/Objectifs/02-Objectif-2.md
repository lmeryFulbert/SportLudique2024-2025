# Objectif Stratégique 2 : Prendre en compte la dimension cartographique

La cartographie va sous peu évoluer du fait la la redistribution des
rôles entre les deux sites de production de Tours et Orléans :

Les 2 sites de production et d’acheminement de Tours et Orléans vont être
regroupés en un seul (sur Tours), le site d’Orléans gardant sa spécificité de R&D.

La Direction demande particulièrement à la DSI de réfléchir dès
maintenant à la manière d’intégrer ces nouveaux paramètres dans
l’infrastructure existante.

##  Stratégie Operationnelle : Optimiser la gestion et la disponibilité de l’infrastructure

Tout doit être mis en œuvre plus rendre l’infrastructure globalement
plus disponible, tant au niveau des serveurs que de des postes
utilisateurs, ce qui revient à assurer une plus grande disponibilité et
donc productivité des utilisateurs et des techniciens du centre
d’appels.

Cela passera par différents moyens d’action :

### Mise en place d’outils de gestion de par cet de supervision réseau

Pour pouvoir réduire le coût des serveurs et des stations de travail, il
sera important de limiter le nombre d’interventions et le temps passé
sur chaque machine.

Pour cela, deux actions de base devront être mises en place :

* Les serveurs seront installés à partir de techniques dites silencieuses, avec des fichiers de réponses.

* Les stations de travail seront industrialisées avec l’installation des
Service Packs et autres. Les postes utilisateurs seront préconfigurés
avec les logiciels nécessaires au fonctionnement de la station de travail de base.

Les outils de gestion de parc et de supervision de réseau devront donc
être étudiés et mis en place, afin de rationaliser les interventions du
centre d’appels.

### Mise en place d’outils de déploiement

On déploiera les logiciels par l’intermédiaire de la technologie
Intelligente proposé par les systèmes d’exploitation (Stratégies de
groupes par exemple) ou des solutions applicative spécialisées
(déploiement via GLPI par exemple).

Pour réduire les coûts liés aux interventions des techniciens sur les
sites, on mettra en place un modèle de poste standard (Master)

### Homogénéité logiciels des stations de travail

Pour garantir la bonne utilisation des postes, la DSI publiera les
logiciels de base, ce qui présentera l’intérêt de permettre une remise
en état automatique en cas de suppression volontaire ou involontaire de
la part de l’utilisateur.

### Limitation des droits des utilisateurs

Pour ne plus avoir de problèmes de stabilité sur les stations de
travail, les utilisateurs ne seront plus administrateurs de leur
station. Il faudra donc utiliser la politique du moindre privilège.

On utilisera des modèles de sécurité pour appliquer des paramètres de
sécurité cohérents sur l’ensemble des stations de travail de
l’organisation. On créera des stratégies de groupe en fonction des
besoins des services (ressources humaines, finances…) et des contraintes
de domaine et de site, pour assurer la meilleure utilisation des postes
selon les besoins spécifiques, et uniquement les besoins.

La mise en place de clichés instantanés permettra aux utilisateurs de
gérer eux-mêmes les sauvegardes des différentes versions de leurs
fichiers. Par une interface très simple, ils pourront restaurer des
versions antérieures et ainsi diminuer le nombre de coups de téléphone
au centre d’appels.

La mise en place d'un serveur de fichier et d'une politique de sauvegarde adéquate devra être mis en place.

L’étude des stratégies de compte en fonction des besoins de chaque
domaine contribuera également à l’effort de réduction de la charge
d’appels.

### Application de quotas d’espace de stockage aux utilisateurs

Pour limiter l’utilisation des serveurs de fichiers et maîtriser les
dépenses dues à l’achat d’espace disque, on appliquera des quotas.

L’action d’un utilisateur sur un poste se limitera uniquement aux
besoins de son périmètre. Il sera important de limiter, voire d’empêcher l’installation de logiciels
exotiques (non nécessaires à l’entreprise), qui sont facteurs de
réinstallation des postes et de surplus de coups de téléphone au centre
d’appels (helpdesk).

### Mettre en place des services réseaux

Messagerie, téléphonie sur IP, services d’impression, accès nomades, accès WIFI

### Mettre en place d’outils de gestion

PGI, SGBD, outils collaboratifs..., certains outils seront d'ailleurs accessible via le Cloud (comme MS Team)
