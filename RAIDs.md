# SISTEMES RAID

#### __Resum de sistemes RAID fent servir una taula com la vista a classe:__

| Nivells | Nº Min Discs | Nº Max Discs Fallats | Capacitat |  Read    |   Write  |
|---------|:------------:|:--------------------:|:---------:|:--------:|:--------:|
| Raid 0  |       2      |               0      |    100%   | Excellent| Excellent|
| Raid 1  |     2 (Màx)  |               1      |     50%   | V.Good   | Good     |
| Raid 5  |       3      |               1      |  67%-94%  | V.Good   | Good     |
| Raid 6  |       4      |               2      |  50%-88%  |  Good    | Good     |
| Raid 10 |       4      |            1/mirror  |     50%   | V.Good   | Good     |


#### __Descripció de la metodologia utilitzada a classe per a fer proves amb màquines virtuals.__

Creem una nova maquina virtual i li afegim els discos necessaris per muntar el RAID que volguem, quan ja haguem muntat el RAID desitjat, i per comprovar que funciona desactivarem un dels discos que hem afegit anteriorment.

#### __Comandes i descripció de les mateixes per tal de crear un sistema RAID1.__

Amb la comanda *mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sdb /dev/sdc*:

El paramentre **--create** et crea un sistema de fitxers amb el nom que li posis, **--level=1** designa que el raid que vols crear es un RAID1, **--raid-devices=2** serveix per posar el numero de discs que vols posar al RAID i la ruta dels mateixos, en aquest cas volem 2 discos: /dev/sdb i /dev/sdc.
   
#### __Comandes i descripció de les mateixes per tal de crear un sistema RAID5.__
   
Amb la comanda *mdadm --create /dev/md0 --level=5 --raid-devices=3 /dev/sdb /dev/sdc /dev/sdd*

El paramentre **--create** et crea un sistema de fitxers amb el nom que li posis, **--level=5** designa que el raid que vols crear es un RAID5, **--raid-devices=3** serveix per posar el numero de discs que vols posar al RAID i la ruta dels mateixos, en aquest cas volem 3 discos: /dev/sdb , /dev/sdc i /dev/sdd.

#### __Comandes i descripció de les mateixes per tal de crear un sistema RAID6.__

Amb la comanda *mdadm --create /dev/md0 --level=6 --raid-devices=4 /dev/sdb /dev/sdc /dev/sdd /dev/sde*

El paramentre **--create** et crea un sistema de fitxers amb el nom que li posis, **--level=6** designa que el raid que vols crear es un RAID6, **--raid-devices=4** serveix per posar el numero de discs que vols posar al RAID i la ruta dels mateixos, en aquest cas volem 4 discos: /dev/sdb , /dev/sdc , /dev/sdd i /dev/sde.

#### __Comandes i descripció de les mateixes per tal de crear un sistema RAID10.__

Amb la comanda *mdadm --create /dev/md0 --level=10 --raid-devices=4 /dev/sdb /dev/sdc /dev/sdd /dev/sde*

El paramentre **--create** et crea un sistema de fitxers amb el nom que li posis, **--level=10** designa que el raid que vols crear es un RAID10, **--raid-devices=4** serveix per posar el numero de discs que vols posar al RAID i la ruta dels mateixos, en aquest cas volem 4 discos: /dev/sdb , /dev/sdc , /dev/sdd i /dev/sde.
