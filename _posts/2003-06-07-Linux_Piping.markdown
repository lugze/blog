---
layout: post
title:  "Linux Piping"
date:   2003-06-07 17:55:20 +0100
categories: blog
---

* Nedim Hadzimahmutovic - grungy@linux.org.ba
* 07.06.2003.- 19.02.2006 v0.8

Mogucnost korištenja pipinga je jedna od moci Unixoidnih sistema. Korištenje ove tehnike u terminalu je dobar trik, a i predstavlja olakšanje pri radu. Piping je takoder raširena metoda medu C programerima. Bez pipinga, bilo bi potrebno pisati velike kolicine koda, da bi se uradili jednostavni zadaci. U osnovi Piping cini akt pokretanja neke komande/programa i zatim slanje njenog izlaznog rezultata na drugi program ili datoteku, znaci zapisivanje u tu datoteku.


## Rad sa pipingom
### I/O redirekcija

Napravite tekst datoteku koja ce sadrzati mnogo linija teksta sacinjenih od rijeci TUX, a zatim jednu recenicu koja ce sadrzati rijec TUX i rijec Linux. Zatim ukucajte sljedece " grep TUX moja_datoteka.txt ". Rezultat ovog zadataka ce kao i obicno biti izlistan na ekranu, a sacinjavat ce pretragu za recenicama koje sadrze rijec TUX. Medutim, ako ukucamo `grep TUX moja_datoteka.txt > tux_recenice.txt`. Rezultat mozete vidjeti u datoteci tux_recenice.txt . Vidimo da je rezultat komande grep redirektiran i zapisan u datoteku tux_recenice.txt . Dio komande " > tux_recenice.txt " kaze shellu da napravi novu datoteku pod nazivom tux_recenice.txt i u nju zapise rezultat komande grep , umjesto da sve izlista na ekran. Ako vec postoji datoteka sa istim imenom onda ce rezultat komande grep biti zapisan preko sadrzaja te datoteke. Kao sto smo primjetili redirekciju izvrsavamo pomocu znaka > , koji se jos i zove Output redirektor .

Medutim, ako umjesto znaka > stavimo znak >>, sadrzaj vec postojece datoteke ce ostati isti, a rezultat ce biti dodan na zadnju liniju teksta. Pomocu ' echo' komande, koja ce neki tekst jednostavno izlistati na ekran, mozemo dodavati tekst u neku datoteku, npr.
echo "pingvin" >> tux_recenice.txt

Takoder redirekciju mozemo vrsiti i pomocu znaka < , ili kako se jos zove Input redirektor . Ovaj znak ima funkciju da redirektira sadrzaj neke datoteke na input ( stdin ), odnosno sadrzaj odredene datoteke bi zamjenili ono sto bi inace dolazilo sa tastature.

Primjer:

```
grep Tux < tux_recenice.txt
```


Input i output redirektori se mogu i kombinovati. Tako na primjer komanda cp se inace koristi za kopiranje datoteka, medutim ako u nekom slucaju ta komanda ne postoji ili je taj program ostecen, mozemo koristiti cat komandu na sljedeci nacin:

```
cat < datoteka1 > datoteka2
```


Ovo je slicno kao i cp datoteka1 datoteka2

### Piping pomocu | znaka

Prava moc pipinga je kada jedan program moze da cita output nekog drugog programa. Posmatrajmo grep komandu kada je pokrenemo bez argumenata.

```
grungy@linux:~> grep Tux
recenica koja sadrzi rijec Tux
recenica koja sadrzi rijec Tux
recenica bez te rijeci
Tux je pingvin
Tux je pingvin
#
```


grep cita sa ulaza, tastature, i ispisuje recenicu u kojoj se nalazi rijec Tux, tako da takve recenice su prikazane dva puta. Sada ukucajte " grep TUX moja_datoteka.txt | grep Linux ". Prvi grep izlista sve Tux recenice kao output. Znak | vrijednosti iz outputa prenosi na input sljedece komande, koja je takoder grep komanda. Druga grep komanda pregleda sadrzaj inputa u potrazi za recenicama koje sadrze rijec Linux u sebi. Komanda grep na ovaj nacin se cesto koristi kao filter, i moze se koristiti u vise primjeraka, npr.


```grep L moja_datoteka.txt| grep i | grep n | grep u | grep x```



### Korisni Primjeri Linux Pipinga & Redirekcije:

• Sljedeci primjer izlistava listu procesa u datoteku test.txt.

```
grungy@linux:~> ps > test.txt
```


• Komanda "ps -aux" izlistava sve procese (programe) koji su pokrenuti u tom momentu. Lista procesa ce biti poslana na grep komandu, koja ce taj sadrzaj pretraziti u potrazi za datim stringom, u ovom slucaju "user". Krajnji rezultat na ekranu bi bila lsita svih procesa koji je odredjeni korisnik pokrenuo. String "user" mozemo zamjeniti sa bilo kojim imenom korisnika na toj linux masinom. Na ovaj nacin mozemo pratiti rad odredjenih korisnika.

```
grungy@linux:~> ps -aux | grep "user"
```


• Lista procesa koje je pokrenuo odredjeni korisnik, snima se u datoteku korisnikovi_procesi.txt (rijec korisnik zamjeniti sa loginom zeljenog korisnika):

```
grungy@linux:~> ps -aux | grep korisnik > korisnikovi_procesi.txt
```


• Listing trenutno pokrenutih procesa, stranica po stranica:

```
grungy@linux:~> ps -Hefw | less
```


• Snimanje listinga direktorijau datoteku:

```
grungy@linux:/usr > ln -l > ~/usr-listing.txt
```

navedena komanda snima sadrzaj direktorija /usr u home direktorij korisnika u datoteku usr-listing.txt .



• Sljedeci primjer koristeci komandu cat, sadrzaj datoteke test.txt salje komandi grep, koja prikazuje samo rezultate koje sadrze rijec blah.


```
grungy@linux:/usr > cat test.txt | grep "blah"
```


• Datoteka /etc/servise sadrzi listu prepoznatljivih TCP/IP servisa, ciji sadrzaj mozemo sortirati po abecedi na sljedeci nacin:

```
grungy@linux:~> cat /etc/services | sort
```


• Sljedeca komanda je nadopuna prethodno navedene, osim sto kao dodatak, komanda tail uzima zadnjih 50 linija datoteke services, i less komanda prikazuje sadzaj stranicu po stranicu.

```
grungy@linux:~> cat /etc/services | sort | tail -n 50 | less
```


• Zamsilite da imate datoteku koja sadrzi hiljade e-mail adresa, i trebate ih sortirati i zatim raspodjeliti u manje dijelove. Da bi ovaj posao obavili koristi se piping tehnika. Komanda cat ucitava sadrzaj datoteke lista.txt i salje je komandi sort koja ih sortira, koristeci argumente. Argumenat "-f" znaci da se nema razlike izmedju malih i velikih slova, argumenat "-t @" definise razmak izmedju redova, argumenat "-k 2" govori da se sortiranje izvrsi po domeni u e-mail adresi,

```
grungy@linux:~> cat lista.txt | sort -f -t @ -k 2 | split -l 500 - lista
```

komanda "split -l 500 - lista" govori da se rezultat sa sortiranja izreze u datoteke dugo po 500 linija, i da im daje imena da pocinju sa rijecju "lista", npr. listaaa, listaab, listaac itd.



• Sortirafni fajlovi se mogu spojiti (opcija -m odnosno merge), koristeci -m opciju:

```
grungy@linux:~> sort -m prvi_kvartal drugi_kvartal > prvo_polugodiste.txt
```


• Piping man stranice neke komande u datoteku. Komanda col sluzi da filtrira output, tako sto izbacuje nepozeljne karaktere,ostavljajuci samo backspace (^H). Kao primjer izabran je 'ls man':

```
grungy@linux:~> man ls | col -bx > datoteka.txt
```


• Zelite saznati koji dorektoriji i stabla zauzimaju najvise prostora? Unesite sljedeci pipe:

```
grungy@linux:~> du -sm $(find $1 -type d -maxdepth 1 -xdev) | sort -g
```


* da dobijete listing svih direktorija u stablu, kucajte:

```
grungy@linux:~> find $1 -type d | xargs du -sm | sort -g
```

• Provjera da li je program apache instaliran, odnosno rpm paket (rpm bazirane distribucije):

```
grungy@linux:~> rpm -qa | grep apache
```


copyleft
Linux User Group Of Zenica - LugZe
