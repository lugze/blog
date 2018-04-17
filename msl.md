---
layout: page
title: Mala Škola Linux-a
permalink: /mala-skola-linuxa/
---

Verzija dokumenta 0.0.2

* TOC
{:toc}

# 1 Linux Zajednica

## 1.1 Evolucija Linux i popularnih operativnih sistema

* open source filozofija
* Distribucije
* Embedded Systems

* Android
* Debian, Ubuntu (LTS)
* CentOS, openSUSE, Red Hat
* Linux Mint, Scientific Linux

## 1.2 Poznate open source aplikacije

* OpenOffice.org, LibreOffice, Thunderbird, Firefox, GIMP
* Apache HTTPD, NGINX, MySQL, NFS, Samba
* C, Java, Perl, shell, Python, Ruby ,Samba
* dpkg, apt-get, rpm, yum

# 2: Snalaženje na Linux Sistemu

## 2.1 Command Line Basics


Description: Basics of using the Linux command line.

**Key Knowledge Areas:**

*    Basic shell
*    Command line syntax
*    Variables
*    Globbing
*    Quoting

**Terms and Utilities:**

*    Bash
*    echo
*    history
*    PATH env variable
*    export
*    type



### 2.1.1 Struktura SHELL Komandi

Komandna u shellu imaju sljedecu formu.

````
komanda  [opcije]  [argumenti]
````

* Komanda - "Sta zelimo uraditi"
* Opcije - "Kako nesto uraditi"
* Argumenti - "Sa čime to raditi"

Komandni parametri ugrubo se dijele u **opcije** i **argumente**.

* Parametri koji pocinju sa znakom **dash** odnosno **-** se nazivaju `opcije`. Ovaj tip parametara je ***opcionalan*** iz cega i nosi naziv.

* Parametri koji ne pozinju sa znakom **-** se nazivaju **argumenti**.

### 2.1.2 Tipovi komandi

* Interne komande - komande koje omogucava sam shell. Bash ili Bourne-again shell omogucava oko 30 internih komandi.

* Eksterne komande - komande koje ne pokrece sam shell, nego pokrece binarne fajlove koji se nalaze u sistemskih direktorijima kao sto su `/bin` ili `/usr/bin`.


#### 2.1.2.1 Komanda **type**


Mozemo koristiti `type` komandu da saznamo tip komande.

* Primjer interne tj. **shell builtin** komande je komanda `echo`.

````
type echo
````

* Primjer eksterne komande je komanda `date`.

````
type date
````

Kao odgovor za eksterne komande dobijamo putanju do binarnog programa. U slucaju komande `date` dobijamo putanju `/bin/date`.



Vise o `type` komandi

````
type --help
userdel --help
````


##### ***Vjezba*** sa komandom `type`

Koje od sljedecih komandi su interne a koje eksterne?

````
alias, echo, rm, test
````

### 2.1.3 Dodatna shell pravila

Shell ne samo da razlikuje mala i velika slova kada se unose imena komandi, nego isto pravilo vazi i za parametre i opcije te i imena fajlova.


### 2.1.4 “Escaping” characters

Ako zelimo napraviti fajl sa razmakom u imenu, moramo koristiti navodnike. Koristenje navodnika je jedan vid tzv. “Escaping” karaktera.  “Escaping” je potrebno raditi sa svim specijalnom karakterima.

Pored razmaka u specijalne karaktere ubrajamo

````
$&;(){}[]*?!<>"'
````

* Za “Escaping” samo jednog karaktera koristimo znak `\` ili backslash.
* Za “Escaping” vise rijeci od jednom koristimo jednostruke `''` i dvostruke `"…"` navodnike.

#### 2.1.4.1 Pravljenje fajla sa razmakom u imenu

````
touch 'Novi Fajl'
````

Kada ne bi koristili navodnike

````
touch Novi Fajl
````

napravili bi smo dva fajla i to `Novi` i `Fajl`.




## 2.2 Using the Command Line to Get Help

Description: Running help commands and navigation of the various help systems.

**Key Knowledge Areas:**

*    Man
*    Info

**Terms and Utilities:**

*    man
*    info
*    Man pages
*    `/usr/share/doc/`
*    locate


### Opcija **-help**

```
ls —help
```

 -> pomoc o komandi


### Komanda *man*

Komanda ```man``` (manual) podrazumjeva nesto opsirniju dokumentaciju.
Riječ je o dokumentaciji koja opisuje naredbe, a koja je podijeljena na sekcije i stranice.
Sekcije/poglavlja pomazu odrediti kako se komande koriste npr. kao korisnik ili kao root korisnik

Ako želimo da nam se ispise stanica iz nekog konkretnog poglavlja, tada kao argument trebamo navesti broj poglavlja.

Sekcija 1 : Standardni korinik
Sekcija 5: Komanze konfiguracije fajla
Sekcija 8: Root korisnik



```man 1 komanda````


Koristenje komande ```whatis``` omogucava pronalazenje man stranica za datu komandu.

```whatis crontab```


```man ls```
-> man-om objasnjvamo komande i lista se sa f i b


Iz dokumentacije izlazimo sa ```q```


### Komanda *info*

Naredba info omogućava pristup do dokumenata koji čine drugi sistem pomoći, takozvane info-stranice. okumentaciju u ovom formatu imaju samo neki, većinom noviji programi posebno pisani upravo za Linux. Ukoliko ne postoji dokumentacija za traženi pojam među info-stranicama, naredba info će ispisati odgovarajuću man-stranicu (ako ona postoji).


```info komanda```


### Komanda *which*
 
Komanda which, je jako korisna komanda u Linuxu, i ispisuje putanju do naredbi koje su izvršne datoteke.
Da bi naredba which mogla pronaći zadanu naredbu na disku, potrebno je da se ona nalazi u direktoriju koji je naveden u varijabli PATH.
 
Sintaksa:

```which komanda```

Primjer:

$ which info
/usr/bin/info

```which ls```




## 2.3 Using Directories and Listing Files

Description: Navigation of home and system directories and listing files in various locations.

**Key Knowledge Areas:**

* Files, directories
* Hidden files and directories
* Home
* Absolute and relative paths

**Terms and Utilities:**

* Common options for ls
* Recursive listings
* cd
* `.` and `..`
* home and `~`
* pretraga pomocu komande `find`


### 2.3.0 Uobičajena organizacija foldera u Linuxu

* `/bin`  - programi koje koriste i administratori i korisnici
* `/dev`  - datoteke koje predstavljaju hardverske uredjaje (mrezna, graficka)  
* `/etc`  - konfiguracijske datoteke
* `/home` - direktoriji korisnika
* `/sbin` - sistemski programi
* `/tmp`  - privremene datoteke
* `/usr`  - korisnicki programi, dokumentacija i biblioteke
* `/var`  - sistemski zapisi i druge datoteke.

* Više na [linku](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard).


### 2.3.1 Identifikacija Tipova Fajlova pomocu komande **file**

Prvo sto moramo razumijeti jeste da u **Linuxu sve je fajl**, direktoriji su posebna vrsta fajla.

Pored klasinih fajlova i direktorija imamo i fajlove koji pokazuju na uredjaje kao sto su USB portovi i hard diskovi. Ovi fajlovi su locirani u `/dev` direktoriju, gdje je **dev** skracenica od **devices**.

Pomocu komande **file** mozemo odrediti tip jednog ili vise fajlova. Pomocu sljedece komande cemo pitati **file** komandu da nam izlista vrstu fajla za sljedece fajlove sa sljedece liste.

* /dev/sda1
* /etc
* /etc/passwd


Mozemo pojedinacno piatti za tip fajla na sljedeci nacin

````
file /dev/sda1
/dev/sda1: block special (8/1)
````

````
file /etc/
/etc/: directory
````

````
file /etc/passwd
/etc/passwd: ASCII text
````
ili grupno na sljedeci nacine

````
file /dev/sda1 /etc /etc/passwd
/dev/sda1:   block special (8/1)
/etc:        directory
/etc/passwd: ASCII text
````

### 2.3.2 Skriveni fajlovi

U Linuxu skriveni fajlovi su fajlovi cije ime pocinje sa **tackom** odnosno zakom **.**. Da bi izlistali skrivene fajlove koristimo opciju **-a** sa komanom **ls** da nam izlista sve vrste fajlova ukljucujuci i skrivene fajove.

Pomocu pipinga i grep komande mozemo izlistati sve fajlove koji pocinju sa znakom **.**.

````
ls -a | grep '^.'
````

Komanda **ls** ima opcije **-a** i **-A**.

* opcija **-a** izlistava sve fajlove
* opcija **-A** islistava skoro sve

Opcija **-A** ne izlistava trenutni direktorij cija je oznaka sama **tacka** odnosno znak **.** te ne izlistava direktorij roditelj cija je oznaka **dvije tacke** odnosno **..**.

### 2.3.3 Home folder

Korsnici imaju sopstveni `home` direktorij koji se nalazi u folderu `/home`. Izuzetak je `root` korisnik, čiji home direktorij se nalazi na lokaciji `/root`. U home direktoriji korisnici cuvaju svoje fajlove i personalne **login skripte** i **bash history** odnosno listu komandi koje su prethodno kucali.

* `~/.bashrc`
* `~/.bash_history`

Korisnik prilikom logovanja ce biti odveden u home direktorij. Putanja do home direktorija je definisana u varijabli `$HOME`. Mozemo ispisati trenutnu vrijednost **$HOME** varijable pomocu **echo** komande na sljedeci nacin.

````
echo $HOME
````
Korisnici mogu pristupiti home folderu tako sto koriste **cd** komandu bez argumenata te ako koriste znak tildu odnosno **~**.

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

### 2.3.4 Prethodni direktorij

Korisna opcija komandi **cd** je **-** opcija. Njihova kombinacija izgleda ovako `cd -`. Ova komanda korisnika vraca u prethodni diretorij. Ovo funkcionise pomocu varijable **$OLDPWD**.

#### 2.3.4.1 Vjezba: vracanje u prethodni direktorij

````
cd ~
cd /tmp
echo $OLDPWD
cd $OLDPWD
cd /home
cd -
echo $OLDPWD
````

### 2.3.6 Putanje do Fajlova

Kada pristupamo fajlovimo koristimo putanje. Putanje mogu biti

* `apsolutne` putanje
* `relativne` putannje

Primjeri putanja

* **.** - Trenutni tj. tekući direktoriju.
* **..** - Direktorij iznad ili roditelj trenutnog direktorija.
* **../..** - Direktorij dva direktorija iznad trenutnog direktorija.
* **/etc/passwd** - Apsulutna ili puna putanja do fajla `passwd` koji se nalazu u sistemom `etc` direktoriju.
* **../etc/passwd** - Ukuloko je trenutni direktorij `/home` ovo bi bila relativna putanja na `passwd` fajla.


#### Fajlovi i direktoriji koji imaju razmak u imenu

File ili direktorij sa space Moj File se pise kao ```Moj\ file```

### 2.3.7 Ispis sadržaja direktorija sa komandom `ls`

Listanje

```
ls
```

Listaj **a**-detalje, **l**-long format, **h**-velicina fileova izrazena razumljivije

```
ls —a -l -h
```

ili ovako:

```
ls -alh
```

##### Ispisi listu fajlova i direktorija unutar trenutnog direktorija

Ako zelimo izlistati sadrzaj tekuceg foldera korisimo komandu ispod.

```
ls .
```

* Ispisi listu fajlova i direktorija unutar trenutnog direktorija ukljucujuci i sakrivene fajlove skriveni fajlvi su fajlovi cije ime pocinje sa tackom odnosno znakom .

```
ls -al .
```

* Ispisi listu fajlova i direktorija unutar trenutnog direktorija, te sadrzaj direktorija koji se nalaze u tekućem direktoriju

```
ls -al *
```

* Ispisi listu fajlova i direktorija unutar trenutnog direktorija na nacin da i direktorije tretiramo kao obične fajlove te ne ispisujemo njihov sadržaja

```
ls -ald *
```

Ispisi listu fajlova i direktorija koji pocinju sa znakom `.` odnosno ispisi samo skrivene fajlove i direktorije

```
ls -ald .*
```


#### Ispisi inode broj fajla

```
ls -i ime_fajla
```

Gledanje u sadrzinu i oko foldera rekurzivno tj. pregled cijele strukture foldera

```
ls -R IME FOLDERA/
```

#### Komanda **cd**

ulazak u folder

```
cd IME FOLDERA
```

SAMO `cd` vraca na pocetni folder odnosno home folder.


izlazak iz trenutnog foldera u jedan nivo vise.

```
cd ..
```

ulazak na udaljeni folder, dva levela iznad

```
cd ../../NEKI FOLDER
```

* Vise o komandi `cd`

````
man cd
````


## Komanda **find**

Sluzi za pretragu file-ova

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

* Vise o komandi `find`

````
man find
````

## 2.4 Creating, Moving and Deleting Files

Description: Create, move and delete files and directories under the home directory.

**Key Knowledge Areas:**

*    Files and directories
*    Case sensitivity
*    Simple globbing and quoting

**Terms and Utilities:**

*  mv, cp, rm, touch
*  mkdir, rmdir



### Pronalazenje putanje do programa pomocu komandi `whereis` i `which`


Koristimo komandu whereis i which da saznamo putanju gdje je instaliran program, odnosno gdje se nalazi binary trazenog programa

#### Komanda **which**

Komanda sluzi za pronalazenje datoteka u korisnickim putanja. Komanda provjerava da li fajl postoji u korisnickoj `$PATH` varijabli.

```
which nano
```

Ako se komanda ne nalazi u putanjama unutar `$PATH` varijable, komanda vraca prazan rezultat.

* Primjer

Logujemo se kao neprivilegovani korisnik

````
su -l korinsnik
````

````
which ifconfig
````

Dobijamo prazan odgovor.

* Vise o komandi `which`

````
man which
````


#### Komanda **whereis**

komanda sluzi za pretragu za `binary` datotekama odnosno ostalim komandama, source i manual stranica.

* Primjeri upotrebe

```
whereis nano
```

```
whereis bash
```


* Pretraga gdje se nalazi **binarna** datoteka

````
whereis -b bash
````

* Pretraga za **manual** stranicama nekog programa

````
whereis -m bash
````

* Vise o komandi `whereis`

````
man whereis
whereis --help
````

#### ***Vjezba***

Pratiti kako se mijenja pwd vrijednost nakon svake izmjene current directorija

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

### Komanda **mkdir**

pravljenje foldera

```
mkdir
```

```
mkdir folder/subfolder/subsubfolder
```

pravljenje parent directorija, koristi se u slucaju da parent folder ne postoji te zelimo u isto vrijeme napraviti parent folder te u njemu subfoldere

```
mkdir -p
```

### Komanda **touch**

pravljenje filea

```
touch mojFile.txt
```


### Komanda **cp**

kopiranje filea

````
cp mojFile.txt mojNoviFile.txt
````

### Komanda **mv**

move files:

```
mv
```

pomijeranje fileova koje se moze koristiti i za rename

```
mv novi_file.txt najbolji_folder
```

```
mv novi_file.txt najbolji_folder/novi_file2
```

pomjeri sve fileove koji zavrsavaju sa .txt iz najbolji_folder u trenutni folder

```
mv najbolji_folder/*.txt .
```

Wildcards:

```
* -> any number of characters
? -> one of the character
```

### Komanda **rm**

delete files:

```
rm novi_file.txt
```

```
rm noviji_file?.txt
```

rekurzivno brisanje fileova (ukoliko folder ima sadrzaja)

```
rm -r
```


### Shell prefixes

```
$ - nalazim se u useru
# - sada sam root
```


### logovanje korsnika

```
su root
```
 -> prelazak u root (potrebna sifra)

```
su korisnik -l
```
 (novi login shell) - logovanje kao korisnik



# Topic 3: The Power of the Command Line (weight: 9)
## 3.1 Archiving Files on the Command Line

Description: Archiving files in the user home directory.

** Key Knowledge Areas:**

*     Files, directories
*     Archives, compression

**Terms and Utilities:**

*     tar
*     Common tar options
*     gzip, bzip2
*     zip, unzip



Archive komande

### Komanda **tar**

```tar -cvf (c-create, v-verbot, f-output to file) myfile.tar Vjezba\ Files/```

### Komanda **bzip2**

* Kompresovanje fajla

````
bzip2 moj_file.txt
````

Sta se desava nakon kompresije? Da li izvorni fajl koji smo kompresovali id alje postoji?

````
ls moj_file.txt.*
````

* Dekompresovanje fajla

````
bzip2 -d moj_file.txt.gz
````

ili

````
bunzip2 moj_file.txt.bz2
````





# Topic 5: Security and File Permissions


## 5.1 Basic Security and Identifying User Types


Description: Various types of users on a Linux system.

**Key Knowledge Areas:**

*    Root and Standard Users
*    System users

**Terms and Utilities:**

*    /etc/passwd, /etc/group
*    id, who, w
*    sudo, su


#### Komanda **finger**

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

### Komanda **id**

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

## 5.2 Creating Users and Groups

Description: Creating users and groups on a Linux system.

**Key Knowledge Areas:**

*    User and group commands
*    User IDs

**Terms and Utilities:**

*    /etc/passwd, /etc/shadow, /etc/group, /etc/skel/
*    id, last
*    useradd, groupadd
*    passwd


### Komanda **useradd**

Sluzi za dodavanje korisnika.

Default psotavke se nalaze u sljedecim fajlovima

* 1. `/etc/default/useradd`

````
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
CREATE_MAIL_SPOOL=yes
````

* 2. default login postavke se nalaze u fajlu `/etc/login.defs`

Navedeni fajl kontrolise kada ce password da istekne, UID, GUID, HOME postavke itd.

* 3. Folder `/etc/skel` sadrzi fajlove koji ce biti kopirani u `home` difektorij korinsika prilikom dodavanja korisnika.

Sintaksa komande

`useradd ime_korisnika`

### Komanda **passwd**

Komanda sluzi za reporting i izmjenu passworda nekog korisnika.

Primjer upotrebe

* Ako zelimo report o statusu passworda korisnika

```
passwd -S username
````

* Ako zelimo status passworda svih korinsika

```
passwd -a -S
````
* Ako zelimo izmijeniti password korinsika

````
passwd ime_korisnika
````

### Komanda **usermod**

Ako zelimo izmijeniti odnosno modifikovati korinsika na sistemu koristimo ovu komandu.

Primjer

* Ako zelimo izmijeniti polje za komentar, kao sto je ime i prezimo

````
usermod -c "Ime Prezime" ime_korisnika
````
ili duza varijanta

````
usermod --comment "Ime Prezime" ime_korisnika
````

Vise o komandu `usermod` mozemo saznati na sljedece nacine:

````
man usermod
usermod --help
````

### Komanda **userdel**

Koristimo komandu kada zelimo korisnika izbrisati sa sistema.


* Brisanje korisnika bez brisanja home direktorija

````
userdel username
````

* Brisanje korisnika i home direktorija

````
userdel -r username
````

ili

````
userdel --remove username
````

Vise o komandi `userdel`

````
man userdel
userdel --help
````

### Upravljanje korisnicima i grupama

### Managing Linux Group Accounts

#### Datoteka `/etc/group`

Vise o datoteci

````
man /etc/group
````

#### Komanda **groupadd**

Sluzi za dodavanje nove grupe

* Ako zelimo dodati novu grupu `moja_grupa` sa brojem grupe **9000**

````
groupadd -g 9000 moja_grupa
````
Nakon dodavanja provjerimo da li je dodana grupa na sljedeci nacine

````
grep -i --color moja_grupa /etc/group
````

#### Komanda **groupmod**

#### Komanda **groupdel**

#### Komanda **su**

#### Komanda **sudo**

#### Log datoteke **/var/log/wtmp** i **/var/log/faillog**

Log fajlovi koji sluze za biljeske pokusaja autenticiranja korisnika



* /var/log/wtmp - binary, succesfully authentication attempts, command to view last
* /var/log/faillog - binary, failed authentication attempts, command to view faillog

##### Komanda **faillog**

Ako zelimo procitati zapise log datoteke `/var/log/faillog` korisitmo komandu faillog.

* Primjer kako koristiti komandu

````
faillog -u username
````

* Vise o komandi `faillog`

````
man faillog
````

#### Komanda **who**

Komanda prikazuje ko je logovan

Primjeri

````
who
````
````
who -a
````

ili

````
who --all
````

Vise o komandi `who`

````
man who
who --help
````

#### Komanda **w**

Komanda prikazuje trenutno logovane korisnike, njihove IP adrese, i sta trenutno rade korisnici.

Primjeri

````
w
````

Vise o komandi `w`

````
man w
w --help
````


## 5.3 Managing File Permissions and Ownership

Description: Understanding and manipulating file permissions and ownership settings.

Key Knowledge Areas:

*    File/directory permissions and owners
*    Terms and Utilities:
*    ls -l, ls -a
*    chmod, chown


#### Komanda **chmod**

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


# Using pipes:

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

```
ssh-keygen -t rsa
```



#### Adding users to sudo or admin group

```adduser username sudo```

```adduser username admin```





## Procesi

#### Izlistaj sve procese svih korisnika

```
ps -ef
```
e --> ispis svih procesa u sistemu
f --> ispis dodatnih podataka o procesima


ili

```
ps -aux
```

### izlistaj procese samo za sshd korisnika

```
ps -f -u sshd
```

### sortiraj procese po potrošnji memorije

```
ps aux --sort pmem
```

### sortoranje procesa po CPU potrošnji

```
ps aux --sort pcpu
```

### Slanje procesa i background

Da bi poslali komandu u backgroun, nakon komande dodamo znak `&` tj. znak ampersand.

U sljedecem primjeru zelimo da pingamo google svakih 5 sekundi sa komandom `ping -i 5 google.com`. Da bi je poslali u background, aa sami kraj komande dodajemo znak `&`.

```
ping -i 5 google.com &
```

Na ovaj nacin komanda ce biti izvrsavana u pozadini i svakih 5 sekundi ce nam ispisati rezultat na ekran, dok se rad u terminalu moze nastaviti.



* izlistamo procese u backgroundu

```
jobs
```

vratimo komandu u foreground

```
fg
```

```
jobs
[1]+  Running   "Komanda koju smo poslali u background"
```
Procesi su programi koji se izvršavaju. Programi su izvršene datoteke.
Prilikom pokretanja sistem svakom procesu dodjeljuje njegov broj (PID). Taj je broj jedinstven.


##### Procesima se mogu slati različiti signali, različitih značenja. Neki od signala su:

SIGHUP (1) - zahtjev za re-inicijalizacijom procesa
SIGKILL (9) - zahtjev za grubim prekidom izvršavanja
SIGTERM (15) - zahtjev za prekidom izvršavanja (softverski završetak rada)

Sintaksa:

```kill [-s SIGNAL] PROCES```


Naredbi ```kill``` se kao argument treba zadati PID procesa čije izvođenje želimo prekinuti ili redni broj koji je procesu dodijelila ljuska. Ako se navodi redni broj koji je procesu dodijelila ljuska tada ispred njega treba upisati znak % .

Ako se ne navede signal koji šaljemo, podrazumijeva se da se radi o signalu SIGTERM. Signale možemo zadati njihovim rednim brojem ili simboličkim imenom.

```$ kill -9 12345``` —>program prekidamo navodeći njegov PID

```$ kill-9 %2``` —> Program prekidamo dodjeljivanjem rednog broja bash-a

```
kill 1 --> broj procesa
```
#### Zapisivanje poruka u log datoteku

U proslom primjeru samo koristi komandu koja pinga `google.com` svakih 5 sekundi te nam ispisuje rezultate na `STDOUT` odnosno ekran. To je u odredjenim situacijama korisno jer korisnika informise u statusu izvrsavanja komande u pozadini, ali cesto samo ometa korisnika u radu.

U situacijama gdje ne zelimo da komanda ispisuje nepotrebne informacije na ekran koristimo redirekciju u fajl pomocu znaka `>`. To mozemo uraditi na sljedeci nacin.

* U ovom primjeru pingamo `google.com` svakih `5` sekundi te poruka koje salje komanda redirektujemo sa ekrana u fajl `/tmp/ping_google.log`, te na samom kraju stavljamo znak `&` cime zeljenu komandu saljemo u background.

````
ping -i 5 google.com > /tmp/ping_google.log &
````

Sada mozemo nastaviti sa radom a ako zelimo periodicno provjeriti stanje komande koristimo `tail` da bi procitali zapis u fajl `/tmp/ping_google.log`.

````
tail /tmp/ping_google.log
````

ili citanja u `real time` modu

````
tail -f /tmp/ping_google.log
````

Ako zelimo prekinuti `real time` citanje koristimo kombinaciju tipki `CTRL+C`.

<<<<<<< HEAD
## Koristenje jerkyll-a (Transform your plain text into static websites)
=======
#### SIGHUP i bacground procesi

Proces koji je poslan u background direktno je vezan za sessiju terminala prek kojeg je korisnik pokrenuo taj isti proces. Kada se korisnik odjavi tj. uradi logout svim background procesima ce biti poslan `SIGHUP` signal. Signal `SIGHUP` je skracenica za `signal hang up` i sluzi za terminiranje procesa.



Ako zelimo da background proces ostane u `running` stanju i da istom procesu ne bude poslan `SIGHUP` signal onda koristimo `nohup` komanu kao prefix.


* Sljedeci primjer koristimo ping komandu da pingamo udaljeni host `google.com` svakih `5` sekundi, te istu komandu saljemo u background. Pomocu `nohup` taj background proces nece biti ugasen nakon sto se korisnik koji je pokrenuo komandu odjavi sa terminala.

````
nohup ping -i 5 google.com &
````

### Koristenje jekyll-a (Transform your plain text into static websites)

* 1. Logovanje na server

* 2. Dodavanje novog korisnika
>>>>>>> 068c225cf6b671cb311d7d16b99e62dc050bcc86

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
````
i

```
gem update —system
```


* 6. Kao korisnik generisati novi kljuc

```
ssh-keygen -t rsa
```

* 7. generisani kljuc za korisnika dodati na github repo gdje je forkovan lugze blog

* 8. Instaliranje bundle-a
```
apt-get install bundle
```

* 9. Ponoviti postupak kloniranja datog repo-a i instalacije jekyll-a

```
git clone naziv git repoa
```
instalacije jekyll-a
```
gem install jekyll bundler
```

* 10. Pokretanje jekyll serve u backgroundu

```
bundle exec jekyll serve &
```

### Pronalazenje public ip adrese i komande ping/traceroute

`ping ime servera` - mjerenje odaziva nekog servera. Ovom komandom, pored drugih podataka, saznajemo public ip servera

`traceroute ime servera` - izlistavanje svih routea, servera koji se nalaze u hijerarhiji nekog servera

IP adresa - adresa servera

`0.0.0.0` - Obicno oznacava da host nije konfigurisan sa IP adrwsom (Ukoliko server ima 10 ip adresa, ovakvim navodom server ce slusati svih 10 tj. sve adrese)
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

* Zasto kao obicni korisnik moramo kucati punu putanju do `ifconfig` komande?

Komanda ifconfig se nalazi u direktoriju `/sbin` stoga moramo provjeriti da li se taj direktorij nalazi u `$PATH` shell varijabli. Korisniku su dostupni programi tj. komande koji se nalaze u pitanjama foldera koji su izlistani u `$PATH` shell varijabli.


 Kada smo logovani kao root korisnik to mozemo testirati na sljedeci nacin.

 ````
 whoami
root
 ````

 Izlistamo foldere iz `$PATH` varijable

 ````
 echo $PATH
 ````

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

| RFC1918 name | IP address range | number of addresses |
|-------------|----------------|--------------------|
| 24-bit block | 10.0.0.0-10.255.255.255 | 16,777,216 |
| 20-bit block | 172.16.0.0-172.31.255.255 | 1,048,576 |
| 16-bit block | 192.168.0.0 – 192.168.255.255 | 65,536 |

Izlistavanje server interfejska komandom:

```
ifconfig
```

* inet denotes IPv4 traffic
* inet6 denotes IPv6 traffic


### Predictable network interface device nameS


U zavisnost od tipa interfejsa imena imaju prefikse:

* 1. en for Ethernet,
* 2. wl for wireless LAN (WLAN),
* 3. for wireless wide area network (WWAN)


Imena imaju tipove:

````
o<index>

s<slot>[f<function>][d<dev_id>]
x<MAC>
[P<domain>]p<bus>s<slot>[f<function>][d<dev_id>]
[P<domain>]p<bus>s<slot>[f<function>][u<port>][..][c<config>][i<interface>]
````






# 5.4 Special Directories and Files

Description: Special directories and files on a Linux system including special permissions.

Key Knowledge Areas:

*    Using temporary files and directories
*    Symbolic links

**Terms and Utilities:**

*    /tmp/, /var/tmp/ and Sticky Bit
*    ls -d
*    ln -s



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


#### ***Vjezba***

Izbrisati prvi fajl. Da li je drugi fajl koji je simbolicki link izbrisan? Da li mozemo pomocu cat komande izlistati sadrzaj drugog fajla?



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


##### ***Vjezba***

Sta se desi ako izbrisemo drugi fajl, da li ce prvi fajl biti izbrisan?


```
rm fajl_drugi
```

# 6 Bash Script

##### List/info manual:
```$ man bash```

```man info```

##### List manual with number of lines:
```$ man bash | wc -l```

-First two character in script should be 
#! (shebeng)
#!/bin/bash

-Make scripts executambe with ```chmon u+x```, but i jou dont have permisions, you can run script with ```bash name_of_sript```
-If your directory dont contain script ```bash ./name_of_script.sh```

### Variables in bash:
-export command
-unset for remove variable
-echo $variable for value of variable

-export mynewvar or declare -x mynewvar
-export and ansigh in same time ```export var2="var2 value"```

Export functions
```export -f myfunction```

##### Bash startup:
-Check path ```pwd```
PATH=$PATH:/usr/local/bin


#### Working with aliases:
-Aliases are for commands
```alias ll="ls -ahl"```
```alias copy="cp"```

-List defined aliases with typed ```alias```

**unset** alias with commans ```unalias```

###Variables

####Typesets:
typeset -i x -> x must be integer
-let- allwos to convenient arithmetics: x++, x=x**2, x=x*3...

####Declare variables####

-if its string **-l** means all upercase, **-u*** lowercase and **-r** readonly
-declare with **-a MyArray** means myarray as indexed array

**exp.**

```#!/bin/bash
declare -l lstring="ABCdef"
declare -u ustring="ABCdef"
declare -r readonly="A Value"
declare -a Myarray
declare -A Myarray2

echo lstring=$lstring
echo ustring=$ustring
echo readonly=$readonly
readonly="New Value"
Myarray[2]="Second Value"
echo 'Myarray[2]= ' ${Myarray[2]}
Myarray2["soccer"]="beer"
echo 'Myarray2[soccer]= ' ${Myarray2["soccer"]} 
```


### The Read Command

#### While loop
```
#!/bin/bash
while 
  ((x<10))
do
  echo loop $x; date>date.$x
  ((x=x+1))
done
```

-While loop with pipeline and reading 3 line (c) from the list
```
#!/bin/bash

ls -l | while
  read a b c d
do
 echo owner $c
done
```


#### For loop
```
for <var> in <list>
do 
  command list
done
```
exp.
```
for animal in dog cat sheep
do
 echo animal is $animal
done
```
-seq command for sequence
```seq 1 9``` -> print sequence 1,2,3,4,5,6,7,8,9

```{A..Z} or {1..10} -> same but without seq```

Using seq in foorloop
```for i in `seq 1` ```

Loop per word from file
```for d in $(<data_file)```

Making a list a file globbing
```for j in *.c```

```for f in (find . -name *.c)``` -> loop, ind filename in current direstory with start extension with font c

#### Reading

-Read first and second line from data_file file
```
export a=first
export b=second
export c=third

echo a is '['$a']', b is '['$b']' and c is '[' $c']'
read a b <data_file
echo a is '['$a']', b is '['$b']' and c is '[' $c']'
```

-Read third column (owner) from ls command
```
#!/bin/bash

ls -l /etc | while
      read a b c d
do
      echo owner is $c
done
```

-Show number of lines from particular file
```nl my-file.sh```

#### Redirection and Pipes

0=>stdin (Standard in)
1=>stdout (Standard out)
2=>sterr (Standard error)

```command &> file``` -> gets stdout and stderr from command (file be created or overwritten)


```command | command2```
Commans2's stdin comes from command's stdout

-Open or close file descriptors

```exec N< myfile``` -> opens file descriptor N for reading from file myfile
```exec N> myfile```-> opens file descriptor N for writing from file myfile
```exec N<> myfile```-> opens file descriptor N for reading and writing from file myfile
```exec N>&-```-> close file descriptor N

#### Arithmetics operations

-use in (( )) or with *let*

### Bash Functions

```
function NAME {
  function body
}

function NAME {
  echo starting
  return
  
  this part of code will not be executed
}
```
### If/Else Statement


**exp**

```
if
grep -q important myfile
then
   echo myfile has importans stuff
else
   echo my file doesn’t have important stuff
fi
```

$? -> What is you status? 
If it’s 1,2 or 3 it’s an error, but if it’s 0 than program succefully xecuted

```		
if [ $? -eq 0 ]; then
  echo
  echo Program was successfully created, exiting program."
else
  echo "Failed, exitting."
```

Test - numeric Operators:
-eq -> ==
-lt -> <
-le -> <=
-ne -> &&

Some tests:

-succes if x is a directory
```test -d X```

-succes if x is regular file
```test -f X```

-succes if x is not empty and if exists
```test -s X```

-succes if x you have x permission on X file (same for w or r permission)
```test -x X```


### Filters and Paremeter Expansions
-Filters can be used with pipes

**head** - prints first n lines
**tail** - prints last n lines

exp:

```ls -l | head 5``` -> show first 5 lines form ls -l
```ls -l | tail 5``` -> show last 7 lines form ls -l

**wc**(word count) - prints line and words
```wc -l``` - prints number of lines

**awk** Breaks the line into the fields $1, $2

#### Positional strings

Script parameters

-To reference multidigital use {} eg. ${10}, or you have to name string as variable ${MojaVarijabla}

-${0} -> its path program to itself

-```shift``` command moves $1 to $2

```
#!/bin/bash

echo agr1 is $1 arg 11 is ${11}
shift
echo now arg1 is $1 arg 11 is ${11}
echo program is $0
```

###### Unset of null variables

```
${variable <OPR> value}
x=${var:-HAmburger}
```
-```:-``` if var unset or null, return value: otherwise return value of var
-```:=``` if var unset or null, var is assigned value and returned
-```:?``` Displays an error and exit script if var unset/null
-```:+``` if var unset or null, return nothing: otherwise return value

```
#!/bin/bash

unset x
a=${x:-Hotdog}
echo a is $a
echo x is $x

a=${x:=Hotdog}
echo a is $a
echo x is $x

unset x
${x:?}
echo Will not get here
```

###### String operations

```${var:offset}``` - value of var starting as offset
```${var:offset:len}``` - value of var starting at offset up to lenght len
```${#var}``` - lenght of var

prefix anf postfix are handy to processing filenames/paths
```${var#pre}``` - removing mathching prefix
```${var%post}``` - remove suffix


### Using coprocesses in bash

-Coprocess is background process where you can get file descriprion for the process's stdin and stdout and it implemented with pipe

### Debugging scripts

```$bash prog``` -> Run prog; don't need execute permission

```bash -x prog``` Echo commands after processing; can also do set -x or set +x  inside of script

```bash -n prog``` Do not execute commands, check for syntax error omly













