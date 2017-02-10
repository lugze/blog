---
layout: post
title:  "/sys : Uvod u sysfs"
author: nedim
date:   2017-02-09 19:41:10 +0100
categories: linux sysfs 101
tags: [linux, proc]
---

* Sysfs je spoj `proc`, `devfs`, and `devpty` virtuelnih file sistema te i sam je virtuelni file sistem. 
* Osnovna svrha mu je pružanje informacija o hardverskoj komponenti sistema userspace programima kao sto je udev.
* Ovaj virtuelni sistem je aktuelan od Linux 2.6 kernel verzije cime su virtuelni fajlovi vezani za hardver izmjesteni iz /proc direktorija.
* Pristup sysfs-u se moze izvrsiti pristupum /sys/ direktoriju iz shella
* Informacije koje se nalaze u sysfs-u su zapisane u `plain text` formatu im ogu im pristupiti kako sistem administratori tako i programi
* sysfs je baziran na `ramfs` programskom kodu u kernel verziji 2.4.
* originalni naziv za sysfs bio je `ddfs` (Device Driver Filesystem)
* `ddfs` u kernelu 2.5 je preimenovan u `driverfs` a prosirenjem funkcionalnosti postao je `sysfs`
 
Sysfs je virtuelni file sistem koji dinamicki kreira i puni sadrzajem Linux kernel. Sadrzaj se odnosi na informacije vezane za hardver te drivere za taj isti hardver. Na ovaj nacin pristupamo iz user space-a preko virtuelnih fajlova do informacija koje se nalaze u kernel space-u. Osim sto ove virtuelne fajlove mozemo koristiti za citanje informacija o hardveru neke od njih mozemo koristiti za konfigurisanje odredjenog hardvera.


### Lokacija

Sysfs file sistem je mountiran na putanju /sys/ i sadrzi direktorije pomocu kojih mozemo saznati informacije o uredjajima koji su na razlicite nacine povezani na racunar.


## Mountiranje sysfs

Sysfs, kao i bilo koji virtuelni file sistem smjesten u memoriji, moze se mountati iz userspace-a pomocu `mount` komande. 
Defaultna lokacija se mounta automatski prilikom bootanja sistema ali vjezbe radi `sysfs` cemo mountati u direktorij po izboru. 
Nakon toga cemo porediti da li je isti sadrzaj u defaultnoj i nasoj lokaciji iz vjezbe.

* Napravite direktorij u koji cemo mountati sysfs

```
 mkdir /mnt/sysfs
```

* Izvrisite mount sysfs-a iz RAMA u `/mnt/sysfs`

```
mount -t sysfs sysfs /mnt/sysfs/
```

* Provjeriti da li postoji sadrzaj nakon mount-a

```
ls /mnt/sysfs/
```
* Trebali bi dobiti nesto slicno sadrzaju ispod

```
block  bus  class  dev  devices  firmware  fs  hypervisor  kernel  module  power
```

* Sada je potrebno porediti da li isti sadrzaj ima defaultna sysfs lokacija te nas direktorij
 * listing defaultne sysfs lokacija
```
ls /sys/
```
 * listing naseg direktorija

```
ls /mnt/sysfs/
```

sadrzaj je isti.

Nakon ove vjezbe potrebno je uraditi `unmount`

* ```umount /mnt/sysfs```

Te provjeriti da li je unmountirani direktorij prazan

* ```ls /mnt/sysfs/```


## Opis /sys poddirektorija


## Tree prikaz

Koristan alat za prikaz strukture /sys/ direktorija je tree komanda. 

Komanda za tree prikaza `/sys`.

```
tree -L 1 /sys/
```

Dobijemo sljedeci ispis.

```
/sys/
├── block
├── bus
├── class
├── dev
├── devices
├── firmware
├── fs
├── hypervisor
├── kernel
├── module
└── power
```

## Opis osnovnih poddirektorija `/sys/`

### /sys/block poddirektorij

Block direktorij sadrzi poddirektorije za sve `block` uredjaje koji su otkriveni od strane sistema. 
Block uredjaji su svi uradjaji koji mogu biti sluzeni za skladistenje podataka kao sto su diskovi, ram memorije itd. 
Svaki uredjaj sadrzi svoj poddirektorij koji sadrzi atribute uredjaja kao sto je velicina itd.

#### Primjer

Recimo da imamo disk na sistemu koji je prijavljen kao `sda` i pokretanjem komande ispod mozemo saznati sve prijavljene informacije i disku..

```
ls /sys/block/sda/
```

U navedenom direktoriju se nalaze fajlovi i poddirektoriji koji sadrze sve potrebne informacije. Recimo velicinu diska mozemo saznati

```
cat /sys/block/sda/size 
```

### /sys/bus poddirektorij

`Bus' direktorij sadrzi poddirektorije za svaku fizicku sabirnicu odnosno bus koja je prijavljena u kernelu. Primjer tree prikaza poddirektorija unutar bus direktorija:

```
/sys/bus/
├── acpi
├── clockevents
├── clocksource
├── container
├── cpu
├── edac
├── event_source
├── i2c
├── iscsi_flashnode
├── machinecheck
├── mc0
├── mdio_bus
├── memory
├── mipi-dsi
├── mmc
├── nd
├── node
├── pci
├── pci_express
├── platform
├── pnp
├── rapidio
├── scsi
├── sdio
├── serio
├── spi
├── usb
├── virtio
├── vme
├── workqueue
├── xen
└── xen-backend

```

Direktorij koji odgovara svakom pojedinacnom bus-u u sys direktoriju sadrzi dva poddirektorija i to `devices` i `drivers`.  

#### /sys/bus/*/devices/ direktorij

Direktorij `devices` sadrzi sve uredjaje tog tipa koji su otkriveni na citavom sistemu. 

Primjer tree prikaza devices poddirektorija za pci bus

```
tree -L 1 /sys/bus/pci/devices/
/sys/bus/pci/devices/
├── 0000:00:00.0 -> ../../../devices/pci0000:00/0000:00:00.0
├── 0000:00:01.0 -> ../../../devices/pci0000:00/0000:00:01.0
├── 0000:00:02.0 -> ../../../devices/pci0000:00/0000:00:02.0
├── 0000:00:06.0 -> ../../../devices/pci0000:00/0000:00:06.0
├── 0000:00:16.0 -> ../../../devices/pci0000:00/0000:00:16.0
├── 0000:00:1a.0 -> ../../../devices/pci0000:00/0000:00:1a.0
├── 0000:00:1c.0 -> ../../../devices/pci0000:00/0000:00:1c.0
├── 0000:00:1c.5 -> ../../../devices/pci0000:00/0000:00:1c.5
├── 0000:00:1c.7 -> ../../../devices/pci0000:00/0000:00:1c.7
├── 0000:00:1d.0 -> ../../../devices/pci0000:00/0000:00:1d.0
├── 0000:00:1e.0 -> ../../../devices/pci0000:00/0000:00:1e.0
├── 0000:00:1f.0 -> ../../../devices/pci0000:00/0000:00:1f.0
├── 0000:00:1f.2 -> ../../../devices/pci0000:00/0000:00:1f.2
├── 0000:00:1f.3 -> ../../../devices/pci0000:00/0000:00:1f.3
├── 0000:01:00.0 -> ../../../devices/pci0000:00/0000:00:01.0/0000:01:00.0
├── 0000:04:00.0 -> ../../../devices/pci0000:00/0000:00:1c.5/0000:04:00.0
└── 0000:05:00.0 -> ../../../devices/pci0000:00/0000:00:1c.7/0000:05:00.0
```

#### drivers dir

Ovaj direktorij sadrzi poddirektorije za svaki device driver koji je prijavljen za taj tip sabirnice. 
Unutar tih direktorija se nalaze atributi pomocu kojim mozemo vidjeti postavke drivera te ih modifikovati.


### /sys/class direktorij

Kao sto ime samo govori class direktorij sadrzi klase koje logicki opisuju hardver. 
Klase predstavljaju nivo apstrakcije koje na intuitivan nacin daju imena hardverskim komponentama.
Primjeri:

#### Svi mrezni uredjaji se nalaze u podrektoriju

ls /sys/class/net

#### Svi input uredjaji se nalaze u poddirektoriju

ls /sys/class/input

#### Serijski uredajaji se nalaze

ls /sys/class/tty

#### Svi block uredjaji se nalaze

ls /sys/class/block/


Svaki uredjaji odredjene klase sadrzi fajlove i direktorije koje sadrze dodatne informacije o tome uradjaju. 

#### Primjeri vezani za mreznu karticu

##### Kako saznati da li je kabl ukljucen u mreznu karticu?

```
cat /sys/class/net/eth0/carrier
```
* 0 - iskljuceno
* 1 - ukljuceno


## /sys/firmware direktorij

firmware direktorij sadrzi interfejse za pregled i manipulisanje atributa koji su specificni za firmware kao sto je BIOS. 

Tree prikaz firmwware direktorija

```
/sys/firmware/
├── acpi
├── dmi
└── memmap
```

## /sys/module direktorij

Ovaj direktorij sadrzi poddirektorije za svaki modul koji je ukljucen u kernel. Module mozemo izlistati pomocu komande

```
ls /sys/module/
```
ili komnde

```
lsmod
```
