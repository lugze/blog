---
layout: page
title: Mala Škola Linuxa
permalink: /mala-skola-linuxa/
---

## Uobicajena organizacija foldera u Linuxu

* `/bin` - programi koje koriste i administratori i korisnici
* `/dev` - datoteke koje predstavljaju hardverske uredjaje (mrezna, graficka)  
* `/etc` - konfiguracijske datoteke
* `/home` - direktoriji korisnika
* `/sbin` - sistemski programi
* `/tmp` - privremene datoteke
* `/usr` - korisnicki programi, dokumentacija i biblioteke
* `/var` - sistemski zapisi i druge datoteke.

## Upravljanje korisnicima i grupama

Koricni imaju sopstveni `home` direktorij koji se nalazi u folderu `/home`. Izuzetak je `root` korisnik, ciji home direktorij se nalazi na lokaciji `/root`.

#### Vjezba: nekoliko nacina kako pristupiti home folderu

* koristiti `cd` komanu bez argumenata.

```
cd
```
* kao argument `cd` komandi proslijediti znak tildu tj. `~`

```
cd ~
```
* kao argument `cd` komandi proslijediti build in shell varijablu `$HOME`

```
cd $HOME
```
### `finger` komanda

Komanda `finger` ispisuje informacije o korisniku. Kao argument komandi proslijedimo korisnicko ime tj `username` korisnika. U sljedecem primjeru `finger` ce prikazati informacije o korisniku `root`.

```
finger root
```

kao odgovor dobijamo sljedece informacije

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

Ukoliko dobijete gresku `-bash: finger: command not found` potrebno je da instalirate komandu sa na sljedeci nacin

```
apt-get update
apt-get install finger
```

### Komanda `id`

Ova komanda nam daje informacije o korisniku kao sto su

* `id` broj korisnika
* `gid` ili group id tj. broj primarne grupe kojoj korinsik pripada
* `groups` kompletna lista grupa kojoj korisnik pripada, tj gid i naziv grupe.


## Rad sa fajlovima i direktorijima

File ili direktorij sa space Moj File se pise kao ```Moj\ file```

#### Ispis sadrzaja direktorija

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

Ispisi listu fajlova i direktorija unutar trenutnog direktorija, te sadrzaj direktorija koji se nalaze u tekucem direktoriju

```
ls -al *
```


Ispisi listu fajlova i direktorija unutar trenutnog direktorija na nacin da i direktorije tretiramo kao obicne fajlove te ne ispisujemo njihov sadrzaja

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


*****************
*****************

### Kreiranje simboličkih linkova

prvo napravimo fajl

```
touch fajl_jedan
```


zapisemo nesto u fajl pomocu redirekcije

```
echo "NEKI TESTNI SADRZAJ">fajl_jedan
```


provjerimo da li je zapisano u fajl

```
cat fajl_jedan
```

napravimo simbolicki link na novi fajl

```
ln -s fajl_jedan fajl_dva_koji_je_simbolicki_link_na_prvi_fajl
```

ispisemo sadrzaj drugog fajla koji je simbolicki link

```
cat fajl_dva_koji_je_simbolicki_link_na_prvi_fajl
```

mozemo primjetiti da je sadrzaj oba fajla isti

provjerimo inodove oba fajla

```
ls -i fajl_jedan
ls -i fajl_dva_koji_je_simbolicki_link_na_prvi_fajl
```

mozemo promjetiti da su inode brojevi razliciti sto znaci da su razliciti fajlove te ako jedan izbrisemo to znaci da drugi fajl nece biti izbrisan


Vjezba: izbrisati prvi fajl. Da li je drugi fajl koji je simbolicki link izbrisan? Da li mozemo pomocu cat komande izlistati sadrzaj drugog fajla?



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

```
ls -i fajl_drugi
6257560 fajl_drugi
```


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

```sudo chown korinik test.sh``` -> prebacujem prava filea na usera emin


Using pipes:

```echo “hello” | wc``` -> 1  1  16  one line, one word and 6 characters


Cat - Concatenate(stick two or more things together) and print files

```cat dugiTekst.txt``` -> izlistavamo cijeli tekst

```head dugiTekst.txt``` -> prvih 10 linija

```tail dugiTekst.txt``` -> zadnjih 10 linija

# Ispisi zadnjih 5 linija pomocu tail komande

```
tail -n 5 dugiTekst.txt
```

```
cat dugiText | cat -n | tail -n 5
```
 -> kombinacija

```
less dugiText
```
 -> izlistavanje

### Grep - Search files for text that matches a given pattern



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


*******************
<<<<<<< HEAD
Archive komande

```tar -cvf (c-create, v-verbot, f-output to file) myfile.tar Vjezba\ Files/```



## Procesi

# Izlistaj sve procese svih korisnika

```
ps -ef
```

ili

```
ps -aux
```

# izlistaj procese samo za sshd korisnika

```
ps -f -u sshd
```

# sortirajprocese po potrosnji memorije

```
ps aux --sort pmem
```

# sortoranje  procesa po CPU potrosnji

```
ps aux --sort pcpu
```

### Slanje procesa i background

Ispisivanje svih procesa:

```
ps
```
-e --> ispis svih procesa u sistemu
-f-->  ispis dodatnih podataka o procesima


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
