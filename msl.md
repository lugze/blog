---
layout: page
title: Mala Škola Linux-a
permalink: /mala-skola-linuxa/
---

Verzija dokumenta 0.0.2

## Uobičajena organizacija foldera u Linuxu

* `/bin`  - programi koje koriste i administratori i korisnici
* `/dev`  - datoteke koje predstavljaju hardverske uređaje (mrežna, grafička)
* `/etc`  - konfiguracijske datoteke
* `/home` - direktoriji korisnika
* `/sbin` - sistemski programi
* `/tmp`  - privremene datoteke
* `/usr`  - korisnički programi, dokumentacija i biblioteke
* `/var`  - sistemski zapisi i druge datoteke

Više na [Filesystem Hierarchy Standard](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard).

## Upravljanje korisnicima i grupama

Korisnici imaju sopstveni `home` direktorij koji se nalazi u folderu `/home`. Izuzetak je `root` korisnik, čiji home direktorij se nalazi na lokaciji `/root`.

### Vježba: nekoliko načina kako pristupiti home folderu

Koristiti `cd` komandu bez argumenata:

```
cd
```

Kao argument `cd` komandi proslijediti tildu tj. `~`:

```
cd ~
```

Kao argument `cd` komandi proslijediti built-in shell varijablu `$HOME`:

```
cd $HOME
```

### Komanda `finger`

Komanda `finger` ispisuje informacije o korisniku. Kao argument komandi proslijedimo korisničko ime tj. `username` korisnika. U sljedećem primjeru `finger` će prikazati informacije o korisniku `root`.

```
finger root
```

Kao odgovor dobijamo sljedeće informacije:

```
Login: root                     Name: root
Directory: /root                Shell: /bin/bash
On since Sun Mar 11 19:22 (UTC) on pts/2 from 77.77.218.xx
   18 minutes 24 seconds idle
     (messages off)
On since Sun Mar 11 19:31 (UTC) on pts/3 from 77.77.218.xx (messages off)
New mail received Mon Mar  5 15:40 2018 (UTC)
     Unread since Tue Feb 27 19:15 2018 (UTC)
No Plan.
```

Ukoliko dobijete grešku `-bash: finger: command not found` potrebno je da instalirate komandu na sljedeći način:

```
apt-get update
apt-get install finger
```

### Komanda `id`

Ova komanda nam daje informacije o korisniku kao što su:

* `uid`    - broj korisnika
* `gid`    - group id tj. broj primarne grupe kojoj korisnik pripada
* `groups` - kompletna lista grupa kojoj korisnik pripada, tj. gid i naziv grupe

Kada komandi `id` argument ostavimo prazan, podrazumijeva se da želimo saznati informacije o trenutno logovanom korisniku, odnosno korisniku koji izvršava komandu. Primjer:

```
id
uid=0(root) gid=0(root) groups=0(root)
```

Kada kao argument komandi `id` proslijedimo `username` dobijemo info o tom korisniku:

```
id korisnik
uid=1001(korisnik) gid=1001(korisnik) groups=1001(korisnik),27(sudo)
```

Ako želimo saznati samo `uid` broj korisnika koristimo parametar `-u`:

```
id -u root
0
```

Ako želimo saznati broj primarne grupe nekog korisnika, koristimo parametar `-g`:

```
id -g korisnik
1001
```

Ako želimo saznati brojeve svih grupa kojoj pripada korisnik, koristimo parametar `-G`:

```
id -G korisnik
1001 27
```

## Rad sa fajlovima i direktorijima

File ili direktorij sa razmakom u imenu, npr. `Moj File`, piše se kao `Moj\ File`.

### Ispis sadržaja direktorija

`ls` - listanje sadržaja direktorija

`ls -a -l -h` - listaj sa svim detaljima: `-a` sve fajlove (i skrivene), `-l` long format, `-h` human-readable veličine

Ili skraćeno:

```
ls -alh
```

Ispiši listu fajlova i direktorija unutar trenutnog direktorija:

```
ls .
```

Ispiši listu fajlova i direktorija uključujući i skrivene fajlove (skriveni fajlovi su fajlovi čije ime počinje sa tačkom `.`):

```
ls -al .
```

Ispiši listu fajlova i direktorija unutar trenutnog direktorija, te sadržaj direktorija koji se nalaze u tekućem direktoriju:

```
ls -al *
```

Ispiši listu fajlova i direktorija unutar trenutnog direktorija na način da i direktorije tretiramo kao obične fajlove te ne ispisujemo njihov sadržaj:

```
ls -ald *
```

Ispiši samo skrivene fajlove i direktorije (koji počinju sa znakom `.`):

```
ls -ald .*
```

### Ispis inode broja fajla

```
ls -i ime_fajla
```

### Kreiranje simboličkih linkova

Prvo napravimo fajl:

```
touch fajl_jedan
```

Zapišemo nešto u fajl pomoću redirekcije:

```
echo "NEKI TESTNI SADRZAJ" > fajl_jedan
```

Provjerimo da li je zapisano u fajl:

```
cat fajl_jedan
```

Napravimo simbolički link na novi fajl:

```
ln -s fajl_jedan fajl_dva_koji_je_simbolicki_link_na_prvi_fajl
```

Ispišemo sadržaj drugog fajla koji je simbolički link:

```
cat fajl_dva_koji_je_simbolicki_link_na_prvi_fajl
```

Možemo primijetiti da je sadržaj oba fajla isti.

Provjerimo inode-ove oba fajla:

```
ls -i fajl_jedan
ls -i fajl_dva_koji_je_simbolicki_link_na_prvi_fajl
```

Možemo primijetiti da su inode brojevi različiti što znači da su to različiti fajlovi, te ako jedan izbrišemo to znači da drugi fajl neće biti izbrisan.

#### Vježba

Izbrisati prvi fajl. Da li je drugi fajl koji je simbolički link izbrisan? Da li možemo pomoću `cat` komande izlistati sadržaj drugog fajla?

### Hard linkovi

Kreirati fajl i dodati neki sadržaj:

```
touch fajl_prvi
echo "NEKI TESTNI SADRZAJ" > fajl_prvi
```

Napraviti hard link:

```
ln fajl_prvi fajl_drugi
```

Provjeriti inode brojeve za oba fajla:

```
ls -i fajl_prvi
6257560 fajl_prvi
```

Inode broj fajla je `6257560`.

```
ls -i fajl_drugi
6257560 fajl_drugi
```

Inode broj drugog fajla je također `6257560`.

Inode brojevi su isti što znači da se oba fajla linkaju na istu lokaciju na disku.

#### Vježba

Šta se desi ako izbrišemo drugi fajl, da li će prvi fajl biti izbrisan?

```
rm fajl_drugi
```

### Rekurzivno listanje sadržaja foldera

```
ls -R IME_FOLDERA/
```

Pregledamo cijelu strukturu foldera rekurzivno.

### Pomoć o komandama

```
ls --help
```

Prikazuje kratku pomoć o komandi.

```
man ls
```

Prikazuje detaljni manual za komandu. Navigacija: `f` (naprijed), `b` (nazad), `q` (izlaz).

---

### Navigacija kroz direktorije

Ulazak u folder:

```
cd IME_FOLDERA
```

Samo `cd` bez argumenata vraća na home folder.

Izlazak iz foldera (jedan nivo gore):

```
cd ..
```

Ulazak na udaljeni folder, dva nivoa iznad:

```
cd ../../NEKI_FOLDER
```

### Putanje do programa

Koristimo komande `whereis` i `which` da saznamo putanju gdje je instaliran program, odnosno gdje se nalazi binary traženog programa:

```
whereis nano
```

```
which nano
```

```
whereis bash
```

```
which rvm
```

### Vježba: praćenje pwd vrijednosti

Pratiti kako se mijenja `pwd` vrijednost nakon svake izmjene trenutnog direktorija:

```
cd ~
pwd
echo $PWD
```

```
cd $HOME
pwd
echo $PWD
```

### Kreiranje direktorija

`mkdir` - pravljenje foldera

```
mkdir folder/subfolder/subsubfolder
```

`mkdir -p` - pravljenje parent direktorija. Koristi se u slučaju da parent folder ne postoji te želimo u isto vrijeme napraviti parent folder i u njemu subfoldere:

```
mkdir -p folder/subfolder/subsubfolder
```

### Kreiranje, kopiranje i premještanje fajlova

Pravljenje fajla:

```
touch mojFile.txt
```

Kopiranje fajla:

```
cp mojFile.txt mojNoviFile.txt
```

Premještanje fajlova (može se koristiti i za preimenovanje):

```
mv novi_file.txt najbolji_folder
```

```
mv novi_file.txt najbolji_folder/novi_file2
```

Pomjeri sve `.txt` fajlove iz `najbolji_folder` u trenutni folder:

```
mv najbolji_folder/*.txt .
```

### Wildcards (džoker znakovi)

* `*` - bilo koji broj znakova
* `?` - tačno jedan znak

### Brisanje fajlova

```
rm novi_file.txt
```

```
rm noviji_file?.txt
```

Rekurzivno brisanje fajlova (ukoliko folder ima sadržaja):

```
rm -r ime_foldera
```

### Pretraga fajlova

```
find . -name "naziv"
find . -name "naziv*"
```

Rekurzivno pretraži sve fajlove u odredišnom direktoriju (u sljedećem primjeru to je direktorij `/home`):

```
find /home
```

Pretraga samo za fajlovima u tekućem direktoriju (ne izlistavamo direktorije):

```
find . -type f
```

Pretraga samo za direktorijima (ne ispisuju se fajlovi):

```
find . -type d
```

### Prompt znakovi

* `$` - nalazimo se kao obični korisnik
* `#` - nalazimo se kao root

### Promjena korisnika

Prelazak u root (potrebna šifra):

```
su root
```

Logovanje kao korisnik (novi login shell):

```
su korisnik -l
```

### Dozvole nad fajlovima

`chmod` - mijenja dozvole nad fajlom.

Oktalne dozvole:

```
User -> Groups -> Others
Read = 4, Write = 2, Execute = 1
```

Simboličke oznake:

* `+` dodaje dozvolu
* `-` uklanja dozvolu
* `=` postavlja dozvolu ali uklanja ostale

Primjeri:

Uklanjamo korisniku pravo čitanja fajla `test.sh`:

```
chmod u-r test.sh
```

Isto ali oktalno (write za vlasnika, read za grupu i ostale):

```
chmod 244 test.sh
```

Prebacujemo vlasništvo fajla na root:

```
sudo chown root test.sh
```

Prebacujemo vlasništvo fajla na korisnika:

```
sudo chown korisnik test.sh
```

### Korištenje pipe-ova

```
echo "hello" | wc
```

Rezultat: `1  1  6` - jedna linija, jedna riječ i 6 znakova.

### Čitanje sadržaja fajlova

`cat` (concatenate) - ispisuje sadržaj fajla:

```
cat dugiTekst.txt
```

`head` - ispisuje prvih 10 linija:

```
head dugiTekst.txt
```

`tail` - ispisuje zadnjih 10 linija:

```
tail dugiTekst.txt
```

Ispiši zadnjih 5 linija pomoću `tail` komande:

```
tail -n 5 dugiTekst.txt
```

Kombinacija komandi sa pipe-om:

```
cat dugiTekst.txt | cat -n | tail -n 5
```

`less` - interaktivno pregledavanje dugačkih fajlova:

```
less dugiTekst.txt
```

### Grep - pretraga teksta u fajlovima

```
grep "text" file.txt
```

### Korisne komande

* `.`  - oznaka za trenutni folder
* `ls -al` - pregled svih fajlova u trenutnom direktoriju (uključujući skrivene)
* `printenv` - ispis svih environment varijabli
* `pwd` - print working directory, provjera putanje na kojoj se nalazimo

### Generisanje SSH ključa

```
ssh-keygen -t rsa
```

### Dodavanje korisnika u sudo ili admin grupu

```
adduser username sudo
```

```
adduser username admin
```

### Archive komande

```
tar -cvf myfile.tar Vjezba_Files/
```

Opcije: `c` - create, `v` - verbose, `f` - output to file.

## Procesi

Izlistaj sve procese svih korisnika:

```
ps -ef
```

* `e` - ispis svih procesa u sistemu
* `f` - ispis dodatnih podataka o procesima

Ili:

```
ps aux
```

Izlistaj procese samo za `sshd` korisnika:

```
ps -f -u sshd
```

Sortiraj procese po potrošnji memorije:

```
ps aux --sort pmem
```

Sortiranje procesa po CPU potrošnji:

```
ps aux --sort pcpu
```

### Slanje procesa u background

Nakon komande dodamo znak `&`:

```
nano &
```

Izlistamo procese u backgroundu:

```
jobs
```

Vratimo komandu u foreground:

```
fg
```

Stopiranje background procesa. Nakon izlistavanja procesa:

```
jobs
[1]+  Running   "Komanda koju smo poslali u background"
```

Ubijamo proces po broju:

```
kill %1
```

### Korištenje Jekyll-a

Jekyll pretvara običan tekst u statičke web stranice.

1. Logovanje na server
2. Dodavanje novog korisnika:

```
adduser korisnik
```

3. Logovanje kao korisnik:

```
su korisnik -l
```

4. Instalacija programskog jezika (u ovom slučaju RVM i Ruby 2.5)

5. Ažuriranje gem-ova:

```
gem update
gem update --system
```

6. Kao korisnik generisati novi ključ:

```
ssh-keygen -t rsa
```

7. Generisani ključ za korisnika dodati na GitHub repo gdje je forkovan LugZe blog.

8. Instaliranje Bundler-a:

```
gem install bundler
```

9. Kloniranje repozitorija i instalacija Jekyll-a:

```
git clone naziv_git_repoa
gem install jekyll bundler
```

10. Pokretanje Jekyll servera u backgroundu:

```
bundle exec jekyll serve &
```

### Pronalaženje public IP adrese i komande ping/traceroute

`ping ime_servera` - mjerenje odaziva nekog servera. Ovom komandom, pored drugih podataka, saznajemo public IP servera.

`traceroute ime_servera` - izlistavanje svih ruta, servera koji se nalaze u hijerarhiji do nekog servera.

IP adresa - adresa servera:

* `0.0.0.0` - ukoliko server ima 10 IP adresa, ovakvim navodom server će slušati na svim adresama
* `127.0.0.1` - IP adresa lokalnog računara (nije routabilna)

### Pronalaženje javne ili privatne IP adrese servera

Ukoliko želimo saznati IP adresu remote servera na kojem se nalazimo:

```
ifconfig
```

Ukoliko smo neprivilegovani korisnik:

```
/sbin/ifconfig
```

**Napomena:** Moderna zamjena za `ifconfig` je komanda `ip addr`.

Nakon ukucane komande tražimo adresu sa `inet` prefiksom što je ujedno i IP adresa servera.

#### Zašto kao obični korisnik moramo kucati punu putanju do `ifconfig` komande?

Komanda `ifconfig` se nalazi u direktoriju `/sbin` stoga moramo provjeriti da li se taj direktorij nalazi u `$PATH` shell varijabli. Korisniku su dostupni programi tj. komande koje se nalaze u putanjama foldera koji su izlistani u `$PATH` shell varijabli.

Kada smo logovani kao root korisnik to možemo testirati na sljedeći način:

```
whoami
root
```

Izlistamo foldere iz `$PATH` varijable:

```
echo $PATH
```

Ili filtriramo samo za `/sbin` gdje se nalazi `ifconfig`:

```
echo $PATH | grep '/sbin'
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

Kao što vidimo dobili smo traženi `/sbin` što znači da root može direktno pozivati programe koji se nalaze u `/sbin` direktoriju.

Sada je potrebno isto da uradimo za običnog/neprivilegovanog korisnika kako bi provjerili zašto taj isti korisnik nema po defaultu pristup komandama iz `/sbin` direktorija.

Logujemo se kao neprivilegovani korisnik:

```
su emin -l
```

Provjerimo da li je login bio uspješan:

```
whoami
emin
```

Zatim provjerimo sadržaj `$PATH` varijable:

```
echo $PATH
```

Ili filtriramo za `/sbin` direktorij što je cilj ove vježbe:

```
echo $PATH | grep '/sbin'
```

Dobijamo prazan odgovor što znači da se `/sbin` ne nalazi u `$PATH` varijabli. To je razlog zašto po defaultu ne možemo koristiti komandu `ifconfig` i dobijamo grešku `ifconfig: command not found`.

Ovo možemo riješiti tako što za trenutnog korisnika dodamo `/sbin` putanju u `$PATH` varijablu:

```
PATH=$PATH:/sbin
```

Sada možemo koristiti `ifconfig` komandu bez unošenja pune putanje:

```
whoami
emin
```

```
ifconfig lo
lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 2563  bytes 299115 (292.1 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 2563  bytes 299115 (292.1 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

**Napomena:** Na ovaj način smo samo trenutno izmijenili vrijednost `$PATH` varijable. Nakon što se korisnik odjavi tj. uradi logout, vrijednost `$PATH` varijable će biti vraćena na prvobitne postavke tj. biće resetovana.

### Kako prepoznavati privatne IP adrese

Private IPv4 address spaces:

| RFC1918 naziv | IP adresni raspon | Broj adresa |
|---|---|---|
| 24-bit blok | 10.0.0.0 – 10.255.255.255 | 16,777,216 |
| 20-bit blok | 172.16.0.0 – 172.31.255.255 | 1,048,576 |
| 16-bit blok | 192.168.0.0 – 192.168.255.255 | 65,536 |

Izlistavanje server interfejsa komandom:

```
ifconfig
```

* `inet` označava IPv4 saobraćaj
* `inet6` označava IPv6 saobraćaj
