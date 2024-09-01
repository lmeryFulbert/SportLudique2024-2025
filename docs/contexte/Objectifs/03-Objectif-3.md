# Objectif Stratégique 3 - Sécuriser le SI

La sécurité doit devenir primordiale, notamment en ce qui concerne son
système d’informations. Les réseaux étant constamment menacés par des
attaques provenant de sources différentes, la direction souhaite
renforcer la sécurisation de son système d'informations.

En ce sens, la Direction a demandé la mise en place d’un plan de
sécurité à tous les niveaux de l’entreprise, et notamment au niveau de
la DSI. Ce plan devra en permanence tenir compte du coût initial et
continu de la sécurité.

Pour répondre au mieux à cette demande, une phase de conception devra
être définie en introduction du plan de sécurité. Elle permettra
d’analyser tous les facteurs qui, s’ils ne sont pas identifiés, risquent d’augmenter le coût de la sécurité, et de rechercher les technologies de
sécurité qui, si elles ne sont pas employées, feront échouer le projet.

Cette phase de conception s’articulera autour des points suivants :

-   la conception de la sécurité pour la gestion du réseau ;

-   la conception d’une infrastructure de mise à jour des dispositifs de
    sécurité ;

-   la conception d’un système de clients sécurisé.

Le plan de sécurité devra impérativement répondre aux exigences
suivantes :

1.  **Considérer les exigences légales qui affectent la mise en œuvre de la sécurité** Pour intégrer les dispositions légales au sein de l’entreprise, il est
important de demander au service juridique de l’entreprise de vérifier
le plan de sécurité. Il s’agit entre autres de réaliser un certain
nombre de démarches auprès des organismes gouvernementaux et des
associations qui peuvent être des sources de conseils en matière de
sécurité.

2.  **Mesurer l’impact des décisions de sécurité sur les utilisateurs finaux** Il faudra mesurer l’impact des décisions de sécurité sur l’utilisateur
final. Par exemple, dans le cas du choix d’une stratégie de sécurisation des
comptes utilisateurs, une stratégie de mot de passe trop lourde (15
caractères) alliée à une stratégie de complexité de mot de passe
(lettres et chiffres), forcerait l’utilisateur à conserver son mot de
passe sur un papier, près de son ordinateur. De même, une stratégie de verrouillage de comptes mal adaptée apportera
un surplus important de coups de téléphone au centre d’appels.

3.  **Mesurer les risques en se fondant sur la probabilité et la criticité de la menace** Il est important de pouvoir mesurer les probabilités d’attaques, les
moyens mis en œuvre face à une menace ainsi que les réponses à ces
menaces, afin d’en estimer les coûts. Cette analyse de menace sera étudié via la **méthode EBIOS**.
Prenons le cas de la probabilité d’une menace. Si on définit une échelle
des probabilités allant de 1 à 4 – 4 étant la probabilité la plus
importante qu’une menace se produise – et si on définit une échelle du
niveau de criticité allant de 1 à 4 – 4 étant la criticité la plus
élevée – une menace avec une probabilité de 2 et une criticité de 4 sur
cette échelle devra être prise en compte selon certaines considérations.

4. **Maintenir la disponibilité et l’interopérabilité des services** Appliquer une sécurité importante dans l’entreprise ne signifie pas que
l’activité doit s’arrêter. Que l’on ne puisse plus communiquer, échanger
des données ou encore piloter des applications n’est pas forcément le
signe d’un réseau sécurisé. Au contraire, il faut pouvoir garantir les
échanges de données en cryptant les informations, en s’assurant de la
compatibilité de certains protocoles avec les autres systèmes, en
veillant à l’aspect fonctionnel de l’infrastructure. Les performances des machines doivent être prises en compte également :
en effet, l’utilisation excessive d’un protocole de chiffrement peut
empêcher un ordinateur de communiquer dans un temps imparti.

5. **Répondre aux besoins d’évolutivité**. Il ne faut pas que l’infrastructure notamment informatique devienne une
voie de garage dans laquelle il ne sera plus possible d’évoluer.

6. **Sécuriser le service de R&D et les services mis en ligne**.Ce service étant celui qui génère la valeur ajoutée de la société, il
faudra particulièrement le sécuriser, tant au niveau des matériels,
qu’au niveau de l’infrastructure (définition d’un domaine dédié) et de
la transmission des données.

## Stratégie Operationnelle : Sécuriser l’Infrastructure

Pour répondre aux objectifs de sécurité imposés par la Direction, la
sécurité devra être implémentée à plusieurs niveaux fonctionnels :
infrastructure, systèmes, processus, flux.

Il sera nécessaire d’étudier les solutions les moins onéreuses et de
regarder les technologies de sécurité apportées par Windows pouvant répondre au mieux au plan de sécurité.

Windows 11 venant tout juste d’être mis à disposition la DSI souhaite
attendre un retour d’expérience utilisateur sur ce nouvel OS.

Les solutions basées sur les **systèmes libres** seront 
envisagées pour la plupart des serveurs. Les postes de travail resteront dans un envioronnement Microsoft.

### Sécurisation du matériel de l’infrastructure

Les serveurs qui joueront un rôle important dans l’infrastructure
devront être sécurisés dans une salle prévue à cet effet. L’ensemble des serveurs pourra être accessible via
une solution basée sur un cluster d’hyperviseur pour faciliter leur
gestion et réduire l’encombrement. La solution d’infrastructure ainsi
virtualisée, **devra être constamment documenté par les techniciens**.
Les utilisateurs devront être tenus responsables de l’usage du matériel
informatique mis à leur disposition par l’entreprise (PC, portables,
téléphones...). Les contrats de travail et la charte informatique de
l’entreprise devront être revus en ce sens.

La solution d'hyperviseur et d'hyperconvergence reposera sur l'éditeur **Nutanix** 

??? info "Nutanix"
    Nutanix AHV (Acropolis Hypervisor) est une plateforme de virtualisation conçue par Nutanix pour permettre la consolidation des ressources informatiques et la gestion des charges de travail sur des clusters de serveurs. C'est une solution de virtualisation intégrée au sein de l'écosystème Nutanix, visant à simplifier et à optimiser l'infrastructure des centres de données (datacenter).

### Sécurisation des flux

L'ensemble des communications de l’entreprise doivent être protégées.

Il s’agit entre autre, d’isoler l’activité de recherche et de
développement du site d’Orléans et de **chiffrer** les données sensibles.
Les techniques de **VLAN**, de **DMZ**, de **VPN** et de chiffrement des données seront
privilégiées.

??? info "Rappel Cybersécurité"
    **Disponibilité** : Il s'agit d'assurer que les systèmes, les données et les services sont accessibles et opérationnels lorsque nécessaire. La disponibilité est essentielle pour garantir la continuité des opérations et éviter les interruptions nuisibles.

    **Intégrité** : L'intégrité concerne la protection des données et des systèmes contre toute altération non autorisée. Les informations doivent rester exactes et non altérées tout au long de leur cycle de vie.

    **Confidentialité** : La confidentialité consiste à empêcher l'accès ou la divulgation non autorisés des informations sensibles. Elle vise à garantir que seules les personnes autorisées peuvent accéder aux données confidentielles.

    **Preuve (ou Preuve d'Audit)** : Il s'agit de la capacité à démontrer que des événements ou des actions spécifiques se sont produits dans un système. Cela implique de conserver des journaux d'activité et des enregistrements pour établir une piste d'audit et vérifier les actions passées.