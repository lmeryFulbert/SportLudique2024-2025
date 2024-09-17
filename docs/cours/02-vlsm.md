# 02-VLSM (Variable Length Subnet Mask)
## Introduction

Le **VLSM (Variable Length Subnet Mask)** est une technique d'adressage IP qui permet de subdiviser un réseau en sous-réseaux de tailles différentes, en fonction des besoins. Contrairement à la technique classique des sous réseaux - **FLSM (Fixed Length Subnet Mask)**, où tous les sous-réseaux ont la même taille, le VLSM permet une utilisation plus efficace de l'espace d'adressage.

### Avantages du VLSM

-    Efficacité de l'utilisation des adresses IP : Permet de minimiser le gaspillage des adresses IP en allouant des sous-réseaux de tailles adaptées aux besoins.
-    Flexibilité : Permet de créer des sous-réseaux de différentes tailles à partir du même espace d'adressage.
-    Scalabilité : Facilite l'extension du réseau en créant de nouveaux sous-réseaux selon les besoins.

??? info "Attention"
    **VLSM** est une technique d'optimisation pour l'adressage utile dans des plages d'adresse publiques. Dans un contexte d'adresse privées (**RFC1918**), cela a nettement moins d'interet.

??? info "RFC 1918"
    Les plages d'adresses privées définies dans cette RFC interdisent leur routage sur Internet. On a :</br>
    -    10.0.0.0 /8  </br>
    -    172.16.0.0 /12 </br>
    -    192.168.0.0 /16 </br>

### Principe de fonctionnement

-    Détermination des besoins en sous-réseaux : Identifiez le nombre de sous-réseaux et le nombre d'hôtes requis pour chaque sous-réseau.

-    Allouer des sous-réseaux à l'aide de masques de sous-réseau de longueurs variables :
-    Commencez par le plus grand sous-réseau (Il est très important de trier avant de commencer a travailler).
-    Choisissez un masque de sous-réseau qui satisfait le nombre d'hôtes requis.
-    Continuez à subdiviser les sous-réseaux restants pour répondre aux autres besoins en utilisant des masques de sous-réseau appropriés.

### Exemple de mise en oeuvre

Supposons que vous avez une adresse réseau 192.168.1.0/24 et que vous devez créer les sous-réseaux suivants en utilisant la technique VLSM :

-    Sous-réseau A : 50 hôtes
-    Sous-réseau B : 25 hôtes
-    Sous-réseau C : 10 hôtes

#### Étapes

-    Sous-réseau A : 50 hôtes → Nécessite 6 bits pour les hôtes (2^6 - 2 = 62 hôtes).
-    Masque de sous-réseau : /26 (255.255.255.192)
-    Sous-réseau : 192.168.1.0/26
-    Plage d'adresses : 192.168.1.1 à 192.168.1.62
----
-    Sous-réseau B : 25 hôtes → Nécessite 5 bits pour les hôtes (2^5 - 2 = 30 hôtes).
-    Masque de sous-réseau : /27 (255.255.255.224)
-    Sous-réseau : 192.168.1.64/27
-    Plage d'adresses : 192.168.1.65 à 192.168.1.94
----
-    Sous-réseau C : 10 hôtes → Nécessite 4 bits pour les hôtes (2^4 - 2 = 14 hôtes).
-    Masque de sous-réseau : /28 (255.255.255.240)
-    Sous-réseau : 192.168.1.96/28
-    Plage d'adresses : 192.168.1.97 à 192.168.1.110

## Conclusion

Le VLSM est une technique puissante qui permet une gestion plus granulaire et efficace de l'espace d'adressage IP en créant des sous-réseaux de différentes tailles selon les besoins spécifiques. Cela permet d'optimiser l'utilisation des adresses IP, surtout dans les grands réseaux.