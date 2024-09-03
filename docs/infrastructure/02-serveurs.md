# Liste des serveurs et services

##  Liste des serveurs obligatoires pour l'examen:

Les machines virtuelles à créer et à héberger sur la ferme de serveur sur chaque site (donc dans chaque VLAN d’îlot)
:

### Contrôleurs de domaine 

-   Contrôleur de domaine AD-DC
-   Service DNS
-   Service DHCP

Dans le cadre de la gestion de l'infrastructure informatique, la mise en place de contrôleurs de domaine est cruciale pour assurer l'administration centralisée et sécurisée des ressources du réseau. Il existe deux types principaux de contrôleurs de domaine : le contrôleur de domaine principal et le contrôleur de domaine secondaire.

#### Contrôleur de domaine principal

Le contrôleur de domaine principal, également appelé PDC (Primary Domain Controller), occupe une place centrale dans l'architecture du domaine. Il est responsable de la gestion des opérations de base liées à l'authentification des utilisateurs, à l'autorisation d'accès aux ressources et à la gestion des politiques de sécurité. En cas de modification des informations du domaine, le contrôleur de domaine principal est le point de référence.

#### Contrôleur de domaine secondaire

Les contrôleurs de domaine secondaires, ou BDC (Backup Domain Controllers), jouent un rôle de sauvegarde et de répartition de la charge par rapport au contrôleur de domaine principal. Ils reproduisent les informations du contrôleur de domaine principal pour garantir une redondance et une disponibilité élevées. En cas de panne du contrôleur de domaine principal, les contrôleurs de domaine secondaires peuvent prendre en charge les opérations critiques, évitant ainsi une interruption majeure des services.

Il est important de noter que la mise en place d'un contrôleur de domaine principal et de contrôleurs de domaine secondaires permet une gestion fiable et sécurisée de l'annuaire, des comptes d'utilisateurs et des stratégies de groupe. Cette architecture renforce la disponibilité des services et facilite la gestion du réseau, tout en minimisant les risques de perte de données et de temps d'arrêt.

La combinaison d'un contrôleur de domaine principal et de contrôleurs de domaine secondaires constitue un élément clé de la gestion de l'infrastructure d'un réseau, qu'il soit de petite ou de grande taille.

### Un serveur de déploiement d’image de stations de travail

\- Au choix parmi les solutions suivantes à documenter (gestion du **multicast**):

-   ServeurMicrosoft **WDS**
-   Serveur **FOG**
-   Serveur **CloneZilla**

??? info "Définition"
    Le **multicast** en informatique est une méthode de communication réseau où un expéditeur envoie des données à un groupe spécifique de destinataires plutôt qu'à tous les nœuds du réseau **(broadcast)**. Cela permet d'économiser la bande passante en envoyant une seule copie des données aux membres du groupe intéressés, au lieu de multiplier les envois comme dans les envois en **unicast**. Le multicast est couramment utilisé pour la diffusion de contenu en streaming, les mises à jour de logiciels et d'autres applications nécessitant la transmission d'informations à un groupe ciblé. C'est la solution utilisé pour déployer vos poste de travail en début d'année (via le boot PXE au demarrage de la machine physique).

### Un logiciel de bonne pratiques ITIL

#### Utilisation de logiciels conformes aux bonnes pratiques ITIL

Dans le cadre de l'alignement sur les meilleures pratiques de gestion des services informatiques ITIL (Information Technology Infrastructure Library), l'utilisation de certains logiciels spécifiques peut grandement faciliter la gestion et l'organisation des processus IT.

##### Gestion de parc informatique et incidents

Pour la gestion efficace du parc informatique et le suivi des incidents, l'outil **GLPI** associé à **Fusion Inventory** s'avère très utile. Ces solutions permettent de créer un inventaire précis des équipements, de gérer les tickets d'incidents et de fournir une vue globale des ressources informatiques.

##### Gestion des configurations et des outils associés

La gestion des configurations est un élément fondamental pour maintenir une infrastructure informatique cohérente et conforme aux bonnes pratiques ITIL. Les outils suivants jouent un rôle clé dans ce processus :

##### Outils de gestion des configurations

Deux outils largement adoptés et conformes aux bonnes pratiques ITIL sont **Ansible** et **Puppet**. Ils automatisent le déploiement, la configuration et la gestion des systèmes et des applications. Ces outils vous permettent de garantir la cohérence et la conformité des configurations tout en simplifiant l'administration.

Dans les environnements Windows, l'utilisation de **GPO** (Group Policy Objects) est courante pour définir et gérer les politiques de sécurité et de configuration. Par ailleurs, **GLPI** peut être utilisé comme service de déploiement de logiciels. Pour les environnements Microsoft, l'outil **chocolatey** simplifie le processus de gestion et de déploiement des logiciels.

### Un service de Proxy filtrant (implémentation au choix après études des possibilités)

-   Proxy filtrant : (Exemple **SquidGuard**)
-   Authentification transparente et traçabilité des accès dans un serveur de logs
-   Possibilité d'utiliser le service correspondant d'un parefeux UTM

??? info "Définition"
    Un **pare-feu UTM (Unified Threat Management)** est une solution de sécurité réseau intégrée qui combine plusieurs fonctionnalités de sécurité au sein d'un seul appareil. Contrairement aux pare-feux traditionnels qui se concentrent principalement sur le filtrage de paquets à la couche 3 et 4, les pare-feux UTM offrent une protection plus complète en intégrant diverses capacités de sécurité au sein d'une seule plateforme. Voici les principales caractéristiques et fonctionnalités d'un pare-feu UTM :

-   **Filtrage des paquets traditionnel** : Comme les pare-feux classiques, les UTM assurent le filtrage des paquets en fonction des adresses IP sources et de destination, ainsi que des ports utilisés.

-    **Protection antivirus et antimalware** : Les pare-feux UTM intègrent des moteurs antivirus et antimalware pour détecter et bloquer les logiciels malveillants et les virus dans le trafic réseau.

-    **Filtrage d'URL et de contenu** : Ils peuvent filtrer le trafic Web en fonction de catégories d'URL pour empêcher l'accès à des sites malveillants, inappropriés ou non conformes. (Pornographie, jeux en ligne, racisme etc...)

-    **Prévention des intrusions (IPS)** : Les UTM surveillent le trafic réseau pour détecter les tentatives d'intrusion et les activités suspectes, puis prennent des mesures pour les bloquer.

-    **Filtrage d'email et de spam** : Ils incluent des fonctionnalités de filtrage d'email pour bloquer les courriers indésirables, les spams et les attaques par email.

-    **VPN (Virtual Private Network)** : Ils offrent des capacités VPN pour établir des connexions sécurisées entre différents sites ou utilisateurs distants.

-    **Journalisation et rapports** : Les UTM offrent des fonctionnalités de journalisation détaillée et de création de rapports pour aider à surveiller l'activité du réseau et à identifier les menaces potentielles.

-    **Gestion centralisée** : Souvent, les pare-feux UTM peuvent être gérés de manière centralisée, ce qui facilite la configuration, la surveillance et la gestion de plusieurs appareils.

#### Un serveur de centralisation des évennements ou un SIEM

!!! info "Serveur de log"
    **Serveur de log (syslog)** :
    Un serveur de logs est un système qui collecte, stocke et gère les logs (journaux) générés par divers dispositifs, applications et systèmes au sein d'un réseau informatique. Les logs peuvent inclure des informations sur les activités, les erreurs, les événements et les incidents qui se produisent dans l'environnement informatique. Le principal objectif d'un serveur de logs est de centraliser ces données pour une surveillance ultérieure, la recherche de problèmes et la conformité réglementaire. 
    Cependant, les serveurs de logs ne sont pas toujours équipés d'outils avancés d'analyse ou de corrélation des données.

!!! info "SIEM"
    **SIEM (Security Information and Event Management)** :
    Un SIEM est une solution plus avancée qui va au-delà de la simple collecte de logs. Il intègre la collecte, la corrélation, l'analyse et la visualisation des données de sécurité à partir de diverses sources, telles que les serveurs, les réseaux, les applications et les systèmes. Les SIEM identifient les schémas et les anomalies dans les événements pour détecter les menaces potentielles ou les incidents de sécurité.

### Un serveur de supervision (implémentation au choix après études des possibilités)

\- A choisir parmis les solutions suivantes:

-    **PRTG** (windows)
-    **Zabbix**
-    **Centreon**
-    Autre solution pertinente possible non testé (**Promteus** / **Grafana**)

### Services Web

Serveurs hébergés dans la **DMZ** de chaque site à isoler et à protéger via une parefeux.
On montera chaque service de la DMZ dans l’une ou l’autre des technologies à savoir Windows et Linux. Les deux technologies doivent être maitrisées (administration système windows ET linux)

-   Possibité de mettre en place un ReverseProxy afin de partager l'IP Publique unique disponible entre plusieurs serveurs privé.
-   Mise en place de services web obligatoirement chiffré via technologie TLS
-   Serveur SFTP, en téléchargement de documents mis en ligne
-   Haute disponibilité des services (**High Availability**)
-   Répartition de charge (**Load Balancing**)

??? info "Définition"
    **High Availability** :
    La haute disponibilité des services, souvent désignée par l'anglais "High Availability" (HA), est un concept et une approche de conception qui vise à garantir un niveau élevé de continuité et de disponibilité des services informatiques. L'objectif principal de la haute disponibilité est d'assurer que les systèmes, applications et services critiques sont accessibles et fonctionnels en permanence, même en cas de défaillance matérielle, logicielle ou de tout autre problème.

??? info "Définition"
    **Load Balancing** :
    La répartition de charge, également appelée "load balancing" en anglais, est une technique utilisée pour distribuer équitablement la charge de travail et le trafic réseau entre plusieurs ressources, telles que des serveurs, des machines virtuelles ou des nœuds de réseau. L'objectif principal de la répartition de charge est d'optimiser les performances, d'assurer une utilisation équilibrée des ressources et de garantir une disponibilité élevée des services.

### Services de base de données

Pour assurer le bon fonctionnement des différentes applications (web ou autres), il sera nécessaire de mettre en place un ou plusieurs serveurs de base de données. Ces serveurs joueront un rôle central dans le système d'information (SI) de l'organisation. Ils devront être soigneusement sécurisés et maintenus à l'intérieur du réseau, sans exposition directe à l'extérieur. Pour cela, nous aurons le choix entre plusieurs options : utiliser **MariaDB** ou **PostgreSQL** sous **Linux** pour une approche open source, ou opter pour **SQL Server** chez **Microsoft Windows**.

### Service de messagerie

La communication au sein de l'entreprise est essentielle, et pour cela, un serveur de messagerie sera mis en place. Ce serveur devra prendre en charge les boîtes aux lettres des utilisateurs de chaque domaine, par exemple *antoine.dupond@chartres.sportludique.fr*. Pour cette tâche, nous utiliserons **hMailServer** sous Windows. Cependant, si un étudiant souhaite s'investir davantage, des options plus avancées sont envisageables, telles que **Microsoft Exchange** ou une solution open source comme **Zimbra** (combinant **Postfix** et **Dovecot**). Quelle que soit la solution retenue, elle devra être opérationnelle afin de gérer les notifications provenant des solutions de supervision et autres outils SIEM.

### Bastion d'authentification

Pour sécuriser l'accès aux comptes privilégiés, la mise en place d'un bastion d'authentification est essentielle. Cet élément central du système garantira que les accès aux comptes à haut niveau d'autorisation sont contrôlés et surveillés. Cette solution permet de garantir la traçabilité des accès aux serveurs. À cette fin, nous adopterons la solution leader du marché, à savoir **Wallix**. 