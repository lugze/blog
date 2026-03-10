---
layout: page
title: Mala Škola Linux-a
permalink: /mala-skola-linuxa/
---

Verzija dokumenta 0.0.4

## Uobičajena organizacija foldera u Linuxu

* `/bin`  - osnovni programi koje koriste i administratori i korisnici (npr. `ls`, `cp`, `cat`)
* `/boot` - kernel i fajlovi potrebni za pokretanje sistema (bootloader)
* `/dev`  - specijalne datoteke koje predstavljaju hardverske uređaje (diskovi, terminali, `/dev/null`)
* `/etc`  - konfiguracijske datoteke sistema i servisa
* `/home` - korisnički direktoriji (svaki korisnik ima svoj podfolder)
* `/lib`  - dijeljene biblioteke potrebne programima iz `/bin` i `/sbin`
* `/media`- automatski mount-ovani uređaji (USB, CD/DVD)
* `/mnt`  - privremeni mount point za ručno montiranje filesystem-a
* `/opt`  - opcioni softver koji nije dio distribucije (third-party aplikacije)
* `/proc` - virtuelni filesystem sa informacijama o pokrenutim procesima i kernelu
* `/root` - home direktorij root korisnika
* `/run`  - runtime podaci od pokretanja sistema (PID fajlovi, socketi)
* `/sbin` - sistemski programi za administraciju (npr. `fdisk`, `iptables`, `reboot`)
* `/sys`  - virtuelni filesystem sa informacijama o hardveru i kernel modulima
* `/tmp`  - privremene datoteke (na većini distribucija se brišu pri restartu ili periodično)
* `/usr`  - sekundarna hijerarhija: korisnički programi (`/usr/bin`), biblioteke (`/usr/lib`), dokumentacija (`/usr/share`)
* `/var`  - promjenjivi podaci: logovi (`/var/log`), mail (`/var/mail`), cache (`/var/cache`)

**Napomena:** Na modernim distribucijama (Fedora 17+, Debian 12+, Ubuntu 22.04+) direktoriji `/bin`, `/sbin` i `/lib` su simbolički linkovi na `/usr/bin`, `/usr/sbin` i `/usr/lib` (tzv. usr merge).

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

**Napomena:** `finger` je zastarjela komanda i nije instalirana po defaultu na većini modernih distribucija. Alternativa je komanda `pinky` (dio GNU coreutils, prikazuje slične ali ograničenije informacije) ili kombinacija `id` i `getent passwd korisnik`.

Komanda `finger` ispisuje informacije o korisniku. Kao argument komandi proslijedimo korisničko ime. U sljedećem primjeru `finger` će prikazati informacije o korisniku `root`:

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

Ukoliko dobijete grešku `-bash: finger: command not found` potrebno je da instalirate paket:

```
sudo apt-get update
sudo apt-get install finger
```

### Komanda `id`

Ova komanda nam daje informacije o korisniku kao što su:

* `uid`    - user ID (jedinstven broj korisnika)
* `gid`    - group ID (broj primarne grupe kojoj korisnik pripada)
* `groups` - kompletna lista grupa kojoj korisnik pripada

Kada komandi `id` ne proslijedimo argument, prikazuje informacije o trenutnom korisniku:

```
id
uid=0(root) gid=0(root) groups=0(root)
```

Kada proslijedimo korisničko ime, dobijemo info o tom korisniku:

```
id korisnik
uid=1001(korisnik) gid=1001(korisnik) groups=1001(korisnik),27(sudo)
```

Korisni parametri:

* `-u` — samo uid: `id -u root` → `0`
* `-g` — samo primarni gid: `id -g korisnik` → `1001`
* `-G` — svi gid-ovi: `id -G korisnik` → `1001 27`
* `-n` — prikaži ime umjesto broja (koristi se uz `-u`, `-g` ili `-G`): `id -Gn korisnik` → `korisnik sudo`

### Komande `adduser` i `usermod`

Dodavanje novog korisnika (interaktivno postavlja šifru i podatke):

```
sudo adduser korisnik
```

Dodavanje korisnika u grupu `sudo` (za administratorski pristup):

```
sudo adduser korisnik sudo
```

Alternativno, koristeći `usermod`:

```
sudo usermod -aG sudo korisnik
```

**Oprez:** Opcija `-a` (append) je **obavezna** uz `-G`. Bez `-a`, korisnik će biti **uklonjen** iz svih grupa osim navedene.

Brisanje korisnika:

```
sudo deluser korisnik
```

Brisanje korisnika zajedno sa home direktorijem:

```
sudo deluser --remove-home korisnik
```

Promjena šifre:

```
passwd              # mijenja šifru trenutnog korisnika
sudo passwd korisnik # mijenja šifru drugog korisnika
```

## Rad sa fajlovima i direktorijima

File ili direktorij sa razmakom u imenu, npr. `Moj File`, piše se kao `Moj\ File` ili se stavlja pod navodnike: `"Moj File"`.

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

Ispiši sve fajlove uključujući skrivene (čije ime počinje sa tačkom `.`):

```
ls -al .
```

Ispiši sadržaj trenutnog direktorija i sadržaj svih poddirektorija:

```
ls -al *
```

Ispiši fajlove i direktorije, ali direktorije tretiramo kao obične fajlove (ne ispisujemo njihov sadržaj — opcija `-d`):

```
ls -ald *
```

Ispiši samo skrivene fajlove i direktorije:

```
ls -ald .*
```

### Ispis inode broja fajla

Inode je jedinstven identifikator fajla na filesystem-u. Svaki fajl i direktorij ima svoj inode broj koji sadrži metadata (dozvole, vlasnik, veličinu, lokaciju na disku).

```
ls -i ime_fajla
```

### Kreiranje simboličkih linkova (symlink)

Simbolički link je poseban fajl koji sadrži putanju do drugog fajla. Ako se originalni fajl obriše, symlink postaje "broken" (mrtav link). Symlink može pokazivati na fajlove na drugim particijama i na direktorije.

Prvo napravimo fajl:

```
touch fajl_jedan
```

Zapišemo nešto u fajl pomoću redirekcije:

```
echo "NEKI TESTNI SADRZAJ" > fajl_jedan
```

Provjerimo da li je zapisano:

```
cat fajl_jedan
```

Napravimo simbolički link:

```
ln -s fajl_jedan fajl_link
```

**Sintaksa:** `ln -s CILJ IME_LINKA` — prvo ide originalni fajl (cilj), pa ime linka.

Ispišemo sadržaj linka:

```
cat fajl_link
```

Sadržaj je isti kao kod originalnog fajla.

Provjerimo inode-ove oba fajla:

```
ls -li fajl_jedan fajl_link
```

Inode brojevi su **različiti** — symlink je zaseban fajl. U `ls -l` ispisu, symlink je označen sa `l` na početku i prikazuje `->` na cilj:

```
lrwxrwxrwx 1 korisnik korisnik 10 mar 10 12:00 fajl_link -> fajl_jedan
```

#### Vježba

Izbrisati originalni fajl (`rm fajl_jedan`). Da li `cat fajl_link` i dalje radi?

(Odgovor: ne — symlink pokazuje na nepostojući fajl i dobijamo grešku `No such file or directory`.)

### Hard linkovi

Hard link je dodatno ime za isti fajl na disku. Za razliku od symlink-a, hard link dijeli isti inode sa originalom — oba imena su ravnopravna. Fajl se briše sa diska tek kada se uklone **svi** hard linkovi na njega (inode reference count padne na 0).

Kreirati fajl i dodati sadržaj:

```
touch fajl_prvi
echo "NEKI TESTNI SADRZAJ" > fajl_prvi
```

Napraviti hard link:

```
ln fajl_prvi fajl_drugi
```

Provjeriti inode brojeve:

```
ls -li fajl_prvi fajl_drugi
6257560 -rw-r--r-- 2 korisnik korisnik 20 mar 10 12:00 fajl_drugi
6257560 -rw-r--r-- 2 korisnik korisnik 20 mar 10 12:00 fajl_prvi
```

Inode brojevi su **isti**, a broj `2` u trećoj koloni označava da postoje 2 hard linka na taj inode.

**Ograničenja hard linkova:**
* Ne mogu se kreirati na direktorije (osim `.` i `..` koje kreira sam filesystem)
* Ne mogu se kreirati između različitih filesystem-a (particija)

#### Vježba

Šta se desi ako izbrišemo `fajl_drugi`? Da li će `fajl_prvi` biti izbrisan?

```
rm fajl_drugi
cat fajl_prvi
```

(Odgovor: `fajl_prvi` i dalje postoji jer je to samo jedno ime manje za isti inode. Link count pada sa 2 na 1.)

### Rekurzivno listanje sadržaja foldera

```
ls -R IME_FOLDERA/
```

Ispisuje cijelu strukturu foldera rekurzivno.

**Alternativa:** Za pregledniji prikaz stabla direktorija:

```
tree IME_FOLDERA/
tree -L 2 IME_FOLDERA/  # ograniči dubinu na 2 nivoa
```

(`tree` se instalira sa `sudo apt-get install tree`)

### Pomoć o komandama

Kratka pomoć:

```
ls --help
```

Detaljni manual:

```
man ls
```

Navigacija u `man`: `f` ili `Space` (naprijed), `b` (nazad), `/tekst` (pretraga), `n` (sljedeći rezultat), `q` (izlaz).

Kratki opis komande:

```
whatis ls
```

Pretraga man stranica po opisu:

```
apropos "copy files"
```

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

Ulazak u folder dva nivoa iznad:

```
cd ../../NEKI_FOLDER
```

Vraćanje na prethodni direktorij:

```
cd -
```

Apsolutna vs. relativna putanja:

* Apsolutna — počinje od root-a (`/`): `/home/korisnik/dokumenti`
* Relativna — od trenutnog direktorija: `dokumenti/projekat` ili `../dokumenti`

### Putanje do programa

Koristimo komande `which` i `whereis` da saznamo putanju programa:

* `which` — prikazuje putanju do izvršnog fajla koji bi shell pokrenuo (pretražuje samo `$PATH`)
* `whereis` — prikazuje putanju do izvršnog fajla, source koda i man stranica (pretražuje standardne lokacije, ne samo `$PATH`)

```
which nano
/usr/bin/nano
```

```
whereis nano
nano: /usr/bin/nano /usr/share/nano /usr/share/man/man1/nano.1.gz
```

Za pronalaženje svih instanci programa u `$PATH`:

```
which -a python3
```

### Vježba: praćenje pwd vrijednosti

Pratiti kako se mijenja `pwd` vrijednost nakon svake izmjene trenutnog direktorija:

```
cd ~
pwd
echo $PWD
```

```
cd /tmp
pwd
echo $PWD
```

```
cd $HOME
pwd
echo $PWD
```

### Kreiranje direktorija

`mkdir` - pravljenje foldera:

```
mkdir novi_folder
```

Bez `-p` opcije, `mkdir` će javiti grešku ako parent direktorij ne postoji:

```
mkdir folder/subfolder/subsubfolder
# mkdir: cannot create directory 'folder/subfolder/subsubfolder': No such file or directory
```

`mkdir -p` kreira cijelu putanju uključujući parent direktorije koji ne postoje:

```
mkdir -p folder/subfolder/subsubfolder
```

Brisanje praznog direktorija:

```
rmdir prazan_folder
```

### Kreiranje, kopiranje i premještanje fajlova

Pravljenje praznog fajla (ili ažuriranje timestamp-a ako fajl već postoji):

```
touch mojFile.txt
```

Kopiranje fajla:

```
cp mojFile.txt mojNoviFile.txt
```

Rekurzivno kopiranje direktorija:

```
cp -r izvorni_folder/ odredisni_folder/
```

Kopiranje uz očuvanje dozvola, vlasništva i timestamp-a:

```
cp -a izvorni_folder/ odredisni_folder/
```

Premještanje fajlova (može se koristiti i za preimenovanje):

```
mv novi_file.txt najbolji_folder/
```

```
mv staro_ime.txt novo_ime.txt
```

Pomjeri sve `.txt` fajlove iz `najbolji_folder` u trenutni folder:

```
mv najbolji_folder/*.txt .
```

### Wildcards (džoker znakovi)

Shell expandira wildcard znakove prije nego proslijedi argumente komandi:

* `*` - bilo koji broj znakova (uključujući nijedan)
* `?` - tačno jedan znak
* `[abc]` - jedan od navedenih znakova
* `[0-9]` - raspon znakova
* `[!abc]` ili `[^abc]` - bilo koji znak osim navedenih

Primjeri:

```
ls *.txt           # svi .txt fajlovi
ls dokument?.pdf   # dokument1.pdf, dokumentA.pdf, itd.
ls slika[1-3].jpg  # slika1.jpg, slika2.jpg, slika3.jpg
ls fajl[!0-9].txt  # fajlovi čiji znak nakon "fajl" nije cifra
```

### Brisanje fajlova

```
rm novi_file.txt
```

Brisanje sa wildcard-om:

```
rm noviji_file?.txt
```

Rekurzivno brisanje direktorija i sadržaja:

```
rm -r ime_foldera
```

**Oprez:** `rm` trajno briše fajlove — nema "korpe za smeće". Koristite `-i` opciju za potvrdu prije brisanja:

```
rm -ri ime_foldera
```

### Pretraga fajlova

Komanda `find` rekurzivno pretražuje direktorije:

```
find . -name "naziv"
find . -name "naziv*"
```

Case-insensitive pretraga:

```
find . -iname "naziv*"
```

Pretraga samo za fajlovima (ne direktorijima):

```
find . -type f
```

Pretraga samo za direktorijima:

```
find . -type d
```

Pretraga po veličini:

```
find . -type f -size +100M    # veći od 100MB
find . -type f -size -1k      # manji od 1KB
```

Pretraga po vremenu izmjene:

```
find . -type f -mtime -7      # mijenjani u zadnjih 7 dana
find . -type f -mtime +30     # stariji od 30 dana
```

Pronađi i izvrši komandu nad rezultatima:

```
find . -name "*.log" -delete                     # obriši sve .log fajlove
find . -name "*.txt" -exec grep -l "trazeni" {} \;  # pretraži sadržaj pronađenih fajlova
```

### Prompt znakovi

* `$` - nalazimo se kao obični korisnik
* `#` - nalazimo se kao root

### Promjena korisnika i root pristup

Prelazak na root korisnika (traži root šifru):

```
su -
```

**Napomena:** Na Ubuntu-u je root nalog zaključan po defaultu. Umjesto `su` koristi se `sudo`:

```
sudo komanda          # pokreni jednu komandu kao root
sudo -i               # otvori root shell (interaktivni login)
sudo su -             # alternativa za root shell
```

Logovanje kao drugi korisnik (login shell — učitava kompletno okruženje korisnika):

```
su - korisnik
```

**Napomena:** `su - korisnik` i `su -l korisnik` su ekvivalentni — crtca `-` je skraćenica za `-l` (login). Bez crtice, `su korisnik` ne učitava korisnikov `.bashrc` i `.profile`, te zadržava `$PATH` i druge varijable prethodnog korisnika.

## Upravljanje paketima (Debian/Ubuntu)

Ažuriranje liste paketa:

```
sudo apt update
```

Nadogradnja instaliranih paketa:

```
sudo apt upgrade
```

Instalacija novog paketa:

```
sudo apt install ime_paketa
```

Deinstalacija paketa:

```
sudo apt remove ime_paketa
```

Deinstalacija zajedno sa konfiguracijskim fajlovima:

```
sudo apt purge ime_paketa
```

Pretraga paketa:

```
apt search ključna_riječ
```

Informacije o paketu:

```
apt show ime_paketa
```

Čišćenje cache-a preuzetih paketa:

```
sudo apt autoremove
sudo apt clean
```

**Napomena:** `apt` je modernija zamjena za `apt-get` i `apt-cache` sa jednostavnijim interfejsom. Za skripte se i dalje preporučuje `apt-get` jer ima stabilniji izlaz.

## Upravljanje servisima (systemd)

Većina modernih distribucija koristi `systemd` za upravljanje servisima.

Provjera statusa servisa:

```
sudo systemctl status nginx
```

Pokretanje / zaustavljanje / restart servisa:

```
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl restart nginx
```

Omogućavanje servisa da se automatski pokrene pri startu sistema:

```
sudo systemctl enable nginx
```

Onemogućavanje automatskog pokretanja:

```
sudo systemctl disable nginx
```

Pregled svih aktivnih servisa:

```
systemctl list-units --type=service --state=running
```

Pregled logova za servis:

```
journalctl -u nginx              # svi logovi
journalctl -u nginx --since today # samo danas
journalctl -u nginx -f            # praćenje u realnom vremenu
```

### Dozvole nad fajlovima

`chmod` - mijenja dozvole nad fajlom.

Oktalne dozvole — tri cifre za vlasnika (user), grupu (group) i ostale (others). Svaka cifra je zbir:

```
Read = 4, Write = 2, Execute = 1
```

Primjer: `chmod 754` znači vlasnik=7 (4+2+1=rwx), grupa=5 (4+0+1=r-x), ostali=4 (4+0+0=r--).

Uobičajene oktalne dozvole:

| Oktalna | Simbolička | Tipična upotreba |
|---|---|---|
| `755` | `rwxr-xr-x` | Izvršni programi i direktoriji |
| `644` | `rw-r--r--` | Obični fajlovi (tekst, konfiguracija) |
| `700` | `rwx------` | Privatni direktoriji |
| `600` | `rw-------` | Privatni fajlovi (SSH ključevi, šifre) |
| `775` | `rwxrwxr-x` | Dijeljeni direktoriji unutar grupe |
| `664` | `rw-rw-r--` | Dijeljeni fajlovi unutar grupe |

Simboličke oznake:

* `+` dodaje dozvolu
* `-` uklanja dozvolu
* `=` postavlja tačno navedene dozvole (uklanja ostale)

Ciljevi:

* `u` - user (vlasnik)
* `g` - group (grupa)
* `o` - others (ostali)
* `a` - all (svi, isto kao `ugo`)

Primjeri:

```
chmod u-r test.sh       # ukloni read za vlasnika
chmod a+x skripta.sh    # dodaj execute za sve
chmod go-w fajl.txt     # ukloni write za grupu i ostale
chmod u=rwx,go=rx dir/  # vlasnik: rwx, grupa i ostali: r-x
chmod 644 test.sh       # oktalno: rw-r--r--
```

### Vlasništvo nad fajlovima

`chown` - mijenja vlasnika i/ili grupu fajla.

```
sudo chown korisnik fajl.txt            # promijeni vlasnika
sudo chown korisnik:grupa fajl.txt      # promijeni vlasnika i grupu
sudo chown :grupa fajl.txt              # promijeni samo grupu
sudo chown -R korisnik:grupa direktorij/ # rekurzivno za direktorij
```

`chgrp` - mijenja samo grupu:

```
sudo chgrp grupa fajl.txt
```

### Korištenje pipe-ova

Pipe (`|`) prosljeđuje standardni izlaz (stdout) jedne komande kao standardni ulaz (stdin) drugoj:

```
echo "hello" | wc
      1       1       6
```

Rezultat: 1 linija, 1 riječ, 6 bajtova (5 znakova + newline karakter).

Više pipe-ova u nizu:

```
cat /var/log/syslog | grep "error" | wc -l
```

Ovo broji koliko linija u syslogu sadrži riječ "error".

### Redirekcija

* `>` - preusmjeri stdout u fajl (prepiše sadržaj)
* `>>` - dodaj stdout na kraj fajla (append)
* `2>` - preusmjeri stderr (greške) u fajl
* `2>&1` - preusmjeri stderr na stdout
* `<` - učitaj stdin iz fajla

```
echo "tekst" > fajl.txt       # prepiše fajl
echo "tekst" >> fajl.txt      # dodaje na kraj
komanda > output.txt 2>&1     # i izlaz i greške u isti fajl
komanda > /dev/null 2>&1      # potpuno utiša izlaz i greške
sort < lista.txt              # sort čita iz fajla umjesto tastature
```

### Čitanje sadržaja fajlova

`cat` - ispisuje cijeli sadržaj fajla (za kraće fajlove):

```
cat dugiTekst.txt
```

Ispis sa brojevima linija:

```
cat -n dugiTekst.txt
```

`head` - ispisuje prvih 10 linija (po defaultu):

```
head dugiTekst.txt
head -n 20 dugiTekst.txt    # prvih 20 linija
```

`tail` - ispisuje zadnjih 10 linija (po defaultu):

```
tail dugiTekst.txt
tail -n 5 dugiTekst.txt     # zadnjih 5 linija
```

Praćenje fajla u realnom vremenu (korisno za logove):

```
tail -f /var/log/syslog
```

**Savjet:** Koristite `Ctrl+C` za prekid `tail -f`.

Kombinacija komandi sa pipe-om — ispiši zadnjih 5 linija sa brojevima:

```
cat -n dugiTekst.txt | tail -n 5
```

`less` - interaktivno pregledavanje dugačkih fajlova (ne učitava cijeli fajl u memoriju):

```
less dugiTekst.txt
```

Navigacija u `less`: `f`/`Space` (naprijed), `b` (nazad), `/tekst` (pretraga), `n` (sljedeći rezultat), `N` (prethodni rezultat), `g` (početak), `G` (kraj), `q` (izlaz).

### Obrada teksta

`wc` - brojanje linija, riječi i bajtova:

```
wc fajl.txt           # linije, riječi, bajtovi
wc -l fajl.txt        # samo broj linija
```

`sort` - sortiranje linija:

```
sort fajl.txt            # abecedno
sort -n fajl.txt         # numerički
sort -r fajl.txt         # obrnuti redoslijed
sort -u fajl.txt         # sortiraj i ukloni duplikate
```

`uniq` - uklanja uzastopne duplikate (obično se koristi sa `sort`):

```
sort fajl.txt | uniq       # ukloni duplikate
sort fajl.txt | uniq -c    # prikaži koliko puta se svaka linija ponavlja
```

`cut` - izdvajanje kolona/polja:

```
cut -d: -f1 /etc/passwd       # izdvoji prvo polje (korisničko ime), delimiter je :
cut -d, -f2,3 podaci.csv      # izdvoji 2. i 3. kolonu iz CSV
```

`diff` - poređenje dva fajla:

```
diff fajl1.txt fajl2.txt
```

### Grep - pretraga teksta u fajlovima

Osnovna pretraga:

```
grep "text" file.txt
```

Korisne opcije:

```
grep -i "text" file.txt        # ignoriši velika/mala slova
grep -r "text" /putanja/       # rekurzivna pretraga
grep -n "text" file.txt        # prikaži brojeve linija
grep -v "text" file.txt        # linije koje NE sadrže tekst
grep -c "text" file.txt        # samo broj pogodaka
grep -l "text" *.txt           # samo imena fajlova koji sadrže tekst
grep -w "text" file.txt        # traži cijelu riječ (ne djelimični match)
```

Kombinacija — rekurzivno pretraži, prikaži brojeve linija, ignoriši velika/mala slova:

```
grep -rni "error" /var/log/
```

Pretraga sa regularnim izrazima (extended regex):

```
grep -E "error|warning|critical" /var/log/syslog
```

### Korisne komande

* `.`  - oznaka za trenutni direktorij
* `..` - oznaka za parent direktorij
* `printenv` - ispis svih environment varijabli
* `env` - ispis environment varijabli (slično `printenv`)
* `pwd` - print working directory
* `whoami` - ime trenutnog korisnika
* `hostname` - ime računara
* `date` - trenutni datum i vrijeme
* `uptime` - koliko dugo sistem radi, broj korisnika, load average
* `df -h` - slobodan prostor na diskovima
* `du -sh direktorij/` - veličina direktorija
* `free -h` - korištenje memorije (RAM i swap)
* `uname -a` - informacije o kernelu i sistemu
* `lsb_release -a` - informacije o distribuciji

### Aliasi

Alias je skraćenica za komandu ili niz komandi:

```
alias ll='ls -alh'
alias gs='git status'
alias update='sudo apt update && sudo apt upgrade'
```

Za trajne aliase, dodati ih u `~/.bashrc`:

```
echo "alias ll='ls -alh'" >> ~/.bashrc
source ~/.bashrc    # učitaj izmjene bez ponovnog logovanja
```

Pregled svih aktivnih aliasa:

```
alias
```

### Generisanje SSH ključa

Preporučeni algoritam za nove ključeve je Ed25519:

```
ssh-keygen -t ed25519 -C "email@primjer.com"
```

Alternativno, RSA (minimalno 2048 bita, preporučeno 4096):

```
ssh-keygen -t rsa -b 4096
```

Kopiranje javnog ključa na udaljeni server:

```
ssh-copy-id korisnik@server
```

Povezivanje na udaljeni server:

```
ssh korisnik@server
```

Kopiranje fajlova na/sa udaljenog servera:

```
scp fajl.txt korisnik@server:/putanja/     # upload
scp korisnik@server:/putanja/fajl.txt .    # download
scp -r folder/ korisnik@server:/putanja/   # rekurzivno
```

### Archive komande

Kreiranje tar arhive:

```
tar -cvf myfile.tar Vjezba_Files/
```

Opcije: `c` - create, `v` - verbose, `f` - output to file.

Kreiranje kompresovane arhive (gzip):

```
tar -czvf myfile.tar.gz Vjezba_Files/
```

Ekstrakcija arhive:

```
tar -xvf myfile.tar
tar -xzvf myfile.tar.gz
```

Ekstrakcija u određeni direktorij:

```
tar -xzvf myfile.tar.gz -C /odredisni/direktorij/
```

Pregled sadržaja arhive bez ekstrakcije:

```
tar -tvf myfile.tar
```

Kompresija/dekompresija pojedinačnih fajlova:

```
gzip fajl.txt         # kompresuje u fajl.txt.gz (briše original)
gunzip fajl.txt.gz    # dekompresuje (briše .gz)
gzip -k fajl.txt      # kompresuje ali zadržava original
```

## Procesi

Izlistaj sve procese svih korisnika:

```
ps -ef
```

* `-e` - ispis svih procesa u sistemu
* `-f` - full format (prikazuje UID, PID, PPID, CMD i druge kolone)

Ili u BSD formatu:

```
ps aux
```

* `a` - procesi svih korisnika vezani za terminal (kombinovano sa `x` prikazuje sve)
* `u` - korisnički format (prikazuje %CPU, %MEM, VSZ, RSS)
* `x` - uključuje procese bez kontrolnog terminala (daemone)

Izlistaj procese za određenog korisnika:

```
ps -f -u sshd
```

Sortiraj procese po potrošnji memorije (opadajuće):

```
ps aux --sort=-%mem
```

Sortiranje po CPU potrošnji (opadajuće):

```
ps aux --sort=-%cpu
```

**Napomena:** Prefiks `-` znači opadajući redoslijed. Bez njega se sortira uzlazno.

Interaktivni pregled procesa u realnom vremenu:

```
top
```

Korisne tipke u `top`: `q` (izlaz), `M` (sortiraj po memoriji), `P` (sortiraj po CPU), `k` (kill proces).

Modernija alternativa sa boljim interfejsom:

```
htop
```

(`htop` se instalira sa `sudo apt install htop`)

### Slanje procesa u background

Nakon komande dodamo znak `&`:

```
sleep 60 &
```

**Napomena:** Interaktivne komande (poput `nano`, `vim`) zahtijevaju pristup terminalu i biće odmah pauzirane ako se pošalju u background.

Izlistamo background procese:

```
jobs
```

Vratimo proces u foreground:

```
fg %1
```

Pauziranje trenutnog procesa i slanje u background: pritisnemo `Ctrl+Z` (pauzira), zatim:

```
bg %1
```

### Upravljanje procesima

Izlistavanje background procesa:

```
jobs
[1]+  Running   sleep 60 &
```

Zaustavljanje procesa po job broju:

```
kill %1
```

Zaustavljanje procesa po PID-u:

```
kill 12345
```

Prisilno zaustavljanje procesa koji ne reaguje na SIGTERM:

```
kill -9 12345
```

**Oprez:** `kill -9` (SIGKILL) ne daje procesu priliku da zatvori fajlove ili oslobodi resurse. Koristite samo ako obični `kill` (SIGTERM, signal 15) ne uspije.

Pronalaženje PID-a po imenu procesa:

```
pgrep -a ime_procesa
```

Zaustavljanje svih procesa po imenu:

```
pkill ime_procesa
```

## Mreža

### Pronalaženje IP adrese

Moderna komanda za pregled mrežnih interfejsa:

```
ip addr show
```

Ili skraćeno:

```
ip a
```

Prikaz samo IPv4 adresa:

```
ip -4 addr
```

**Zastarjela alternativa** (dio paketa `net-tools`, nije instalirana po defaultu na novijim sistemima):

```
ifconfig
```

Za pregled mrežnih konekcija i otvorenih portova:

```
ss -tulnp
```

* `-t` TCP, `-u` UDP, `-l` listening, `-n` numerički, `-p` prikaži proces

**Zastarjela alternativa:** `netstat -tulnp` (također dio `net-tools`).

### Komande ping i traceroute

`ping` - mjerenje odaziva nekog servera:

```
ping -c 4 ime_servera
```

**Napomena:** Na Linuxu `ping` bez `-c` opcije radi beskonačno. Prekida se sa `Ctrl+C`.

`traceroute` - izlistavanje svih čvorova na putu do nekog servera:

```
traceroute ime_servera
```

DNS pretraga:

```
dig ime_servera
nslookup ime_servera
```

Preuzimanje sadržaja sa URL-a:

```
curl -O https://primjer.com/fajl.zip    # preuzmi fajl
wget https://primjer.com/fajl.zip       # alternativa
curl -I https://primjer.com             # samo HTTP zaglavlja
```

### Posebne IP adrese

* `0.0.0.0` - označava "sve interfejse". Kada server sluša na `0.0.0.0`, prihvata konekcije na svim mrežnim interfejsima
* `127.0.0.1` - loopback adresa (localhost), dostupna samo lokalno
* `::1` - IPv6 loopback adresa (ekvivalent `127.0.0.1`)

### Zašto kao obični korisnik moramo kucati punu putanju do `ifconfig` komande?

**Napomena:** Ovo se odnosi na starije distribucije (Debian 10 i ranije, Ubuntu 18.04 i ranije). Na modernim sistemima `/sbin` je uključen u `$PATH` svih korisnika.

Komanda `ifconfig` se nalazi u direktoriju `/sbin`. Korisniku su dostupni samo programi koji se nalaze u putanjama izlistanim u `$PATH` shell varijabli.

Kada smo logovani kao root korisnik, provjerimo `$PATH`:

```
whoami
root
```

```
echo $PATH | tr ':' '\n' | grep sbin
/usr/local/sbin
/usr/sbin
/sbin
```

Root ima `/sbin` u svom `$PATH`.

Logujemo se kao neprivilegovani korisnik:

```
su - emin
```

```
whoami
emin
```

Provjerimo `$PATH`:

```
echo $PATH | tr ':' '\n' | grep sbin
```

Prazan odgovor — `/sbin` nije u `$PATH`. Zato dobijamo grešku `ifconfig: command not found`.

Privremeno rješenje — dodamo `/sbin` u `$PATH`:

```
export PATH=$PATH:/sbin
```

Sada `ifconfig` radi bez pune putanje.

**Napomena:** Ova izmjena važi samo za trenutnu sesiju. Za trajnu promjenu, dodajte u `~/.bashrc`:

```
echo 'export PATH=$PATH:/sbin' >> ~/.bashrc
```

### Prepoznavanje privatnih IP adresa

Privatni IPv4 adresni prostori (RFC 1918):

| CIDR notacija | IP adresni raspon | Broj adresa | Uobičajena upotreba |
|---|---|---|---|
| 10.0.0.0/8 | 10.0.0.0 – 10.255.255.255 | 16,777,216 | Velike korporativne mreže, cloud |
| 172.16.0.0/12 | 172.16.0.0 – 172.31.255.255 | 1,048,576 | Srednje mreže |
| 192.168.0.0/16 | 192.168.0.0 – 192.168.255.255 | 65,536 | Kućne i manje mreže |

Privatne adrese nisu routabilne na internetu — koriste se samo unutar lokalnih mreža. Za pristup internetu se koristi NAT (Network Address Translation).

## Tekst editor Nano

`nano` je jednostavan tekst editor za terminal. Pokreće se sa:

```
nano fajl.txt
```

Najvažnije prečice (oznaka `^` znači `Ctrl`):

* `Ctrl+O` - sačuvaj fajl (Write Out)
* `Ctrl+X` - izlaz (Exit)
* `Ctrl+K` - izreži liniju (Cut)
* `Ctrl+U` - zalijepi liniju (Paste)
* `Ctrl+W` - pretraga (Where Is)
* `Ctrl+G` - pomoć (Get Help)
* `Alt+U` - undo
* `Alt+E` - redo

## Korištenje Jekyll-a

Jekyll pretvara Markdown tekst u statičke web stranice.

1. Logovanje na server

2. Dodavanje novog korisnika:

```
sudo adduser korisnik
```

3. Logovanje kao korisnik:

```
su - korisnik
```

4. Instalacija Ruby-ja (preporučeno putem [rbenv](https://github.com/rbenv/rbenv))

5. Ažuriranje gem-ova:

```
gem update
gem update --system
```

6. Generisanje SSH ključa:

```
ssh-keygen -t ed25519
```

7. Dodati javni ključ (`~/.ssh/id_ed25519.pub`) na GitHub repo.

8. Instaliranje Bundler-a i Jekyll-a:

```
gem install bundler jekyll
```

9. Kloniranje repozitorija:

```
git clone URL_REPOZITORIJA
cd ime_repozitorija
bundle install
```

10. Pokretanje Jekyll servera:

```
bundle exec jekyll serve
```

Server će biti dostupan na `http://localhost:4000`.

Za pokretanje u backgroundu:

```
bundle exec jekyll serve &
```
