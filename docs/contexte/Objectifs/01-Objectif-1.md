# Objectif stratégique 1 : Réduire les coûts

L’entreprise bien qu’encore en pleine croissance perçoit un tassement du
marché sur lequel elle travaille : la concurrence se fait plus rude, les
clients sont de plus en plus regardant sur les prix.  
Pour maintenir sa position sur son marché, elle doit absolument
maintenir ses prix de vente. Cela passe par une maîtrise totale de ses
coûts de production, mais également de ses coûts structurels. L’audit
ayant montré que les coûts induits par les dysfonctionnements de son SI
étaient nombreux, la direction demande à la DSI de travailler dans le
sens d’une réduction des coûts d’infrastructure et de fonctionnement du
SI.

## Stratégie Operationnelle : Réorganisation au sein d’une architecture unique

Informatiquement parlant, il est possible de considérer la filiale de
Bourges de deux façons :

\- Soit comme un partenaire communiquant avec *SportLudique*,

\- Soit comme faisant partie intégrante de l’infrastructure de *SportLudique*.

La direction souhaitant absorber juridiquement cette filliale, il paraît
évident de l’absorber dans la l’infrastructure de *SportLudique* tout en conservant ses spécificités:

Il en découle que l’entreprise sera réorganisée de la façon suivante :

-   Les trois sites de Chartres, Orléans et Tours posséderont chacun un
    serveur d’infrastructure lié au domaine auquel il appartient,

-   <del>La succursale de Bourges, qui ne concerne que dix utilisateurs,
    n’aura ni serveur d’infrastructure, ni domaine. Le SI sera
    accessible par un moyen sécurisé en utilisant une connexion
    distante.</del>

-   Toutefois, pour des raisons pédagogique la succursale de Bourges disposera de son infrastructure autonome.

### Choix de la solution d’infrastructure organisationnelle

Les serveurs d’infrastructure auront les rôles de services réseaux de base, tels
que serveurs DNS, serveurs DHCP, Annuaure Active Directory.

La DSI a retenu la mise en œuvre d’un annuaire Active Directory basé sur
un modèle de forêt unique reposant sur des serveurs Windows 2019 minimum.

Cette solution permet d’exploiter les avantages de l’annuaire Active
Directory autour du nom de domaine ***sportludique.fr***. Le fait de
rassembler l’organisation de l’entreprise sous une forme de forêt unique
ne ferme pas les portes sur les possibilités d’isoler une partie de
l’entreprise ayant des besoins spécifiques, en matière de sécurité par
exemple.

L’annuaire Active Directory permet d’exploiter de nouvelles
fonctionnalités telles que la prise en compte des notions de site,
d’unité organisationnelle, de groupe universel.

On pourra appliquer des stratégies de groupe aux utilisateurs et aux
ordinateurs en fonction de critères multiples.

Par cette réorganisation, l’entreprise va réduire considérablement le
trafic réseau et les relations d’approbation au travers du réseau. Elle
conservera une certaine indépendance au niveau de l’administration, tout
en intégrant sa nouvelle filiale au sein d’une organisation unique.

### Refonte du plan d’adressage IP

Cette réorganisation est l’occasion rêvée de remettre à plat le plan
d’adressage IP et le plan de nommage afin d’harmoniser et de simplifier
l’utilisation du réseau au travers des différents sites, de clarifier
les rôles des serveurs et d’anticiper le futur (rachat de nouvelles
sociétés par exemple).
