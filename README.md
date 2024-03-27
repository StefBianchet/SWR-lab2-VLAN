# SWR-lab2-VLAN
## Introduction

> 1. Donnez deux avantages concrets de l’utilisation des VLANs.

- Sécurité améliorée
- Les utilisateurs peuvent se déplacer sans changer de LAN.

> 2. Pour chaque affirmation, spécifiez si elle est vraie ou fausse : \
> a. Tous les membres d'un même VLAN sont dans le même domaine de broadcast. \
> b. Tous les membres d'un même VLAN sont dans le même domaine de collision. \
> c. Tous les membres d'un même VLAN doivent être connectés physiquement au même switch. \
> d. Tous les membres d'un même VLAN requièrent la capacité de travailler dans le mode full-duplex. 

a) Vrai
b) Faux
c) Faux
c) Faux

> 3. Quelle est la fonction du protocole 802.1Q (VLAN tagging) ?

Il ajoute un tag aux trames VLAN.

> 4. Une école d’ingénieurs dispose de deux VLANs : un VLAN ‘professeur-e-s’ et un VLAN ‘étudiant-e-s’. Comment est-il possible qu’étudiant accède au même serveur que son professeur ?

A l'aide d'un routeur les 2 VLAN peuvent communiquer

> 5. Décrivez brièvement le principe des VLAN par port.

Une machine se connecte par exemple au port 1 d'un switch qui appartient au VLAN 10. La machine sera donc connectée au 

> 6. Donnez deux inconvénients des VLAN par port. 

- Cela augmente la complexité de l'infrastructure.
- Un VLAN ne peut pas transmettre du traffic à un autre VLAN

## Configuration des ports access

> 8. Adapter ces mêmes commandes pour configurer le switch S2. Indiquer les commandes utilisées dans votre rapport.

```ios
Switch>enable
Switch#vlan database
% Warning: It is recommended to configure VLAN from config mode,
  as VLAN database mode is being deprecated. Please consult user
  documentation for configuring VTP/VLAN in config mode.

Switch(vlan)#vlan 1
VLAN 1 modified:
Switch(vlan)#vlan 2
VLAN 2 added:
    Name: VLAN0002
Switch(vlan)#vlan 3
VLAN 3 added:
    Name: VLAN0003
Switch(vlan)#exit
APPLY completed.
Exiting....
Switch#conf t
Switch(config)#inter
Switch(config)#interface e0/1
Switch(config-if)#swi
Switch(config-if)#switchport acce
Switch(config-if)#switchport access vlan 2
Switch(config-if)#exit
Switch(config)#interface e0/2          
Switch(config-if)#switchport access vlan 3
Switch(config-if)#exit
Switch(config)#interface e0/3          
Switch(config-if)#switchport access vlan 1
Switch(config-if)#exit
```

> 9. Testez la configuration sur S1. Depuis PC1, effectuez un ping sur une adresse IP 172.16.1.x inexistante. Quels PCs reçoivent la requête ARP ? Conclusion ?

Le seul PC à recevoir la requête ARP est le PC2. Le PC4 ne reçoit pas de requête car la liaison n'est pas faite entre les 2 switchs pour transmettre les VLANS.

## Configuration des ports trunk

> 11. Testez la configuration. Depuis PC1, envoyez un ping sur une adresse 172.16.1.x inexistante. Qui reçoit la requête ARP ? 

Tous les PCs du VLAN 1 reçoivent la requête ARP.

> 12. Analysez les trames échangées entre les deux switches. \
a) Indiquez l'emplacement et le format du 'VLAN tag' 802.1Q dans une trame Ethernet. \
b) Quel champ identifie le VLAN d'une trame ? \
c) Comparez deux trames de deux VLAN différentes pour vérifier vos propos. Attention : souvenez-vous que l'encapsulation 802.1Q n'a pas lieu sur tout le réseau.

![alt text](./screenshots/image.png)

> 13. Combien de VLANs di érents peuvent être gérés avec l’encapsulation 802.1Q ? 

> 14. L’encapsulation 802.1Q est-elle également utilisée sur les ports access ? 

> 15. Quelle est la longueur maximum d'une trame avec 802.1Q ? \
 a) Justifiez avec une capture Wireshark et comparez le résultat avec les trames sans 802.1Q. Grâce à l'option -s du ping, envoyez une trame d'une taille supérieure à 2000 bytes. La longueur de la trame a ichée sur Wireshark (on wire) ne prend pas compte du CRC (+ 4bytes). \
 b) Expliquez comment un ping avec une payload plus grande que le maximum peut nous permettre de déterminer de manière rigoureuse la taille maximum d'une trame. (question bonus)