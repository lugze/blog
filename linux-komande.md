---
layout: page
title: Linux komande
permalink: /linux-komande/
---

Referenca Linux komandi od A do Z. Komande označene sa **(zastarjelo)** su zamijenjene modernijim alternativama.

#### A

`adduser` - Kreiranje korisničkih naloga.

`anacron` - Administrativna komanda koja se pokreće pri podizanju sistema i periodično izvršava komande. Lista poslova se podrazumijevano čita iz datoteke /etc/anacrontab.

`apropos` - Na standardnom izlazu prikazuje ime i opis svih komandi koje u opisu imaju zadati string.

`apt-get` - Debian Package Management System - alat za rad sa paketima iz komandne linije. Front-end za APT.

`aptitude` - Debian Package Management System - alat za interaktivni rad sa paketima. Front-end sa sistemom tekstualnih menija za APT.

`arch` - Prikazuje arhitekturu računara na standardnom izlazu (kao `uname -m`).

`arp` - TCP/IP administrativna komanda za rad sa ARP kešom kernela. ARP se koristi za prevođenje IP adresa u MAC adrese mrežnih adaptera. **Napomena:** na modernim sistemima koristite `ip neigh`.

`at` - Komanda kojom se zakazuje izvršenje drugih komandi u određeno vrijeme.

`atd` - Daemon koji izvršava komande zakazane komandom `at`. Normalno se pokreće prilikom podizanja sistema.

`atq` - Prikazuje zakazane `at` poslove korisnika. U slučaju da komandu zada superuser, prikazuju se svi zakazani poslovi.

`atrm` - Brisanje zakazanih `at` poslova.


#### B

`badblocks` - Administrativna komanda za analizu površine diskova.

`basename` - Izdvaja ime datoteke iz pune putanje, uklanjajući direktorijumski prefiks i opcioni sufiks (na primer: `basename /home/korisnik/fajl.txt` ispisuje `fajl.txt`). Komanda je korisna za shell programiranje.

`bash` - Bash komandni interpreter (Bourne-Again Shell).

`batch` - Slično komandi `at`, izvršava komande date na standardnom ulazu. Ukoliko se vrijeme izvršenja ne navede, komande se izvršavaju kada opterećenje sistema (load average) padne ispod praga 1.5.

`bc` - Interaktivni kalkulator koji ulazne podatke prima sa standardnog ulaza ili iz datoteke.

`bzip2` - Paket za kompresiju sličan programu gzip koji koristi drugačije algoritme i postiže veći stepen kompresije. Paket uključuje programe za kompresiju i dekompresiju (bzip2, bunzip2), pregledanje sadržaja (bzcat, bzless, bzmore) i oporavak (bzip2recover).


#### C

`cal` - Prikazuje kalendar za tekući mjesec. Takođe može prikazati godišnji ili mjesečni kalendar za godinu i mjesec koji se navode kao parametri.

`cancel` - Uklanjanje poslova iz reda za štampu (System V).

`cat` - Konkatenacija datoteka i prikazivanje na standardnom izlazu.

`cfdisk` - Administrativni program sa sistemom menija za particionisanje diska.

`chgrp` - Promjena grupe kojoj objekat sistema datoteka pripada. U opštem slučaju ovu komandu može da izvrši root, a na nekim sistemima može i vlasnik objekta.

`chmod` - Promjena pristupnih prava objekta sistema datoteka. Ovu komandu mogu da izvrše root i vlasnik objekta.

`chown` - Promjena vlasnika objekta sistema datoteka. U opštem slučaju ovu komandu može da izvrši root, a na nekim sistemima može i vlasnik objekta.

`chpasswd` - Administrativna komanda za grupnu promjenu lozinki korisnika (čita parove korisnik:lozinka sa standardnog ulaza).

`chsh` - Promjena komandnog interpretera koji se pokreće nakon login procesa. Ime komandnog interpretera se navodi sa apsolutnom putanjom.

`chvt` - Prelazak na virtuelni terminal N. Ukoliko terminal ne postoji, biće napravljen. Ekvivalentno kombinaciji tastera Ctrl+Alt+N, gdje je N broj terminala.

`cksum` - Izračunavanje CRC kontrolne sume za datoteku.

`clear` - Brisanje ekrana terminala.

`cmp` - Upoređivanje datoteka i prikazivanje prve razlike na standardnom izlazu.

`compress` - Program za kompresiju datoteka. **(zastarjelo)** Gzip i bzip2 se danas koriste umjesto ovog programa.

`cp` - Kopiranje datoteke, grupe datoteka ili dijelova direktorijumskog stabla. Takođe se može koristiti za kreiranje linkova.

`cpio` - Arhiviranje i dearhiviranje datoteka (copy-out i copy-in). Takođe se može koristiti za kopiranje datoteka u aktivnom UNIX stablu (copy-pass).

`cron` - Administrativna komanda koja se pokreće pri podizanju sistema i periodično izvršava komande. Cron provjerava korisničke crontab datoteke (nalaze se u direktorijumu /var/spool/cron/crontabs, a imenovane su na osnovu korisničkih naloga) svaki minut i pokreće programe koje tada treba izvršiti.

`crontab` - Zakazivanje periodičnog izvršenja komandi u specificiranim intervalima. Zavisno od konkretnog UNIX sistema, izvršenje mogu zakazati svi ili samo privilegovani korisnici.

`curl` - Alat za prenos podataka sa ili na server koristeći podržane protokole (HTTP, HTTPS, FTP, SFTP i mnoge druge). Veoma fleksibilan alat za rad sa web servisima i API-jima.


#### D

`date` - Prikazuje ili postavlja trenutni datum i vrijeme.

`dd` - Konvertuje i kopira datoteku ili određeni dio medijuma. Prilikom pristupa medijumu može zaobići sistem datoteka, čime je omogućeno kopiranje medijuma koji nisu ni u jednom od formata koje UNIX prepoznaje.

`debugfs` - Administrativna komanda kojom se ostvaruje pristup zaglavlju i meta-data strukturama ext2/ext3/ext4 sistema datoteka.

`depmod` - Kreira datoteku u kojoj je opisana međusobna zavisnost programskih modula kernela.

`df` - Prikazuje iskorištenost aktiviranih sistema datoteka.

`diff` - Upoređuje datoteke i prikazuje sve razlike na standardnom izlazu.

`dig` - Komanda za slanje upita DNS serverima, fleksibilnija od `nslookup` komande.

`dpkg` - Debian Package Management System - rad sa paketima iz komandne linije.

`du` - Prikazuje količinu prostora na sistemu datoteka koju zauzimaju datoteke u poddirektorijumima tekućeg direktorijuma.

`dumpe2fs` - Administrativna komanda koja na standardnom izlazu prikazuje informacije iz superbloka sistema datoteka.


#### E

`e2fsck` - Administrativna komanda za provjeru integriteta ext2, ext3 i ext4 sistema datoteka.

`e2image` - Administrativna komanda za kreiranje slike (image) značajnijih dijelova sistema datoteka (kao što je superblok) na izmjenljivom medijumu.

`e2label` - Administrativna komanda za prikazivanje i promjenu imena (labele) sistema datoteka.

`echo` - Prikazuje niz karaktera ili vrijednost promjenljive na standardnom izlazu.

`edquota` - Editor kvota.

`egrep` - Traži proširene regularne izraze u datoteci. Na modernim sistemima ekvivalentno sa `grep -E`.

`emacs` - Emacs tekst editor.

`env` - Prikazuje vrijednosti promjenljivih koje čine okruženje, ili pokreće komandu u modifikovanom okruženju.

`expr` - Obavlja jednostavne aritmetičke operacije.

#### F

`fdisk` - Administrativni program za particionisanje hard diskova.

`fgconsole` - Prikazuje broj trenutno aktivne virtuelne konzole (na primer 2, ukoliko korisnik radi na /dev/tty2).

`find` - Traži datoteku na osnovu zadatih kriterijuma u aktivnom UNIX stablu.

`finger` - Prikazuje informacije o korisnicima, uključujući i informacije iz datoteka .plan i .project u home direktorijumu korisnika.

`free` - Prikazuje informacije o iskorištenosti operativne memorije i swap prostora.

`fsck` - Administrativna komanda za provjeru integriteta sistema datoteka.

`ftp` - Interaktivni program za transfer datoteka između dva udaljena sistema. **(zastarjelo)** Koristite `sftp` ili `scp` za siguran transfer.


#### G

`grep` - Traži regularne izraze u datotekama. Jedna od najkorištenijih Linux komandi.

`groupadd` - Administrativna komanda za kreiranje nove korisničke grupe.

`groupdel` - Administrativna komanda za brisanje postojeće korisničke grupe.

`groupmod` - Administrativna komanda za modifikovanje parametara grupe.

`groups` - Prikazuje grupe kojima navedeni korisnik pripada.

`grpck` - Administrativna komanda za provjeru integriteta datoteka /etc/group i /etc/gshadow.

`gunzip` - Dekompresija .gz datoteka.

`gzip` - Kompresija datoteka u .gz format.


#### H

`halt` - Administrativna komanda za zaustavljanje sistema. Ukoliko se sistem nalazi u nivoima izvršenja 0 ili 6, halt zaustavlja sve procese, a inače poziva komandu `shutdown -h`.

`hdparm` - Administrativna komanda za pregledanje i postavljanje parametara hard diskova. Koristi se uglavnom na IDE/SATA diskovima.

`head` - Prikazuje početak datoteke (podrazumijevano prvih 10 linija).

`hexdump` - Prikazuje datoteku u heksadecimalnom ili oktalnom formatu.

`host` - Prikazuje informacije o računarima i zonama u DNS domenu.

`hostname` - Prikazuje ime računara, pri čemu privilegovani korisnik može dodijeliti novo ime računaru.

`hwclock` - Administrativna komanda kojom privilegovani korisnik može podesiti hardverski (RTC) sat sistema.


#### I

`id` - Prikazivanje informacija o korisnicima, uključujući UID, GID i članstvo u grupama.

`ifconfig` - TCP/IP administrativna komanda za konfigurisanje mrežnih interfejsa rezidentnih u kernelu. **(zastarjelo)** Na modernim sistemima koristite `ip addr` i `ip link`.

`init` - Osnovni proces (PID 1) i administrativna komanda za inicijalizaciju sistema i promjenu nivoa izvršenja. Na modernim sistemima zamijenjen sa `systemd`.

`ip` - Moderna komanda za upravljanje mrežnim interfejsima, rutiranjem, tunelima i ARP kešom. Zamjenjuje `ifconfig`, `route`, `arp` i `netstat`.

`ipchains` - Administrativna komanda za konfigurisanje firewalla u Linux kernelu 2.2. **(zastarjelo)** Zamijenjeno sa `iptables`, a zatim `nftables`.

`iptables` - Administrativna komanda za konfigurisanje firewalla (netfilter) u Linux kernelu 2.4+. Na modernim sistemima zamjenjuje se sa `nftables`/`nft`.


#### J

`journalctl` - Komanda za pregled logova iz systemd journal sistema. Zamjenjuje tradicionalno čitanje log fajlova iz /var/log/.


#### K

`kill` - Šalje signale procesu sa poznatim PID-om.

`killall` - Šalje signale svim procesima nastalim pokretanjem određenog programa (kao argument se navodi ime programa).


#### L

`last` - Prikazuje nekoliko posljednjih login procedura, odnosno imena korisnika, terminal, ime udaljenog računara i vrijeme prijavljivanja na sistem.

`lastb` - Prikazuje nekoliko posljednjih neuspješnih login procedura, u istom formatu kao i `last`.

`lastlog` - Prikazuje sve korisnike sistema i vrijeme kada su se zadnji put prijavili na sistem.

`less` - Interaktivni program za pregledanje sadržaja tekstualnih datoteka. Napredniji od `more`.

`ln` - Kreiranje hard i simboličkih linkova.

`locale` - Štampa izvještaj o regionalnim podešavanjima na standardnom izlazu.

`login` - Prijavljivanje na sistem. Treći proces u nizu init-getty-login-shell.

`logname` - Prikazuje ime korisnika koji je prijavljen na sistem na osnovu podataka u datoteci /var/run/utmp.

`look` - Prikazuje riječi iz datoteke /usr/share/dict/words koje počinju zadatim nizom karaktera.

`ls` - Prikazuje sadržaj direktorijuma na standardnom izlazu.

`lsattr` - Prikazuje specijalne atribute datoteka karakteristične za ext2/ext3/ext4 sisteme datoteka.

`lsblk` - Prikazuje informacije o blok uređajima (diskovi, particije) u formatu stabla.

`lsmod` - Prikazuje module učitane u tekuće jezgro.

`lsof` - Prikazuje otvorene datoteke i procese koji ih koriste.


#### M

`mail` - Prikazivanje, čitanje i slanje pošte drugim korisnicima sistema.

`make` - Prevođenje i povezivanje izvornog koda na osnovu datoteke Makefile.

`man` - Prikazuje stranicu uputstva (man page) za određenu komandu.

`mesg` - Komanda kojom korisnik dozvoljava ili zabranjuje drugim korisnicima da mu šalju poruke komandom `write`.

`mkdir` - Kreiranje direktorijuma. Sa opcijom `-p` kreira i roditeljske direktorijume ako ne postoje.

`mkfs` - Administrativna komanda, front-end za alate kojima se kreiraju sistemi datoteka (mkfs.ext4, mkfs.xfs, itd.).

`mkfifo` - Kreiranje imenovanih FIFO datoteka (imenovani pipe).

`mknod` - Kreiranje specijalnih datoteka (nodova), odnosno datoteka koje mogu da šalju i primaju podatke (karakter i blok uređaji).

`mkswap` - Administrativna komanda za kreiranje logičke strukture swap datoteke ili particije.

`modinfo` - Štampa na standardnom izlazu informacije o određenom modulu kernela. Informacije se čitaju iz zaglavlja datoteke u kojoj se taj modul nalazi.

`modprobe` - Administrativna komanda za učitavanje i uklanjanje modula kernela, uz automatsko rješavanje zavisnosti.

`more` - Komanda za pregledanje sadržaja tekstualnih datoteka (stranica po stranica).

`mount` - Administrativna komanda za aktiviranje sistema datoteka (montiranje na mount-point direktorijume). Svi korisnici pomoću ove komande mogu utvrditi koji su sistemi datoteka trenutno aktivirani.

`mv` - Pomjeranje datoteke, grupe datoteka ili direktorijuma sa jedne lokacije na drugu. Također se koristi za preimenovanje datoteka.


#### N

`named` - Server imena (DNS). Poznat i kao BIND.

`netstat` - TCP/IP dijagnostički alat koji daje izvještaje o mrežnom interfejsu, tabelama rutiranja, mrežnim konekcijama i statistici korištenja TCP/IP skupa protokola. **(zastarjelo)** Na modernim sistemima koristite `ss`.

`nft` - Komanda za konfigurisanje nftables firewalla. Moderna zamjena za `iptables`.

`nice` - Izvršavanje komande sa izmijenjenim prioritetom ("be nice to other users"). Podrazumijevano snižava prioritet.

`nohup` - Pokreće program čije se izvršenje nastavlja nakon odjavljivanja korisnika sa sistema.

`nslookup` - Komanda za ispitivanje DNS servera. Na modernim sistemima preporučuje se `dig` ili `host`.


#### P

`passwd` - Promjena lozinke korisnika.

`ping` - TCP/IP dijagnostički alat za slanje ICMP ECHO paketa. Ovim alatom se može utvrditi da li je udaljeni računar dostupan.

`pppd` - PPP (Point-to-Point Protocol) daemon za uspostavljanje mrežnih konekcija putem serijskih linija.

`pr` - Priprema tekstualnih datoteka za štampanje (podjela datoteke na stranice, numerisanje stranica i navođenje datuma i imena datoteke u zaglavlju).

`ps` - Štampa izvještaj o procesima na standardnom izlazu.

`pwck` - Provjera integriteta passwd datoteke.

`pwd` - Štampa na standardnom izlazu putanju tekućeg direktorijuma.


#### Q

`quota` - Prikazuje zauzeće diska od strane određenog korisnika ili grupe i ograničenja u sistemu datoteka.

`quotacheck` - Na osnovu analize potrošnje prostora na odgovarajućem sistemu datoteka kreira odgovarajuće datoteke quota.user i quota.group.

`quotaon` - Aktiviranje kvote.

`quotaoff` - Deaktiviranje kvote.

`repquota` - Prikazuje informacije o zauzeću diska i kvotama za navedeni sistem datoteka.


#### R

`readlink` - Prikazuje sadržaj simboličkog linka, odnosno putanju i ime objekta na koji link pokazuje. Sa opcijom `-f` razrješava sve simboličke linkove u putanji.

`reboot` - Administrativna komanda za zaustavljanje i ponovno podizanje sistema. Ukoliko sistem nije u nivou izvršenja 0 ili 6, reboot poziva komandu `shutdown -r`.

`rename` - Promjena imena većeg broja datoteka (jedan niz karaktera u imenima se mijenja drugim).

`renice` - Promjena prioriteta pokrenutog procesa.

`resize2fs` - Administrativna komanda za promjenu veličine ext2/ext3/ext4 sistema datoteka. Može povećati sistem datoteka online (bez demontiranja) ili ga smanjiti nakon demontiranja.

`rev` - Štampa datoteku na standardnom izlazu, pri čemu svaku liniju datoteke štampa unazad.

`rm` - Brisanje datoteke, grupe datoteka i dijelova direktorijumskog stabla.

`rmdir` - Brisanje praznih direktorijuma.

`rmmod` - Uklanjanje modula iz tekućeg jezgra.

`route` - TCP/IP komanda za izmjenu sadržaja tabele rutiranja. **(zastarjelo)** Na modernim sistemima koristite `ip route`.

`rpm` - Red Hat Package Manager - rad sa RPM paketima.

`rsync` - Brza i fleksibilna komanda za sinhronizaciju datoteka i direktorijuma lokalno ili između udaljenih sistema. Prenosi samo razlike između izvora i odredišta.

`runlevel` - Prikazuje nivo izvršavanja.


#### S

`scp` - Sigurno kopiranje datoteka između udaljenih računara putem SSH protokola.

`sed` - Stream editor - modifikacija sadržaja datoteka bez interakcije korisnika.

`sftp` - Siguran transfer datoteka između udaljenih računara putem SSH protokola. Zamjena za `ftp`.

`shred` - Prepisuje slučajni sadržaj preko datoteke, nakon čega briše datoteku. Time se obezbjeđuje da se datoteka ne može povratiti.

`shutdown` - Administrativna komanda za zaustavljanje sistema na kontrolisan način.

`sort` - Uređivanje sadržaja datoteka.

`split` - Dijeljenje datoteka na segmente jednake veličine.

`ss` - Moderna komanda za prikaz informacija o mrežnim soketima. Zamjena za `netstat`.

`ssh` - Secure Shell - sigurno prijavljivanje na udaljeni sistem (podaci na liniji se šifruju).

`sshd` - Secure Shell server (daemon).

`strings` - Prikazuje vidljive (printable) karaktere u izvršnoj ili binarnoj datoteci.

`stty` - Podešavanje karakteristika terminala.

`su` - Privremeno prijavljivanje na sistem sa drugim korisničkim nalogom.

`sudo` - Izvršavanje komandi sa root privilegijama (ili privilegijama drugog korisnika).

`swapon` - Administrativna komanda za uključivanje swap prostora.

`swapoff` - Administrativna komanda za isključivanje swap prostora.

`sync` - Administrativna komanda koja upisuje sadržaj keša na disk i prazni keš.

`systemctl` - Komanda za upravljanje systemd servisima i sistemom. Koristi se za pokretanje, zaustavljanje, restartovanje servisa, te pregled statusa.


#### T

`tac` - Štampa sadržaj datoteke na standardnom izlazu počev od posljednje linije ka prvoj (obrnuti `cat`).

`tail` - Prikazuje kraj datoteke (podrazumijevano posljednjih 10 linija). Sa opcijom `-f` kontinuirano prati nove linije.

`tar` - Tape Archiver - arhiviranje i dearhiviranje datoteka.

`tcpdump` - Alat za snimanje i analizu mrežnog saobraćaja na mrežnom interfejsu.

`tee` - Podatke sa standardnog ulaza upisuje u datoteku i šalje ih na standardni izlaz.

`telnet` - Prijavljivanje na udaljeni sistem. **(zastarjelo)** Komunikaciona linija se ne šifruje. Koristite `ssh`.

`time` - Izvršava komandu i određuje vrijeme potrebno za izvršenje te komande.

`top` - Obezbjeđuje informacije o procesima u realnom vremenu, uključujući potrošnju CPU i memorije.

`touch` - Postavlja vrijeme zadnjeg pristupa i vrijeme posljednje modifikacije na tekuće vrijeme. Ukoliko datoteka ne postoji, kreiraće praznu datoteku.

`traceroute` - Identifikacija rute (niz rutera) do odredišnog računara.

`tty` - Prikazuje ime uređaja koji se koristi kao standardni ulaz.

`tune2fs` - Administrativna komanda za podešavanje parametara ext2/ext3/ext4 sistema datoteka.


#### U

`umount` - Administrativna komanda za deaktiviranje (demontiranje) sistema datoteka.

`uname` - Prikazuje ime računara, arhitekturu hardvera, verziju kernela i ime operativnog sistema.

`uniq` - Uklanja sve duplikate uzastopnih identičnih linija iz tekstualne datoteke.

`uptime` - Prikazuje vrijeme proteklo od posljednjeg podizanja sistema, broj trenutno prijavljenih korisnika i prosječno opterećenje sistema.

`useradd` - Administrativna komanda za kreiranje korisničkih naloga.

`userdel` - Administrativna komanda za brisanje korisničkih naloga.

`usermod` - Modifikacija parametara korisničkog naloga.


#### V

`vdir` - Ekvivalentna komandi `ls -lb`.

`vi` - Vi tekst editor, prisutan na svim UNIX sistemima.

`vim` - Vi Improved, poboljšana verzija vi editora.

`vmstat` - Prikazuje statistički izvještaj o memoriji, swap prostoru, iskorištenosti procesora i procesima.


#### W

`w` - Prikazuje koji su korisnici prijavljeni na sistem i šta trenutno rade.

`wall` - Slanje poruke svim korisnicima ("Broadcast Message from...").

`watch` - Izvršava zadatu komandu repetitivno (podrazumijevano svake 2 sekunde) tako da korisnik može da prati izlaz komande.

`wc` - Brojanje karaktera, riječi i linija u datoteci.

`wget` - Alat za neinteraktivno preuzimanje datoteka sa weba. Podržava HTTP, HTTPS i FTP protokole.

`whatis` - Na standardnom izlazu prikazuje kratak opis navedene komande.

`whereis` - Prikazuje lokaciju izvršnih datoteka, izvornog koda i prateće dokumentacije programa.

`which` - Prikazuje lokaciju izvršne datoteke u PATH-u.

`who` - Prikazuje koji su korisnici prijavljeni na sistem.

`whoami` - Prikazuje korisničko ime korisnika koji je komandu zadao.


#### X

`xargs` - Čita stavke sa standardnog ulaza i izvršava komandu sa tim stavkama kao argumentima. Koristan u kombinaciji sa `find` i drugim komandama.

`xinetd` - TCP/IP wrapper (extended Internet services daemon). Na nekim sistemima se koristi umjesto `inetd` wrappera. **(zastarjelo)** Zamijenjeno sa systemd socket aktivacijom.


#### Z

`zcat` - Komanda `cat` za .Z i .gz datoteke (prikazuje sadržaj bez dekompresije na disk).

`zmore` - Komanda `more` za .Z i .gz datoteke.

`zstd` - Moderna komanda za kompresiju i dekompresiju koristeći Zstandard algoritam. Nudi bolji omjer brzine i kompresije od gzip-a.
