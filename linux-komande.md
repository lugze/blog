---
layout: page
title: Linux komande
permalink: /linux-komande/
---


#### A

```adduser``` - Kreiranje korisnickih naloga.

```anacron``` - Administrativna komanda koja se normalno pokrece pri podizanju sistema
i periodino izvršava komande. Lista poslova se podrazumjevano cita iz
datoteke /etc/anacrontab.

```apropos``` - Na standardnom izlazu prikazuje ime i opis svih komandi koje u opisu
imaju zadati string.

```apt-get``` - Debian Package Management System - alat za rad sa paketima iz
komandne linije. Front-end za APT.

```aptitude``` - Debian Package Management System - alat za interaktivni rad sa
paketima. Front-end sa sistemom tekstualnih menija za APT.

```arch``` - Prikazuje arhitekturu racunara na standardnom izlazu (kao uname -m).

```arp``` - TCP/IP administrativna komanda za rad sa ARP kešom kernela. ARP se
koristi za prevodjenje IP adresa u MAC adrese mrežnih adaptera.

```at``` - Komanda kojom se zakazuje izvršenje drugih komandi u odredjeno vrijeme.

```atd``` - Daemon koji izvršava komande zakazane komandom at. Normalno se
pokrece prilikom podizanja sistema.

```atq``` - Prikazuje zakazane at poslove korisnika. U slucaju da komandu zada
superuser, prikazuju se svi zakazani poslovi.

```atrm``` - Brisanje zakazanih at poslova


#### B

```badblocks``` - Administrativna komanda za analizu površine diskova

```banner``` - Na standardnom izlazu prikazuje string kao "poster".

```basename``` - Prikazuje ime direktorijuma bez vodece apsolutne putanje (na primer:
basename $PWD). Komanda je korisna za shell programiranje.

```bash``` - Bash komandni interpreter (Bourne-Again Shell).

```bashburn``` - Front-end za cdrecord (snimanje CD-ROM medijuma).

```batch``` - Slino komandi at, izvršava komande date na standardnom ulazu. Ukoliko
se vreme izvršenja ne navede, komande se izvršavaju kada optereenje
sistema dostigne dovoljno nizak nivo (80%).

```bc``` - Interaktivni kalkulator koji ulazne podatke prima sa standardnog ulaza ili
iz datoteke.

```biod``` - NFS server.

```bzip2``` - Paket za kompresiju slian programu gzip koji koristi drugacije algoritme i
postiže vei stepen kompresije. Paket ukljuuje programe za kompresiju i
dekompresiju (bzip2, bunzip2), pregledanje sadržaja (bzcat, bzless,
bzmore) i oporavak (bzip2recover).


#### C

```cal``` - Prikazuje kalendar za tekuci mjesec. Takodje može prikazati godišnji ili
mesecni kalendar za godinu i mjesec koji se navode kao parametri.

```cancel``` - Uklanjanje poslova iz reda za štampu (System V).

```cat``` - Konkatenacija datoteka i prikazivanje na standardnom izlazu.

```cdrecord``` - Program za snimanje kompakt diskova sa velikim brojem opcija.

```cfdisk``` - Administrativni program sa sistemom menija za particionisanja diska

```chgrp``` - Promena grupe kojoj objekat sistema datoteka pripada. U opštem slucaju
ovu komandu može da izvrši root, a na nekim sistemima može i vlasnik
objekta.

```chmod``` - Promjena pristupnih prava objekta sistema datoteka. Ovu komandu mogu
da izvrše root i vlasnik objekta.

```chown``` - Promjena vlasnika objekta sistema datoteka. U opštem sluaju ovu
komandu može da izvrši root, a na nekim sistemima može i vlasnik
objekta.

```chpasswd``` - Administrativna komanda za promenu lozinke.

```chsh``` - Promena komandnog interpretera koji se pokree nakon login procesa. Ime
komandnog interpretera se navodi sa apsolutnom putanjom.

```chvt``` - Prelazak na virtuelni terminal N. Ukoliko terminal ne postoji bie
napravljen. Ekvivalentno kombinaciji tastera <Ctrl-Alt-N>, gde je N broj
terminala.

```cksum``` -  Run-anje CRC ek-sume za datoteku.

```clear``` - Brisanje ekrana.

```cmp``` - Uporedjivanje datoteka i prikazivanje prve razlike na standardnom izlazu.

```compress``` - Program za kompresiju datoteka. Gzip i bzip2 se danas koriste umesto
ovog programa.

```cp``` - Kopiranje datoteke, grupe datoteka ili delova direktorijumskog stabla.
Takodje se može koristiti za kreiranje linkova.

```cpio``` -  Arhiviranje i dearhiviranje datoteka (copy-out i copy-in). Takoe se može
koristiti za kopiranje datoteka u aktivnom UNIX stablu (copy-pass).

```cron``` - Administrativna komanda koja se normalno pokree pri podizanju sistema
i periodino izvršava komande. Cron proverava korisnike crontab
datoteke (nalaze se u direktorijumu /var/spool/cron/crontabs a imenovane
su na osnovu korisnikih naloga) svaki minuta i po i pokree programe
koje tada treba izvršiti.

```crontab``` -  Zakazivanje periodinog izvršenja komandi, odnosno izvršenja u
specificiranim intervalima. Zavisno od konkretnog UNIX sistema
izvrsenje mogu zakazati svi ili samo privilegovani korisnici.


#### D


```date``` - Prikazuje trenutni datum i vreme.

```dd``` - Konvertuje i kopira datoteku ili odreeni deo medijuma. Prilikom pristupa
medijumu može zaobici sistem datoteka, ime je omoguceno kopiranje
medijuma koji nisu ni u jednom od formata koje UNIX prepoznaje.

```debugfs``` - Administrativna komanda kojom se ostvaruje pristup zaglavlju i meta-data
strukturama ext2 sistema datoteka.

```depmod``` - Kreira datoteku u kojoj je opisana medjusobna zavisnost programskih
modula.

```df``` - Prikazuje iskorišenost aktiviranih sistema datoteka.

```diff``` - Uporedjuje datoteke i prikazuje sve razlike na standardnom izlazu.

```dig``` - Komanda za slanje upita DNS serverima, fleksibilnija od nslookup
komande.

```dpkg``` - Debian Package Management System - rad sa paketima iz komandne
linije.

```dselect``` - Debian Package Management System - okruženje sa menijima.

```du``` - Prikazuje kolicinu prostora na sistemu datoteka koju zauzimaju datoteke u
poddirektorijumima tekuceg direktorijuma.

```dumpe2fs``` - Administrativna komanda koja na standardnom izlazu prikazuje
infomacije iz superbloka sistema datoteka

#### E

```e2fsck``` - Administrativna komanda za provjeru integriteta ext2 i ext3 sistema
datoteka.

```e2image``` - Administrativna komanda za kreiranje slike (image) znaajnijih delova
sistema datoteka (kao što je superblok) na izmenljivom medijumu
(disketi).

```e2label``` - Administrativna komanda za prikazivanje i promenu imena sistema
datoteka.

```echo``` - Prikazuje niz karaktera ili vrednost promenljive na standardnom izlazu.

```edquota``` - Editor kvota.

```egrep``` - Traži regularne izraze u datoteci.

```emacs``` - Emacs tekst editor.

```env``` - Prikazuje vrednosti promenljivih koje ine okruženje.

```expr``` - Obavlja jednostavne aritmetike operacije.

#### F

```fdformat``` - Formatiranje disketa niskog nivoa.

```fdisk``` - Administrativni program za particionisanje hard diskova.

```fgconsole``` - Prikazuje broj trenutno aktivne virtuelne konzole (na primer 2, ukoliko
korisnik radi na /dev/tty2).

```fgrep``` - Traži niz karaktera u datoteci.

```find``` - Traži datoteku na osnovu zadatih kriterijuma u aktivnom UNIX stablu.

```finger``` - Prikazuje informacije o korisnicima, ukljuujui i informacije iz datoteka
.plan i .project u home direktorijumu korisnika.

```fingerd``` - Server za informacije o korisnicima.

```free``` - Prikazuje informacije o iskorišenosti operativne memorije i swap
prostora.

```fsck``` - Administrativna komanda za proveru integriteta sistema datoteka.

```ftp``` - Interaktivni program za transfer datoteka izmeu dva udaljena sistema.

```ftpd``` - FTP server.

#### G

```gpm``` - Server za miša koji obezbeuje cut-and-paste funkcionalnost na Linux
konzoli.

```grep``` - Traži osnovne regularne izraze u datoteci.

```groupadd``` - Administrativna komanda za kreiranje nove korisnike grupe.

```groupdel``` - Administrativna komanda za brisanje postojee korisnike grupe

```groupmod``` - Administrativna komanda za modifikovanje parametara grupe.

```groups``` - Prikazuje grupe kojima navedeni korisnik pripada.

```grpck``` - Administrativna komanda koja uklanja duplikate iz datoteke /etc/group.

```grpconv``` - Administrativna komanda za kreiranje /etc/gshadow datoteke, u koju se
smeštaju sve grupne lozinke.

```grpunconv``` - Administrativna komanda kojom se uklanja /etc/gshadow datoteka.

```gunzip``` - Dekompresija .gz datoteka.

```gzexe``` - Kreiranje samoraspakujue izvršne gzip datoteke. Nakon pokretanja takva
datoteka e se sama dekompresovati. Ovde se štedi na prostoru, ali gubi na
vremenu potrebnom za izvršavanje datoteke.

```gzip``` - Kompesija datoteka u .gz format.


#### H

```halt``` - Administrativna komanda za zaustavljanje sistema. Ukoliko se sistem
nalazi u nivoima izvršenja 0 ili 6 halt zaustavlja sve procese, a inace
poziva komandu shutdown -h.

```hdparm``` - Administrativna komanda za pregledanje i postavljanje parametara hard
diskova. Koristi se uglavnom na IDE diskovima.

```head``` - Prikazuje pocetak datoteke.

```hexdump``` - Prikazuje datoteku u heksadecimalnom ili oktalnom formatu.

```host``` - Prikazuje informacije o racunarima i zonama u DNS domenu.

```hostname``` - Prikazuje ime raunara, pri cemu privilegovani korisnik može dodeliti
novo ime racunaru.

```hwclock``` - Administrativna komanda kojom privilegovani korisnik može podesiti
hardverski sat sistema.


#### I

```id``` - Prikazivanje informacija o korisnicima, ukljucujuci i clanstvo u grupama.

```ifconfig``` - TCP/IP administrativna komanda za konfigurisanje mrežnih interfejsa
rezidentnih u kernelu. Komandom ifconfig mogu se postaviti parametri
poput IP adrese, maske podmreže i broadcast adrese. Komanda ifconfig se
koristi prilikom podizanja sistema radi postavljanja parametara mrežnog
interfejsa. Nakon toga naješe se koristi u dijagnostike svrhe - komanda
prikazuje trenutnu konfiguraciju mrežnog interfejsa i MAC adresu mrežne
kartice.

```inetd``` - TCP/IP administrativna komanda kojom se može zaustaviti ili pokrenuti
inetd wrapper.

```init``` - Osnovni proces i administrativna komanda za inicijalizaciju sistema
(forsira se novo itanje konfiguracione datoteke /etc/inittab) i promenu
nivoa izvršenja.

```ipchains``` - Administrativna komanda za konfigurisanje firewalla u Linux kernelu 2.2

```iptables``` - Administrativna komanda za konfigurisanje firewalla u Linux kernelu 2.4

#### K

```kernelversion``` - Prikazuje verziju tekueg kernela.

```kill``` - Šalje signale procesu sa poznatim PID

```killall``` - Ubija procese nastale pokretanjem odreenog programa (kao argument se
navodi ime programa).

#### L

```last``` - Prikazuje nekoliko poslednjih login procedura, odnosno imena korisnika,
terminal, ime udaljenog raunara i vreme prijavljivanja na sistem.

```lastb``` - Prikazuje nekoliko poslednjih neuspešnih login procedura, u istom
formatu kao i last.

```lastlog``` - Prikazuje sve korisnike sistema i vreme kada su se zadnji put prijavili na
sistem.

```less``` - Interaktivni program za pregledanje sadržaja tekstualnih datoteka.

```ln``` - Kreiranje hard i simbolikih linkova.

```locale``` - Štampa izveštaj o regionalnim podešavanjima na standardnom izlazu.

```lockfile``` - Kreira specijalne semafor datoteke koje se koriste za ograniavanje
pristupa datotekama.

```login``` - Prijavljivanje na sistem. Trei proces u nizu init-getty-login-shell.

```logname``` - Prikazuje ime korisnika koji je prijavljen na sistem na osnovu podataka u
datoteci /var/run/utmp.

```look``` - Prikazuje rei iz datoteke /usr/dict/words koje poinju zadatim nizom
karaktera.

```lp``` - Štampanje iz komandne linije (System V).

```lpadmin``` - Administracija CUPS servisa za štampu.

```lpc``` - Administrativna komanda za kontrolu LPRng servisa za štampu.

```lpd``` - LPRng line printer daemon (servis za štampu).

```lpinfo``` - Informacije o štampaima (CUPS).

```lpq``` - Ispitivanje reda za štampu (BSD).

```lpr``` - Štampanje iz komandne linije (BSD).

```lprm``` - Uklanjanje poslova iz reda za štampu (BSD).

```lpstat``` - Ispitivanje reda za štampu (System V).

```ls``` - Prikazuje sadržaj direktorijuma na standardnom izlazu.

```lsattr``` - Prikazuje specijalne atribute datoteka karakteristine za ext2 i ext3
sisteme datoteka.

```lsmod``` - Prikazuje module uitane u tekue jezgro.



#### M

```mail``` - Prikazivanje, itanje i slanje pošte drugim korisnicima sistema.

```make``` - Prevoenje i povezivanje izvornog koda na osnovu datoteke makefile.

```man``` - Prikazuje stranicu uputstva (man page) za odreenu komandu.

```mtools``` - Alati za rad sa MS-DOS diskovima. Koriste DOS sintaksu, odnosno
korisnici se diskovima obraaju preko labela, a ne preko nodova.

```mesg``` Komanda kojom korisnik dozvoljava ili zabranjuje drugim korisnicima da
mu šalju poruke komandom write.

```mkdir``` - Kreiranje direktorijuma u aktivnom UNIX stablu.

```mkfs``` - Administrativna komanda, front-end za alate kojima se kreiraju sistemi
datoteka.

```mkfs.ext2``` - Administrativna komanda za kreiranje ext2 sistema datoteka (mke2fs).

```mkfs.ext3``` - Administrativna komanda za kreiranje ext3 sistema datoteka.

```mkfs.msdos``` - Administrativna komanda za kreiranje MS-DOS sistema datote
ka.

```mkfifo``` - Kreiranje imenovanih FIFO datoteka (imenovani pipe).

```mkisofs``` - Kreiranje ISO9660/Joliet/HFS (Macintosh Hierarchical File System)
sistema datoteka radi snimanja CD-ROM medijuma alatom cdrecord.

```mklost+found``` - Kreiranje lost+found direktorijuma na ext2 sistemima datoteka.

```mknod``` - Kreiranje specijalnih datoteka (nodova), odnosno datoteka koje mogu da
šalju i primaju podatke (karakter i blok ureaji).

```mkraid``` - Administrativna komanda za kreiranje novog RAID niza diskova
definisanog konfiguracionom datotekom /etc/raidtab. Inicijalizacija
uništava sve podatke na diskovima koji ine RAID niz.

```mkswap``` - Administrativna komanda za kreiranje logike strukture swap datoteke ili
particije.

```modinfo``` - Štampa na standardnom izlazu informacije o odreenom modulu kernela.
Informacije se itaju iz zaglavlja datoteke u kojoj se taj modul nalazi.

```modprobe``` - Administrativna komanda za rad sa modulima kernela. Uz komandu
depmod omoguava lakši rad sa modulima.

```more``` - Komanda za pregledanje sadržaja tekstualnih datoteka.

```mount``` - Administrativna komanda za aktiviranje sistema datoteka (montiranje na
mount-point direktorijume). Svi korisnici pomou ove komande mogu
utvrditi koji su sistemi datoteka trenutno aktivirani.

```mountd``` - NFS/NIS administrativna komanda. Server koji upravlja zahtjevima za
montiranje NFS sistema datoteka.

```mt``` - Administrativna komanda za upravljanje magnetnim trakama.

```mv``` - Pomeranje datoteke, grupe datoteka ili direktorijuma sa jedne lokacije na
drugu. Promjena imena datoteka.

#### N

```named``` - Server imena (DNS).

```nameif``` - Administrativna komanda za dodelu imena interfejsa sa zadatom MAC
adresom.

```netstat``` - TCP/IP dijagnostiki alat koji daje izveštaje o mrežnom interfejsu,
tabelama rutiranja, mrežnim konekcijama i statistici korišenja TCP/IP
skupa protokola.

```newusers``` - Administrativna komanda za kreiranje korisnikih naloga na osnovu
sadržaja datoteke koja se navodi kao parametar (u datoteci se navode
korisnika imena i lozinke). Prilikom kreiranja korisnikih naloga, kreiraju
se i grupe i home direktorijumi, ukoliko ve ne postoje.

```nfsd``` - NFS klijent.

```nfsstat``` - NFS dijagnostiki alat koji štampa statistiki izveštaj o korišenju NFS-a.

```nice``` - Izvršavanje komande sa nižim prioritetom ("be nice to other users").

```nohup``` - Pokrece program (komanda se zadaje kao argument) cije se izvršenje
nastavlja nakon odjavljivanja korisnika sa sistema.

```nslookup``` - Komanda za ispitivanje DNS servera.

```nsupdate``` - Administrativna komanda za podnošenje zahteva za dinamicko ažuriranje
servera imena.

#### P

```passwd``` - Promjena lozinke korisnika.

```ping``` - TCP/IP dijagnosticki alat za slanje ICMP ECHO paketa. Ovim alatom se
može utvrditi da li je udaljeni racunar dostupan.

pppd PPP (Point-to-Point Protocol) server.

```pr``` - Priprema tekstualnih datoteka za štampanje (podjela datoteke na stranice,
numerisanje stranica i navodjenje datuma i imena datoteke u zaglavlju).

```ps``` - Štampa izveštaj o procesima na standardnom izlazu.

```pwck``` - Provjera integriteta passwd datoteke.

```pwconv``` - Administrativni alat za kreiranje datoteke /etc/shadow. Originalne lozinke
u datoteci /etc/passwd zamenjuju se znakom x.

```pwunconv``` - Administrativni alat za uklanjanje datoteke /etc/shadow.

```pwd``` Štampa na standardnom izlazu putanju tekuceg direktorijuma.

#### Q

```quota``` - Prikazuje zauzee diska od strane odredjenog korisnika ili grupe i
ogranicenja u sistemu datoteka.

```repquota``` - Prikazuje informacije o zauzecu diska i kvotama za navedeni sistem
datoteka, trenutnom broju datoteka i zauzecu diska za svakog korisnika
kome su dodeljene kvote.

```quotacheck``` - Na osnovu analize potrošnje prostora na odgovarajuem sistemu datoteka
kreira odgovarajue datoteke quota.user i quota.group.

```quotaon``` - Aktiviranje kvote.

```quotaoff``` - Deaktiviranje kvote.

#### R

```rcp``` - Kopiranje datoteka izmedju udaljenih racunara.

```readlink``` - Prikazuje sadržaj simbolikog linka, odnosno putanju i ime objekta na koji
link pokazuje.

```reboot``` - Administrativna komanda za zaustavljanje i ponovno podizanje sistema
koja odmah ubija sve procese. Ukoliko sistem nije u nivou izvršenja 0 ili
6, reboot poziva komandu shutdown -r.

```rename``` - Promjena imena veceg broja datoteka (jedan niz karaktera u imenima se
mijenja drugim).

```renice``` - Promjena prioriteta procesa.

```resize2fs``` - Administrativna komanda za promenu veliine sistema datoteka. Komanda
zahtjeva da se najpre programom fdisk obriše particija u kojoj se nalazi
sistem datoteka, a zatim kreira nova (vea) pocev od istog cilindra.

```rev``` - Štampa datoteku na standardnom izlazu, pri cemu svaku liniju datoteke
štampa unazad.

```rm``` - Brisanje datoteke, grupe datoteka i delova direktorijumskog stabla.

```rmdir``` - Brisanje praznih direkorijuma.

```rmmod``` - Uklanjanje modula iz tekuceg jezgra.

```route``` - TCP/IP command za izmjenu sadržaja tabele rutiranja (tabele rutiranja
održava routed).

```routed``` - Mrežni ruter, podržava Routing Information Protocol.

```rpm``` - Red Hat Package Manager.

```runlevel``` - Prikazuje nivo izvršavanja.

```run-parts``` - Pokrece skriptove u direktorijumu po abecednom redu.

#### S

```sed``` - Stream editor modifikacija sadržaja datoteka bez interakcije korisnika.

```setfdprm``` - Konfigurisanje parametara flopi diskova.

```sftp``` Siguran transfer datoteka izmedju udaljenih racunara putem ssh.

```showmount``` - NFS/NIS koja prikazuje informacije o NFS serveru.

```shred``` - Prepisuje slucajni sadržaj preko datoteke, nakon cega briše datoteku. Time
se obezbjedjuje da se datoteka ne može povratiti.

```shutdown``` - Administrativna komanda za zaustavljanje sistema.

```sort``` - Uredjivanje sadržaja datoteka.

```split``` - Dijeljenje datoteka na segmente jednake velicine.

```ssh``` - Secure Shell - sigurno prijavljivanje na udaljeni sistem (podaci na liniji se
šifruju).

```sshd``` - Secure Shell server.

```strings``` - Prikazuje vidljive karaktere u izvršnoj ili binarnoj datoteci.

```stty``` - Podešavanje karakteristika terminala.

```su``` - Privremeno prijavljivanje na sistem sa drugim korisnickim nalogom.

```sudo``` - Izvršavanje komandi sa root privilegijama.

```sum``` - Racuna i prikazuje cek-sumu i velicinu datoteka. Komanda je korisna za
verifikaciju transfera datoteka.

```swapoff``` - Administrativna komanda za iskljucivanje swap prostora.

```swapon``` - Administrativna komanda za ukljucivanje swap prostora.

```sync``` - Administrativna komanda koja upisuje sadržaj keša na disk i prazni keš.

```sysklogd``` - Daemon koji poruke operativnog sistema upisuje u odgovarajue log
datoteke.

#### T

```tac``` - Štampa sadržaj datoteke na standardnom izlazu pocev od posljednje linije
ka prvoj.

```tail``` - Prikazuje kraj datoteke (nekoliko poslednjih linija).

```tar``` -  Tape Archiver - arhiviranje i dearhiviranje datoteka.

```tcpd``` -  TCP/IP wrapper.

```tcsh``` - Poboljšana verzija C shell komandnog interpretera.

```tee``` - Podatke sa standardnog ulaza upisuje u datoteku i šalje ih na standardni izlaz.

```telnet``` - Prijavljivanje na udaljeni sistem. Za razliku od ssh, komunikaciona linija
se ne šifruje, tako da nije sigurna.

```telnetd``` - Telnet server.

```time``` - Izvršava komandu i odreuje vreme potrebno za izvršenje te komande.

```tload``` - Prikazuje grafik opterecenja sistema.

```top``` - Obezbjedjuje informacije o procesima koji su kriticni po pitanju potrošnje
procesorskog vremena (top processes).

```touch``` - Postavlja vrijeme zadnjeg pristupa i vrijeme posljednje modifikacija na tekuce vrijeme. Ukoliko datoteka ne postoji, kreirat ce praznu datoteku.

```traceroute``` - Identifikacija rute do odredišnog run-era

```tty``` - Prikazuje ime uredjaja koji se koristi kao standardni ulaz.

```tune2fs``` - Administrativna komanda za podešavanje parametara ext2 sistema
datoteka.

```tunelp``` - Administrativna komanda za podešavanje parametara štampaca.

#### U

```umount``` - Administrativna komanda za deaktiviranje sistema datoteka.

```uname``` - Prikazuje ime racunara, arhitekturu hardvera i ime operativnog sistema.

```uncompress``` - Dekompresija .Z datoteka.

```uniq``` - Uklanja sve duplikate linija iz tekstualne datoteke (izbacuje sve
konsekventne identine linije, osim prve u nizu).

```uptime``` - Prikazuje vreme proteklo od posljednjeg podizanja sistema, broj trenutno
prijavljenih korisnika i prosjecno opterecenje sistema.

```useradd``` - Administrativna komanda za kreiranje korisnikih naloga.

```userdel``` - Administrativna komanda za brisanje korisnikih naloga.

```usermod``` - Modifikacija parametara korisnikog naloga.

#### V

```vdir``` Ekvivalentna komandi ls -lb.

```vi``` - Vi tekst editor, prisutan na svim UNIX sistemima.

```vim``` - Vi Improved, poboljšana verzija vi editora.

```vmstat``` - Prikazuje statisticki izveštaj o memoriji, swap prostoru, iskorišenosti
procesora i procesima.

#### W

```w``` - Prikazuje koji su korisnici prijavljeni na sistem i "šta trenutno rade".

```wall``` - Slanje poruke svim korisnicima ("Broadcast Message from...").

```watch``` - Izvršava zadatu komandu repetativno (podrazumevano na svake dvije
sekunde) tako da korisnik može da prati izlaz komande.

```wc``` - Brojanje karaktera, rijeci i linija u datoteci.

```whatis``` - Na standardnom izlazu prikazuje opis navedene komande.

```whereis``` - Prikazuje lokaciju izvršnih datoteka, izvornog koda i pratece
dokumentacije programa.

```which``` - Prikazuje lokaciju izvršne datoteke.

```who``` - Prikazuje koji su korisnici prijavljeni na sistem.

```whoami``` - Prikazuje korisnicko ime korisnika koji je komandu zadao.

```write``` - Slanje poruka odredjenom korisniku.

#### X

```xinetd``` TCP/IP wrapper (extended Internet services daemon). Na nekim sistemima
se koristi umjesto inetd wrappera.

#### Y

```ypbind``` - NFS/NIS komanda. Proces kojim se klijentu dodeljuje NIS server.

```ypcat``` - NFS/NIS komanda za prikazivanje informacija u NIS bazi.

```ypchfn``` - NFS/NIS komanda za promjenu informacija u datoteci /etc/passwd.

```ypinit``` - NFS/NIS komanda za kreiranje NIS baze na NIS serveru.

```yppasswd``` - NFS/NIS komanda za promenu lozinke za prijavljivanje na NIS domen.

```yppasswdd``` - Rješava zahtjeve za promjenu lozinke korisnika sa udaljenih racunara.

```yppoll``` - Zahtev slave servera za ažuriranje baze sa master serverom.

```yppush``` - Prosljedjuje tabele sa master servera na slave servere.

```ypserv``` - NIS server.

```yptest``` - NFS/NIS komanda za provjeru konfiguracije NIS servisa.

```ypwhich``` - NFS/NIS komanda koja prikazuje ime NIS servera koji opslužuje lokalni
racunar.

```ypxfr``` - Program koji vrši transfer tabela sa jednog servera na drugi.

```ypxfrd``` - Proces na master serveru koji upravlja prenošenjem ažuriranih podataka
na slave server.

```ypupdated``` - Proces na slave serveru koji upravlja prenošenjem ažuriranih podataka sa
master servera.

```ypset``` - Zahtev da sistem bude server procesu ypbin na klijent racunaru.

#### Z

```zcat``` - Komanda cat za .Z i .gz datoteke.

```zmore``` - Komanda more za .Z i .gz datoteke.

```znew``` - Dekomprimuje .Z kompresovanu datoteku, a zatim je kompresuje u .gz
format.
