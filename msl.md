---
layout: page
title: Mala Škola Linux-a
permalink: /mala-skola-linuxa/
---

Verzija dokumenta 0.0.3

## Uobičajena organizacija foldera u Linuxu

* `/bin`  - osnovni programi koje koriste i administratori i korisnici (npr. `ls`, `cp`, `cat`)
* `/dev`  - datoteke koje predstavljaju hardverske uređaje (diskovi, mrežne kartice, terminali)
* `/etc`  - konfiguracijske datoteke sistema i servisa
* `/home` - korisnički direktoriji (svaki korisnik ima svoj podfolder)
* `/sbin` - sistemski programi za administraciju (npr. `fdisk`, `iptables`)
* `/tmp`  - privremene datoteke (brišu se pri restartu)
* `/usr`  - korisnički programi, dokumentacija i biblioteke
* `/var`  - promjenjivi podaci: logovi (`/var/log`), mail, cache i sl.

**Napomena:** Na modernim distribucijama (Debian 12+, Ubuntu 22.04+, Fedora 30+) direktoriji `/bin` i `/sbin` su simbolički linkovi na `/usr/bin` i `/usr/sbin` (tzv. usr merge).

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

**Napomena:** `finger` je zastarjela komanda i nije instalirana po defaultu na većini modernih distribucija. Alternativa je komanda `pinky` (dio GNU coreutils) ili kombinacija `id` + `getent passwd`.

Komanda `finger` ispisuje informacije o korisniku. Kao argument komandi proslijedimo korisničko ime tj. `username` korisnika. U sljedećem primjeru `finger` će prikazati informacije o korisniku `root`:

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
sudo apt-get update
sudo apt-get install finger
```

### Komanda `id`

Ova komanda nam daje informacije o korisniku kao što su:

* `uid`    - broj korisnika (user ID)
* `gid`    - group ID tj. broj primarne grupe kojoj korisnik pripada
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

### Komande `adduser` i `usermod`

Dodavanje novog korisnika:

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

**Napomena:** Opcija `-a` (append) je obavezna uz `-G`, inače će korisnik biti uklonjen iz svih ostalih grupa.

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

Ispiši listu fajlova i direktorija uključujući i skrivene fajlove (skriveni fajlovi su fajlovi čije ime počinje sa tačkom `.`):

```
ls -al .
```

Ispiši listu fajlova i direktorija unutar trenutnog direktorija, te sadržaj poddirektorija:

```
ls -al *
```

Ispiši listu fajlova i direktorija, ali direktorije tretiramo kao obične fajlove (ne ispisujemo njihov sadržaj):

```
ls -ald *
```

Ispiši samo skrivene fajlove i direktorije (koji počinju sa znakom `.`):

```
ls -ald .*
```

### Ispis inode broja fajla

Inode je jedinstven identifikator fajla na filesystem-u. Svaki fajl i direktorij ima svoj inode broj.

```
ls -i ime_fajla
```

### Kreiranje simboličkih linkova (symlink)

Simbolički link je poseban fajl koji pokazuje na putanju drugog fajla. Ako se originalni fajl obriše, symlink postaje "broken" (mrtav link).

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

Napravimo simbolički link:

```
ln -s fajl_jedan fajl_link
```

**Sintaksa:** `ln -s CILJ IME_LINKA` — prvo ide originalni fajl, pa ime linka.

Ispišemo sadržaj linka:

```
cat fajl_link
```

Sadržaj je isti kao kod originalnog fajla.

Provjerimo inode-ove oba fajla:

```
ls -i fajl_jedan fajl_link
```

Inode brojevi su **različiti** — symlink je zaseban fajl koji samo pokazuje na putanju originala.

#### Vježba

Izbrisati originalni fajl (`rm fajl_jedan`). Da li `cat fajl_link` i dalje radi? (Odgovor: ne, jer symlink pokazuje na nepostojući fajl.)

### Hard linkovi

Hard link je drugo ime za isti fajl na disku. Za razliku od symlink-a, hard link dijeli isti inode sa originalom. Fajl se briše sa diska tek kada se uklone **svi** hard linkovi na njega.

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
ls -i fajl_prvi fajl_drugi
6257560 fajl_drugi
6257560 fajl_prvi
```

Inode brojevi su **isti** — oba imena pokazuju na istu lokaciju na disku.

**Ograničenja hard linkova:**
* Ne mogu se kreirati na direktorije
* Ne mogu se kreirati između različitih filesystem-a (particija)

#### Vježba

Šta se desi ako izbrišemo `fajl_drugi`? Da li će `fajl_prvi` biti izbrisan?

```
rm fajl_drugi
cat fajl_prvi
```

(Odgovor: `fajl_prvi` i dalje postoji jer je to samo jedno ime manje za isti inode.)

### Rekurzivno listanje sadržaja foldera

```
ls -R IME_FOLDERA/
```

Ispisuje cijelu strukturu foldera rekurzivno.

**Alternativa:** Za pregledniji prikaz stabla direktorija:

```
tree IME_FOLDERA/
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

Navigacija u `man`: `f` ili `Space` (naprijed), `b` (nazad), `/tekst` (pretraga), `q` (izlaz).

Kratki opis komande:

```
whatis ls
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

### Putanje do programa

Koristimo komande `whereis` i `which` da saznamo putanju programa:

* `which` - prikazuje putanju do executable-a koji bi se pokrenuo (pretražuje samo `$PATH`)
* `whereis` - prikazuje putanju do binary-ja, source koda i man stranica

```
which nano
/usr/bin/nano
```

```
whereis nano
nano: /usr/bin/nano /usr/share/nano /usr/share/man/man1/nano.1.gz
```

```
whereis bash
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

### Kreiranje, kopiranje i premještanje fajlova

Pravljenje praznog fajla (ili ažuriranje timestamp-a postojećeg):

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

* `*` - bilo koji broj znakova (uključujući nijedan)
* `?` - tačno jedan znak
* `[abc]` - jedan od navedenih znakova
* `[0-9]` - raspon znakova

Primjeri:

```
ls *.txt          # svi .txt fajlovi
ls dokument?.pdf  # dokument1.pdf, dokumentA.pdf, itd.
ls slika[1-3].jpg # slika1.jpg, slika2.jpg, slika3.jpg
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

**Oprez:** `rm` trajno briše fajlove — nema "korpa za smeće". Koristite `-i` opciju za potvrdu prije brisanja:

```
rm -ri ime_foldera
```

### Pretraga fajlova

```
find . -name "naziv"
find . -name "naziv*"
```

Case-insensitive pretraga:

```
find . -iname "naziv*"
```

Rekurzivno pretraži sve fajlove u direktoriju `/home`:

```
find /home
```

Pretraga samo za fajlovima (ne direktorijima):

```
find . -type f
```

Pretraga samo za direktorijima:

```
find . -type d
```

Pretraga fajlova po veličini (veći od 100MB):

```
find . -type f -size +100M
```

Pretraga fajlova mijenjanih u zadnjih 7 dana:

```
find . -type f -mtime -7
```

### Prompt znakovi

* `$` - nalazimo se kao obični korisnik
* `#` - nalazimo se kao root

### Promjena korisnika i root pristup

Prelazak na root korisnika:

```
su -
```

**Napomena:** Na Ubuntu i sličnim distribucijama, root nalog je zaključan po defaultu. Umjesto `su` koristi se `sudo`:

```
sudo komanda          # pokreni jednu komandu kao root
sudo -i               # otvori root shell (interaktivni login)
```

Logovanje kao drugi korisnik (novi login shell):

```
su - korisnik
```

**Napomena:** `su - korisnik` (sa crticom) je ispravniji od `su korisnik -l` jer učitava kompletno okruženje korisnika.

### Dozvole nad fajlovima

`chmod` - mijenja dozvole nad fajlom.

Oktalne dozvole — tri cifre za vlasnika (user), grupu (group) i ostale (others):

```
Read = 4, Write = 2, Execute = 1
```

Primjeri oktalnih dozvola:

| Oktalna | Simbolička | Značenje |
|---|---|---|
| `755` | `rwxr-xr-x` | Vlasnik: sve; grupa i ostali: čitanje + izvršavanje |
| `644` | `rw-r--r--` | Vlasnik: čitanje + pisanje; grupa i ostali: samo čitanje |
| `700` | `rwx------` | Samo vlasnik ima pristup |
| `600` | `rw-------` | Vlasnik: čitanje + pisanje; niko drugi nema pristup |

Simboličke oznake:

* `+` dodaje dozvolu
* `-` uklanja dozvolu
* `=` postavlja tačno navedene dozvole (uklanja ostale)

Ciljevi:

* `u` - user (vlasnik)
* `g` - group (grupa)
* `o` - others (ostali)
* `a` - all (svi)

Primjeri:

Uklanjamo korisniku pravo čitanja fajla `test.sh`:

```
chmod u-r test.sh
```

Dajemo svima pravo izvršavanja:

```
chmod a+x skripta.sh
```

Postavljamo dozvole oktalno (vlasnik: rw, grupa: r, ostali: r):

```
chmod 644 test.sh
```

### Vlasništvo nad fajlovima

`chown` - mijenja vlasnika fajla.

Prebacujemo vlasništvo fajla na root:

```
sudo chown root test.sh
```

Mijenjamo i vlasnika i grupu:

```
sudo chown korisnik:grupa test.sh
```

Rekurzivna promjena vlasništva za direktorij:

```
sudo chown -R korisnik:grupa direktorij/
```

### Korištenje pipe-ova

Pipe (`|`) prosljeđuje izlaz jedne komande kao ulaz drugoj:

```
echo "hello" | wc
      1       1       6
```

Rezultat: 1 linija, 1 riječ, 6 bajtova (5 znakova + newline).

Više pipe-ova u nizu:

```
cat /var/log/syslog | grep "error" | wc -l
```

Ovo broji koliko linija u syslogu sadrži riječ "error".

### Redirekcija

* `>` - preusmjeri izlaz u fajl (prepiše sadržaj)
* `>>` - dodaj izlaz na kraj fajla (append)
* `2>` - preusmjeri greške (stderr) u fajl
* `2>&1` - preusmjeri greške na standardni izlaz

```
echo "tekst" > fajl.txt     # prepiše fajl
echo "tekst" >> fajl.txt    # dodaje na kraj
komanda > output.txt 2>&1   # i izlaz i greške u isti fajl
```

### Čitanje sadržaja fajlova

`cat` (concatenate) - ispisuje sadržaj fajla:

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
```

Prvih 20 linija:

```
head -n 20 dugiTekst.txt
```

`tail` - ispisuje zadnjih 10 linija (po defaultu):

```
tail dugiTekst.txt
```

Zadnjih 5 linija:

```
tail -n 5 dugiTekst.txt
```

Praćenje fajla u realnom vremenu (korisno za logove):

```
tail -f /var/log/syslog
```

Kombinacija komandi sa pipe-om — ispiši zadnjih 5 linija sa brojevima:

```
cat -n dugiTekst.txt | tail -n 5
```

`less` - interaktivno pregledavanje dugačkih fajlova:

```
less dugiTekst.txt
```

Navigacija u `less`: `f`/`Space` (naprijed), `b` (nazad), `/tekst` (pretraga), `n` (sljedeći rezultat), `q` (izlaz).

### Grep - pretraga teksta u fajlovima

Osnovna pretraga:

```
grep "text" file.txt
```

Case-insensitive pretraga:

```
grep -i "text" file.txt
```

Rekurzivna pretraga kroz direktorij:

```
grep -r "text" /putanja/
```

Prikaži brojeve linija:

```
grep -n "text" file.txt
```

Prikaži linije koje **ne** sadrže traženi tekst:

```
grep -v "text" file.txt
```

Kombinacija — rekurzivno pretraži, prikaži brojeve linija, ignoriši velika/mala slova:

```
grep -rni "error" /var/log/
```

### Korisne komande

* `.`  - oznaka za trenutni direktorij
* `..` - oznaka za parent direktorij
* `printenv` - ispis svih environment varijabli
* `pwd` - print working directory, provjera putanje na kojoj se nalazimo
* `whoami` - prikazuje ime trenutno logovanog korisnika
* `hostname` - prikazuje ime računara
* `date` - prikazuje trenutni datum i vrijeme
* `uptime` - prikazuje koliko dugo sistem radi
* `df -h` - prikazuje slobodan prostor na diskovima
* `du -sh direktorij/` - prikazuje veličinu direktorija
* `free -h` - prikazuje korištenje memorije

### Generisanje SSH ključa

Preporučeni algoritam za nove ključeve je Ed25519:

```
ssh-keygen -t ed25519 -C "email@primjer.com"
```

Alternativno, RSA sa dovoljnom dužinom ključa (minimalno 3072 bita):

```
ssh-keygen -t rsa -b 4096
```

**Napomena:** Ed25519 je brži i sigurniji od RSA za nove instalacije. RSA ključevi kraći od 2048 bita se smatraju nesigurnim.

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

Opcija `z` dodaje gzip kompresiju.

Ekstrakcija arhive:

```
tar -xvf myfile.tar
```

Ekstrakcija kompresovane arhive:

```
tar -xzvf myfile.tar.gz
```

Pregled sadržaja arhive bez ekstrakcije:

```
tar -tvf myfile.tar
```

## Procesi

Izlistaj sve procese svih korisnika:

```
ps -ef
```

* `-e` - ispis svih procesa u sistemu
* `-f` - ispis dodatnih podataka o procesima (full format)

Ili:

```
ps aux
```

* `a` - procesi svih korisnika
* `u` - korisnički format (prikazuje CPU, memoriju)
* `x` - uključuje procese bez terminala

Izlistaj procese samo za `sshd` korisnika:

```
ps -f -u sshd
```

Sortiraj procese po potrošnji memorije:

```
ps aux --sort=-%mem
```

Sortiranje procesa po CPU potrošnji:

```
ps aux --sort=-%cpu
```

**Napomena:** Prefiks `-` sortira u opadajućem redoslijedu (najveći potrošači prvo). Bez prefiksa se sortira uzlazno.

Interaktivni pregled procesa:

```
top
```

Ili modernija alternativa:

```
htop
```

### Slanje procesa u background

Nakon komande dodamo znak `&`:

```
sleep 60 &
```

**Napomena:** Interaktivne komande (poput `nano`, `vim`) nije praktično slati u background jer zahtijevaju pristup terminalu.

Izlistamo procese u backgroundu:

```
jobs
```

Vratimo proces u foreground:

```
fg %1
```

Pošaljemo running proces u background: pritisnemo `Ctrl+Z` (pauzira proces), zatim:

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

Prisilno zaustavljanje procesa koji ne reaguje:

```
kill -9 12345
```

**Napomena:** `kill -9` (SIGKILL) bi trebao biti zadnja opcija jer proces nema priliku da se čisto zatvori. Prvo probajte obični `kill` (SIGTERM).

Pronalaženje PID-a po imenu procesa:

```
pgrep -a ime_procesa
```

## Mreža

### Pronalaženje IP adrese

Moderna komanda za pregled mrežnih interfejsa:

```
ip addr
```

Ili skraćeno:

```
ip a
```

**Zastarjela alternativa** (možda nije instalirana na novijim sistemima):

```
ifconfig
```

`ifconfig` je dio paketa `net-tools` koji se više ne instalira po defaultu. Koristite `ip` komandu umjesto toga.

Nakon ukucane komande tražimo adresu sa `inet` prefiksom (IPv4) ili `inet6` (IPv6).

### Komande ping i traceroute

`ping` - mjerenje odaziva nekog servera:

```
ping -c 4 ime_servera
```

**Napomena:** Na Linuxu `ping` radi beskonačno dok se ne prekine sa `Ctrl+C`. Opcija `-c 4` šalje samo 4 paketa.

`traceroute` - izlistavanje svih čvorova na putu do nekog servera:

```
traceroute ime_servera
```

### Posebne IP adrese

* `0.0.0.0` - označava "sve interfejse". Kada server sluša na `0.0.0.0`, prihvata konekcije na svim IP adresama
* `127.0.0.1` - loopback adresa (localhost), koristi se za lokalne konekcije i nije dostupna izvana

### Zašto kao obični korisnik moramo kucati punu putanju do `ifconfig` komande?

**Napomena:** Ovo se odnosi na starije distribucije. Na modernim sistemima (Debian 11+, Ubuntu 20.04+) `/sbin` je uključen u `$PATH` svih korisnika, pa ovaj problem više ne postoji.

Komanda `ifconfig` se nalazi u direktoriju `/sbin`. Korisniku su dostupni samo programi koji se nalaze u putanjama izlistanim u `$PATH` shell varijabli.

Kada smo logovani kao root korisnik, provjerimo `$PATH`:

```
whoami
root
```

```
echo $PATH | grep '/sbin'
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
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
echo $PATH | grep '/sbin'
```

Prazan odgovor — `/sbin` nije u `$PATH`. Zato dobijamo grešku `ifconfig: command not found`.

Privremeno rješenje — dodamo `/sbin` u `$PATH`:

```
PATH=$PATH:/sbin
```

Sada `ifconfig` radi bez pune putanje.

**Napomena:** Ova izmjena važi samo za trenutnu sesiju. Nakon logout-a `$PATH` se vraća na početne vrijednosti. Za trajnu promjenu, dodajte liniju u `~/.bashrc`:

```
echo 'export PATH=$PATH:/sbin' >> ~/.bashrc
```

### Prepoznavanje privatnih IP adresa

Privatni IPv4 adresni prostori (RFC 1918):

| Blok | IP adresni raspon | Broj adresa | Uobičajena upotreba |
|---|---|---|---|
| 10.0.0.0/8 | 10.0.0.0 – 10.255.255.255 | 16,777,216 | Velike mreže, cloud |
| 172.16.0.0/12 | 172.16.0.0 – 172.31.255.255 | 1,048,576 | Srednje mreže |
| 192.168.0.0/16 | 192.168.0.0 – 192.168.255.255 | 65,536 | Kućne i manje mreže |

Pregled mrežnih interfejsa i njihovih IP adresa:

```
ip addr
```

* `inet` — IPv4 adresa
* `inet6` — IPv6 adresa

## Korištenje Jekyll-a

Jekyll pretvara običan tekst (Markdown) u statičke web stranice.

1. Logovanje na server

2. Dodavanje novog korisnika:

```
sudo adduser korisnik
```

3. Logovanje kao korisnik:

```
su - korisnik
```

4. Instalacija Ruby-ja (preporučeno putem rbenv ili RVM)

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
