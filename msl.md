---
layout: page
title: Mala Škola Linux-a
permalink: /mala-skola-linuxa/
---

Verzija dokumenta 0.0.1

## Uobičajena organizacija foldera u Linuxu

* `/bin`  - programi koje koriste i administratori i korisnici
* `/dev`  - datoteke koje predstavljaju hardverske uredjaje (mrezna, graficka)  
* `/etc`  - konfiguracijske datoteke
* `/home` - direktoriji korisnika
* `/sbin` - sistemski programi
* `/tmp`  - privremene datoteke
* `/usr`  - korisnicki programi, dokumentacija i biblioteke
* `/var`  - sistemski zapisi i druge datoteke.

* Više na [linku](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard).

## Upravljanje korisnicima i grupama

Korsnici imaju sopstveni `home` direktorij koji se nalazi u folderu `/home`. Izuzetak je `root` korisnik, čiji home direktorij se nalazi na lokaciji `/root`.

#### Vježba: nekoliko načina kako pristupiti home folderu

* koristiti `cd` komanu bez argumenata.

```
cd
```
* kao argument `cd` komandi proslijediti znak tildu tj. `~`.

```
cd ~
```
* kao argument `cd` komandi proslijediti build in shell varijablu `$HOME`

```
cd $HOME
```
### Komanda `finger`

Komanda `finger` ispisuje informacije o korisniku. Kao argument komandi proslijedimo korisničko ime tj. `username` korisnika. U sljedećem primjeru `finger` će prikazati informacije o korisniku `root`.

```
finger root
```

kao odgovor dobijamo sljedeće informacije

```
finger root
Login: root           			Name: root
Directory: /root                    	Shell: /bin/bash
On since Sun Mar 11 19:22 (UTC) on pts/2 from 77.77.218.xx
   18 minutes 24 seconds idle
     (messages off)
On since Sun Mar 11 19:31 (UTC) on pts/3 from 77.77.218.xx (messages off)
New mail received Mon Mar  5 15:40 2018 (UTC)
     Unread since Tue Feb 27 19:15 2018 (UTC)
No Plan.
```

Ukoliko dobijete grešku `-bash: finger: command not found` potrebno je da instalirate komandu sa na sljedeći način:

```
apt-get update
apt-get install finger
```

### Komanda `id`

Ova komanda nam daje informacije o korisniku kao što su

* `id`     - broj korisnika
* `gid`    - group id tj. broj primarne grupe kojoj korinsik pripada
* `groups` - kompletna lista grupa kojoj korisnik pripada, tj gid i naziv grupe.

Kada komandi `id` argument ostavimo prazan, podrzaumijeva se da zelimo saznati informacije o trenutno logovanom korisniku, odnosno korisniki koji izvrsava komandu. Primjer:

```
id
uid=0(root) gid=0(root) groups=0(root)
```

Kada kao argument komandi `id` proslijedimo `username` dobijemo info o tom korinsiku.

```
id korisnik
uid=1001(korisnik) gid=1001(korisnik) groups=1001(korisnik),27(sudo)
```

Ako želimo saznati samo `id` broj korinsiko koristimo parametar `-u`.

```
id -u root
0
```

Ako želimo saznati broj primarne grupe nekog korisnika, koristimo parametar `-g`.

```
id -g korisnik
1001
```

Ako želimo saznati brojeve svih grupa kojoj priapada korisnik, korisitmo parametar `-G`.

```
id -G korisnik
1001 27
```

## Rad sa fajlovima i direktorijima

File ili direktorij sa space Moj File se pise kao ```Moj\ file```

#### Ispis sadržaja direktorija

```ls```  -> listanje

```ls —a -l -h``` -> Listaj a-detalje, l-long format, h-jasnije covjeku

ili ovako:

```
ls -alh
```

##### Ispisi listu fajlova i direktorija unutar trenutnog direktorija

```
ls .
```

Ispisi listu fajlova i direktorija unutar trenutnog direktorija ukljucujuci i sakrivene fajlove skriveni fajlvi su fajlovi cije ime pocinje sa tackom odnosno znakom .

```
ls -al .
```

Ispisi listu fajlova i direktorija unutar trenutnog direktorija, te sadrzaj direktorija koji se nalaze u tekućem direktoriju

```
ls -al *
```


Ispisi listu fajlova i direktorija unutar trenutnog direktorija na nacin da i direktorije tretiramo kao obične fajlove te ne ispisujemo njihov sadržaja

```
ls -ald *
```


Ispisi listu fajlova i direktorija koji pocinju sa znakom . odnosno ispisi samo skrivene fajlove i direktorije

```
ls -ald .*
```


#### Ispisi inode broj fajla

```
ls -i ime_fajla
```


### Kreiranje simboličkih linkova

prvo napravimo fajl

```
touch fajl_jedan
```


zapišemo nesto u fajl pomoću redirekcije

```
echo "NEKI TESTNI SADRZAJ">fajl_jedan
```


provjerimo da li je zapisano u fajl

```
cat fajl_jedan
```

napravimo simbolički link na novi fajl

```
ln -s fajl_jedan fajl_dva_koji_je_simbolicki_link_na_prvi_fajl
```

ispišemo sadrzaj drugog fajla koji je simbolički link

```
cat fajl_dva_koji_je_simbolicki_link_na_prvi_fajl
```

možemo primjetiti da je sadržaj oba fajla isti

provjerimo inodove oba fajla

```
ls -i fajl_jedan
ls -i fajl_dva_koji_je_simbolicki_link_na_prvi_fajl
```

možemo promjetiti da su inode brojevi razliciti sto znaci da su razliciti fajlove te ako jedan izbrisemo to znaci da drugi fajl nece biti izbrisan


#### Vjezba: izbrisati prvi fajl. Da li je drugi fajl koji je simbolicki link izbrisan? Da li mozemo pomocu cat komande izlistati sadrzaj drugog fajla?



## Hard linkovi

Kreirati fajl i dodati neki sadrzaj

```
touch fajl_prvi
echo "NEKI TESTNI SADRZAJ">fajl_prvi
```

napraviti hard link

```
ln fajl_prvi fajl_drugi
```

provjeriti inode brojeve za oba fajla

```
ls -i fajl_prvi
6257560 fajl_prvi
```

inode broj fajla je broj `6257560`
```
ls -i fajl_drugi
6257560 fajl_drugi
```

inode broj drugog fajla je takodjer `6257560`


inode brojevi su isti sto znaci da su oba fajla linkaju na istu lokaciju na disku


##### Vjezba: Sta se desi ako izbrisemo drugi fajl, da li ce prvi fajl biti izbrisan?


```
rm fajl_drugi
```


```
ls -R IME FOLDERA/
```

-> gledanje u sadrzinu i oko foldera rekurzivno tj. pregled cijele strukture foldera


```
ls —help
```

 -> pomoc o komandi


```
man ls
```
 -> man-om objasnjvamo komande i lista se sa f i b

**********************

```
cd IME FOLDERA
```
 -> ulazak u folder

SAMO cd vraca na pocetni folder

```
cd ..
```
 -> izlazak iz foldera

```
cd ../../NEKI FOLDER
```
 -> ulazak na udaljeni folder, dva levela iznad


### Putanje do programa


koristimo komandu whereis i which da saznamo putanju gdje je instaliran program, odnosno gdje se nalazi binary trazenog programa

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


#### Vjezba: pratiti kako se mijenja pwd vrijednost nakon svake izmjene current directorija

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


```mkdir``` -> pravljenej foldera

```mkdir folder/subfolder/subsubfolder```

```mkdir -p``` -> pravljenej parent directorija, koristi se u slucaju da parent folder ne postoji te zelimo u isto vrijeme napraviti parent folder te u njemu subfoldere


```touch mojFile.txt```
 -> pravljenje filea

```
cp mojFile.txt mojNoviFile.txt
```
 -> kopiranje filea

move files:

```
mv
```
 -> pomijeranje fileova koje se moze koristiti i za rename
```
mv novi_file.txt najbolji_folder
```

```
mv novi_file.txt najbolji_folder/novi_file2
```

```mv najbolji_folder/*.txt .``` -> pomjeri sve fileove koji zavrsavaju sa .txt iz najbolji_folder u trenutni folder

Wildcards:

```
* -> any number of characters
? -> one of the character
```


delete files:

```
rm novi_file.txt
```

```
rm noviji_file?.txt
```


```
rm -r
```
 -> rekurzivno brisanje fileova (ukoliko folder ima sadrzaja)

Pretraga fileova:

```
find . -name “naziv”
find . -name “naziv*”
```

Rekurzivno pretrazi sve fajlove u odredisnom direktoriju (u sljedecom primjeru to je direktorij /home)

```
find /home
```

Pretraga za fajlovima, u tekucem direktoriju, samo tipa file (ne izlistavamo direktorije)

```
find . -type f
```

Pretraga za direktorijima, ne ispisuju se fajlovima

```
find . -type d
```


```
$ - nalazim se u useru
# - sada sam root
```

```
su root
```
 -> prelazak u root (potrebna sifra)

```
su korisnik -l
```
 (novi login shell) - logovanje kao korisnik

```
chmod -> change the permission on a file
```

Octal file permisions:

```
User -> Groups -> others
Read = 4, Write = 2, Execute =1
```

```
+ adds permission
- remove permission
= adds permission but removes others
```

```chmod u-r test.sh``` -> uzimamo useru pravo citanja filea test.sh

```chmod 244 test.sh``` -> isto ali oktalno

```sudo chown root test.sh``` -> prebacujem prava filea na root

```sudo chown korinik test.sh``` -> prebacujem prava filea na usera korinik


Using pipes:

```echo “hello” | wc``` -> 1  1  16  one line, one word and 6 characters


Cat - Concatenate(stick two or more things together) and print files

```cat dugiTekst.txt``` -> izlistavamo cijeli tekst

```head dugiTekst.txt``` -> prvih 10 linija

```tail dugiTekst.txt``` -> zadnjih 10 linija

# Ispiši zadnjih 5 linija pomoću tail komande

```
tail -n 5 dugiTekst.txt
```

```
cat dugiText | cat -n | tail -n 5
```
 -> kombinacija

```less dugiText``` -> izlistavanje

### Grep - Search files for text that matches a given pattern

```
grep "text" file.txt
```



```.``` -> Current folder


```la -al``` -> view . files from current directory

```printnv``` -> printanje svih varijabli

```su korisnik -l``` (novi login shell)

```pwd``` -> print working directory i provjera putanje na kojoj se nalazimo

#### Generisanje set key-a

```ssh-keygen -t rsa```



#### Adding users to sudo or admin group

```adduser username sudo```

```adduser username admin```



<<<<<<< HEAD
Archive komande

```tar -cvf (c-create, v-verbot, f-output to file) myfile.tar Vjezba\ Files/```



## Procesi

# Izlistaj sve procese svih korisnika

```
ps -ef
```
e --> ispis svih procesa u sistemu
f --> ispis dodatnih podataka o procesima


ili

```
ps -aux
```

# izlistaj procese samo za sshd korisnika

```
ps -f -u sshd
```

# sortiraj procese po potrošnji memorije

```
ps aux --sort pmem
```

# sortoranje procesa po CPU potrošnji

```
ps aux --sort pcpu
```

### Slanje procesa i background



nakon komande dodamo znak &

```
nano &
```

izlistamo procese u backgroundu

```
jobs
```

vratimo komandu u foreground

```
fg
```

Stopiranje background procesa:
Nakon izlistavanja procesa
```
jobs
[1]+  Running   "Komanda koju smo poslali u background"
```
Ukucavamo

```
kill 1 --> broj procesa
```


###Koristenje jerkyll-a (Transform your plain text into static websites)

1. Logovanje na server
2. Dodavanje novog korisnika
```
adduser korisnik
```

3. Logovanje kao korisnik
```
su korisnik -l
```


4. Instalacija programskog jezika (u ovom slucaju rvm i ruby 2.5)
5.
```
gem update
i
gem update —system
```


6. Kao korisnik generisati novi kljuc
```
ssh-keygen -t rsa
```

7. generisani kljuc za korisnika dodati na github repo gdje je forkovan lugze blog
8. Instaliranje bundle-a
```
apt-get install bundle
```

9. Ponoviti postupak kloniranja datog repo-a i instalacije jekyll-a

```
git clone naziv git repoa
```
instalacije jekyll-a
```
gem install jekyll bundler
```

10. Pokretanje jekyll serve u backgroundu

```
bundle exec jekyll serve &
```

###Pronalazenje public ip adrese i komande ping/traceroute

`ping ime servera` - mjerenje odaziva nekog servera. Ovom komandom, pored drugih podataka, saznajemo public ip servera

`traceroute ime servera` - izlistavanje svih routea, servera koji se nalaze u hijerarhiji nekog servera

IP adresa - adresa servera

`0.0.0.0` - Ukoliko server ima 10 ip adresa, ovakvim navodom server ce slusati svih 10 tj. sve adrese
`127.0.0.1` - IP adresa lokalnog racunara (nije routabilna)

#### Pronalazenje javne ili privatne IP adrese nekog servera:

* 1. Ukoliko zelimo saznati ip adresu remote servera na kojem se nalazimo

```
ifconfig - ukoliko smo root
```

ili

```
/sbin/ifconfig - ukoliko smo korisnik
```

Nakon ukucanie komande trazimo adresu a `inet` prefiksom sto je ujedno i public ip adresa servera

##### Zasto kao obicni korisnik moramo kucati punu putanju do `ifconfig` komande?

Komanda ifconfig se nalazi u direktoriju `/sbin` stoga moramo provjeriti da li se taj direktorij nalazi u `$PATH` shell varijabli. Korisniku su dostupni programi tj. komande koji se nalaze u pitanjama foldera koji su izlistani u `$PATH` shell varijabli.


 Kada smo logovani kao root korisnik to mozemo testirati na sljedeci nacin.

 ````
 whoami
root
 ````

 Izlistamo foldere iz `$PATH` varijable

 ````
 echo $PATH
 ```

 ili filtriramo samo za `/sbin` gdje se nalazi ifconfig

 ````
 echo $PATH | grep '/sbin'
 /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
 ````

 kao sto vidimo dobili smo trazeni `/sbin` sto znaci da root moze direktno pozivati programe koji se nalaze u `/sbin` direktoriju.

 Sada je potrebno isto da uradimo za obicnog/neprivilegovanog korisnika kako bi provjerili zasto taj isti korisnik nema po defaultu pristup komandama iz `/sbin` direktorija.

 * logujemo se kao neprivilegovano korisnik

 ````
 eu emin -l
 ````

 * provjerimo da li je login bio uspjesan

 ````
 whoami
emin
````

* zatim provjerimo sadrzaj `$PATH` varijable

````
echo $PATH
````

* ili filtriramo za `/sbin` direkotorijem sto je cilj ove vjezbe

````
echo $PATH | grep '/sbin'
````

dobijamo prazan odgovor sto znaci da se `/sbin` ne nalazi u `$PATH` varijabli. To je razlog zasto po defaultu ne mozemo koristiti komandu `ifconfig` i dobijamo gresku `ifconfig: command not found`.

* Ovo mozemo rijesiti tako sto za trenutnog korisnika dodamo `/sbin` putanju u `$PATH` varijablu. Potrenno je uraditi sljedece

````
PATH=$PATH:/sbin
````

Sada mozemo koristiti `ifconfig` komandu a da ne unosimo punu putanju do komande.

````
whoami
emin
````

````
fconfig lo
lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 2563  bytes 299115 (292.1 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 2563  bytes 299115 (292.1 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
````

* Napomena: na ovaj nacin smo samo trenutno izmijenili vrijednost `$PATH` varijable, nakon sto se korisnik odjavi tj. uradi logout vrijednost `$PATH` varijable ce biti vracena na prvobitno postavke tj. bice resetovana.

### Kako prepoznavati privatne ip adrese

Private IPv4 address spaces

RFC1918 name | IP address range | number of addresses
-------------  ----------------   --------------------
24-bit block | 10.0.0.0-10.255.255.255 | 16,777,216
20-bit block | 172.16.0.0-172.31.255.255	|	1,048,576
16-bit block | 192.168.0.0 – 192.168.255.255	| 65,536

Izlistavanje server interfejska komandom:

```
ifconfig
```

inet denotes IPv4 traffic

inet6 denotes IPv6 traffic
