---
layout: post
title:  "Kratki opis Linux Filesistema (pregled direktorijskog stabla)"
date:   2002-10-07 17:55:20 +0100
categories: blog
---


Nedim Hadzimahmutovic grungy@linux.org.ba v0.2


U ovom poglavlju mozete procitati o tome kako je linux direktorijsko stablo organizovano. Citavo stablo je tako napravljeno da ga je moguco podijeliti u manje dijolve, tako da je svaki zasebno sposoban biti na odvojenoj particiji ili cak hard disku tako da ti dijelovi mogu biti ograniceni na odredjenu velicinu, sto zavisi od velicine particije . Ovo prije svega omogucuje laksu administraciju masine. Glavni dijelovi su root (/), /usr, /var, i /home filesistemi. Svaki dio ima odredjenu svrhu. Direktorijsko stablo je tako dizajnirano da veoma dobro radi i mrezi linux masina koje mogu da dijele medjusobno neke dijelove filesistema.

* root filesistem
* /usr filesistem
* /var filesistem
* /home filesistem



`/bin`

* U ovom direktoriju se nalaze komande koje su potrebne prilikom podizanja sistema, i kmande koje koriste normalno korisni prilikom rada, odnosno poslije dizanja sistema.

`/sbin`

* Slican /bin direktoriju, samo sto sadrzi komande koje nisu namijenjene normalnim korisnicima, znaci komande koje uglavnom koristi root.


`/etc`

* Konfiguracijske datoteke specificne za masinu, kako ih mi podesimo.


`/root`

- Kucni, home, direktorij za root korisnika. Ovaj direktorij inace nije pristupan normalnim korisnicima na sistemu.


`/lib`

* Biblioteke koje su potrebne za pokretanje programa.


`/lib/modules`

* Loadable kernel moduli, pogotovo oni koji su potrebni za oporavak sistema poslije pada sistema.


`/dev`

* Device datoteke.

`/tmp`

* Trenutne datoteke. Medjutim danas se trenutne datoteke uglavnom smjestaju i /var/tmp direktorij i programi koji se pokrecu nakon dozanja sistema bi trebali da koriste ovaj direktorij. Direktorij /tmp je cesto simbolicna veza (link) na /var/tmp dir.


`/boot`

* Datoteke koje su koristene od LILO izbornika.



`/mnt`

* Tacka u kojoj su smjesteni trenutno mountirani uredjaji itd.


Za pojedinacne opise vaznijih direktorija ( `/etc, /dev, /usr, /var, /proc` ) i datoteka pod njima, pogledajte sljedeci link: http://ze.lugbih.org/textware



copyleft LugBih, LugZe
