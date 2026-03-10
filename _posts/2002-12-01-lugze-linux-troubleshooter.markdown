---
layout: post
title:  "LugZe Linux Troubleshooter"
author: lugze
date:   2002-12-01 12:00:00 +0100
categories: blog
---

LugZe -= ze.lugbih.org =- Predstavlja:

Vodic kroz Linux OS, pomoc pri koristenju, linux trikovi... Troubleshooter

## Uvod

Ovaj tekst predstavlja skup najcescih problema i njihovih rjesenja, koji ce desavaju pri radu sa linuxom, te je namijenjen iskljucivo linux pocetnicima. Sve sugestije i komentari su dobrodosli. Ako zelite sta dodati tekstu, molim da se obratite na mail grungy@linux.org.ba.

## Najcesci problemi prilikom rada sa Linuxom

### Kako ponovo vratiti izgubljeni lilo?

**Opis problema:**

Desio vam se problem da lilo vise nije funkcionalan, npr. prilikom bootanja racunara pokaze vam se samo "LI" (umjesto lilo izbornika) ili ste instalirali drugi operativni sistem (windows) pored linuxa, naknadno, i izgubili ste lilo tako da se on uopste ne pojavljuje, vec direktno se podize taj sekundarni operativni sistem.

**Rjesenje:**

Podignite (bootajte) sistem sa vase linux boot diskete i kada se podigne linux i izvrsite prijavu korisnika u konzoli kucate `lilo` (bez navodnika) i problem je rijesen. Racunar ce procitati lilo konfiguracijski fajl `/etc/lilo.conf` i vas stari lilo ce biti ponovo vracen i funkcionalan - ponovo zapisan u boot sektor. Ako posjedujete prvi SuSe instalacijski cd jedne od novijih distribucija a nemate linux boot diskete, sistem mozete podici i putem tog prvog, boot cd-a, kao da zelite instalirati SuSe samo sto na jednom od pocetnih koraka izaberete "Boot Instaled System" umjesto "News Instalation", kasnije izaberete particiju na kojoj vam je instaliran vas linux (naitive particiju). Naravno ovaj korak nije potreban ako posjedujete linux boot disketu.

**Napomena:** da bi ste izvrsili ove radnje morate imati root (administracijske) privilegije!

---

**Autori:**

- Semir Mujkic - semir@hotpop.com
- Nedim Hadzimahmutovic - grungy@linux.org.ba
- Kemal Sanjta - gomez@codelinux.com

---
*Izvor: [lugze/archive](https://github.com/lugze/archive/tree/master/dokumentacija)*
