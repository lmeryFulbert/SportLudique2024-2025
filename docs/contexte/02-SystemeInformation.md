# Le Système d'Information

##  Présentation de l’infrastructure Informatique

Le système d'information (SI) de SportLudique reflète la dynamique de l'entreprise : mis en place il y a quelques années, il a depuis connu une expansion considérable. SportLudique est divisée en quatre domaine windows autonomes, chacun opérant sur un site géographique distinct et controlé par un controleur de domaine indépendant.

En réponse à la croissance de l'activité et à divers projets informatiques, des serveurs Windows 2019 Server et Windows Server 2022 ont été intégrés au système. Cette initiative visait à renforcer la fiabilité et à ajouter des fonctionnalités, le tout sans perturber l'infrastructure existante. 

L'architecture actuelle repose sur la virtualisation, mise en œuvre à travers de la solution hyperconvergée proposée par Nutanix et son hypervieur AHV. Un projet de mise en oeuvre d'un système de tolérance aux pannes reposant sur des hyperviseurs Proxmox sera à mettre en oeuvre et devront accueillir à minima un controlleur de domaine secondaire pour assurer une haute disponibilité de ce service critique.

Chaque site bénéficie de son propre département informatique, couvrant un large éventail de responsabilités allant de l'administration réseau et système (Windows et Linux), la supervision de l'infrastructure à l'assistances aux utilisateurs via une solution de helpdesk qu'il faudra mettre en oeuvre.

Les utilisateurs font partie d'un domaine géré localement par délégation du nom de domaine commun **sportludique.fr**. Les postes de travail de l'équipe IT sont sous Linux avec une interface utilisateur (GUI). Ils utilisent diverses applications adaptées à leurs activités, notamment des suites bureautiques telles que LibreOffice, ainsi que des outils graphiques ou des applications internes développées au sein de l'entreprise.

L'administration des machines windows se fera avec un client SSH intégré nativement au système **sans** bureau X11
L'administration des machines Windows se fera avec un client RDP (Remote Desktop Protocol) déjà intégré aux postes de travail via la commande suivante:

``` xfreerdp /u:user@domain.tld /v:fqdn-server-or-IP /sec:nla```