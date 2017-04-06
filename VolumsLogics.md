# GESTIÓ DE VOLUMS LÒGICS
---
### __Descripció del que són.__

És una capa d'abstracció entre un dispositiu d'emmagatzematge i un sistema de fitxers.

### __Què volen dir les sigles, definició, analogies i exemples de comandes vistes a classe?__

+ PV: Vol dir Physical Volume, es una font d'emmagatzematge es a dir, un dispositiu que ens proporciona espai.
    + Exemples:
   
    *pvcreate* **/dev/sda**: Crea un PV.
   
    *pvs*: Visualitza els PVs que hagis creat.

+ VG: Vol dir Volume Group, discs virtuals. Està compost d'un o més PVs i pot anar creixent amb el temps (afegint-hi més PVs).

    + Exemples:
   
    *vgcreate* **nom** PV: Crea un VG.
   
    *vgs*: Visualitza els VGs que hagis creat.

+ LV: Vol dir Logical Volume, similar a les particions. Són els dispositius que utilitzarem per crear els sistemes de fitxers.

    + Exemples:
   
    *lvcreate -L* **size** *-n* **nom de LV** VG: Crea un LV  amb mides que tu li posis i al VG que tu li posis.
   
    *lvs*: Visualitza els LVs que hagis creat.
   
### __Entorn de pràctiques: Explicar com farem la pràctica detalladament (màquina virtual i afegir tres discs de 200M).__

Crearem una maquina virtual (en el meu cas Debian) amb el virt-manager i li afegirem 3 discs virtiO de 200M cadascun. Un cop fet això, iniciarem la màquina virtual i comprovarem que els discs s'han afegit correctament.

### __Pràctica 1: Creació d'un volum lògic a partir d'un dels tres discs durs (vda per exemple). Aquest volum lògic ha de ser del total de capacitat del disc. El volum de grup s'ha de dir practica1 i el volum lògic dades.__

Per fer això haurem d'executar aquesta comanda:
```
lvcreate -l 100%FREE -n dades practica1 
```
+ lvcreate com ja s'ha dit anteriorment crea un Volum Lògic.
+ El parametre -l serveix per determinar la mida del LV, en aquest cas amb 100%FREE li diem que ocupi tot l'espai del disc.
+ El parametre -n serveix per posar-li un nom al LV. Un cop fet això has de posar el nom d'un VG.

### __Pràctica 2: Creació d'un sistema de fitxers xfs al volum lògic creat i muntatge a /mnt. També s'ha de crear un fitxer amb dd de 180MB.__

Per fer això haurem d'executar les següents comandes:
```
mkfs.xfs /dev/practica1/dades
mount /dev/practica1/dades /mnt
```
I per crear el fitxer:
```
dd if=/dev/zero of=test.img bs=180M count=1
```
+ El que fa aquesta comanda es generar-te un fitxer que es digui test.img amb una mida de 180M al dispositiu /dev/zero. 

### __Pràctica 3: Creació d'un RAID 1 als dos discos sobrants (vdb i vdc per exemple).__

Ho farem amb aquesta comanda:
```
mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/vdb /dev/vdc
```
+ Aquesta comanda et crea al dispositiu /dev/md0 un RAID de nivell 1 (--level), a partir de 2 discos (--raid-devices) que en aquest cas seran /dev/sdb i /dev/sdc.

### __Pràctica 4: Ampliació del volum lògic de dades al raid.__

Per fer això utilitzarem aquesta comanda:
```
lvextend -l +100%FREE /dev/practica1/dades /dev/md0 
```
+ Fa una extensió del volum logic /dev/dades/practica1 del tamany maxim, afegint el dispositiu RAID /dev/md0.

### __Pràctica 5: Ampliació del sistema de fitxers xfs al tamany actual del volum lògic dades (s'ha de poder fer sense desmuntar-lo de /mnt ja que és xfs). Una vegada creat crearem un nou fitxer de 180M.__

Necessitarem executar aquestes comandes:
```
xfs_growfs /dev/practica1/dades
dd if=/dev/zero of=test2.img bs=180M count=1
```
