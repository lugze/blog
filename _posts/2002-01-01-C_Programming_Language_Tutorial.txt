---
layout: post
title:  "C Programming Language Tutorial"
date:   2002-01-01 17:55:20 +0100
categories: blog
---

Mirza S. mirzas@codelinux.com &
Nedim Hadzimahmutovic grungy@linux.org.ba, LugZe
http://ze.lugbih.org
v 1.0 , 1 Yanuar 2002


Ovaj tutorial je iskljucivo napisan za pocetnike, koji misle da pocnu
svoju programersku karijeru na najboljem Os-u na svijetu ,Linux naravno, i u C, programskom jeziku.
Ako se pitate da li da pocnem sa C-om , i da li se ipak isplati uciti C, odgovor je definitivno DA!
Takodjer je velika prednost programirati na Linux-u, jer pored sto je i sam OS besplatan, imate veliku
kolicinu kodova koji su otvorenog tipa (open source) od kojih mozete mnogo nauciti, samim time mozete naci
neke nedostatke ili poboljsati te kodove (zar nije dobar osjecaj znati kako u tom citavom Linuxu ima
tvojih ideja i koda, odnosno da si TI sudjelovao u izgradnji tako dobrog OS-a, naravno da jest:).

ZA sve dopune, greske ili komantare javite se na e-mail adresu jednog od autora.
---------------------------------------

*  Copyright

  Copyright (C) 2002 Mirza S, CodeLinux.This
  document is free; you can redistribute it and/or modify it under the
  terms of the GNU General Public License as published by the Free
  Software Foundation; either version 2 of the License, or (at your
  option) any later version. This document is distributed in the hope
  that it will be useful, but

  WITHOUT ANY WARRANTY; without even the implied warranty of
  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU
  General Public License for more details. You can get a copy of the GNU
  GPL here <http://www.gnu.org/copyleft/gpl.html>

 ->Jednostavno receno, ovaj dokumenta je pod GNU licencom,
   mozete ga slobodno dalje dijeliti, koristiti se sadrzajem, modifikovati ga...
   al ipak, ako se odlucite da upotrijebite sadrzaj ovog tutoriala,
   dajte i koji kredit stvarnom autoru.
---------------------------------------

## Globalna struktura c programa


C programi su u stvari skup funkcija u jednom ili vise fajlova.
Svaki c program bio on kompajliran ili interpretiran mora da ima bar jednu funkciju.
Ta funkcija je main() funkcija i ujedno je entery point programa tj. ulazna tacka za
taj program i prva koja ce biti pozvana kada se program pokrene.
main funkcija moze da poziva druge funkcije i druge funkcije mogu da pozivaju druge funkcije.
Kod ovoga treba paziti da se neke funkcije ne pozivaju nekontrolisano. tj. da se treba
paziti slucajne rekurzije. Rekurzija nije problem ako se pazljivo dizajniraju funkcije, i ako ima
dovoljno memorije..
Memorija je problem jer svaki puta kada se funkcija rekurzivno pozove napravi se duplikat
iste (bar u Turbo Pascalu pod WinxxxOS-om) i taj duplikat zauzima dragocjenu memoriju.

Primjer programa:

```
/*
	Moj dragi program i moj dragi komentar.
	by Nedim H. 2001 (c)

		Das tutor1.c programm.
*/

void main(void){
	printf("Hello ya all\n");
}
```


Pravo jednostavno, ovaj program ispisuje Hello ya all na konzolu i prelazi u sljedeci red, jer na kraju ima '\n'
a '\n' je new line :)

Funkcije mogu imati parametre i mogu imati svoj tip. U gore navedenom primjeru funkcija main nema nikakve parametre
i nema povratni tip. (void se koristi u tim slucajevima)
Sto znaci da mozemo i ovako napisati identican program,

```
/*
	Das komentar
*/

int main(void){
	printf("Hello ya all\n");
	return 0;
}
```

Napomena: Kada funkcija ima povratni tip (u ovom slucaju int), pozeljno (ako ne i obavezno) je da se koristi return xxx;
Kako i samo ime govori return se vraca tj. izlazi iz funkcije i vraca vrijednost xxx. Ako pozovemo return
u main funkciji to bi znacilo da je kraj programa i da se linije poslije toga nece izvrsavati.
(nisam pokusao jer sam uglavnom koristio exit(0) kada sam nasilno gasio program.)

Razlika izmedju exit(0) i return je sto exit(0) bilo gdje da se pozove prouzrokuje zaustavljanje programa, dok to
return radi samo ako je u main funkciji. (logicno jer ako izadje iz glavne funkcije sta mu ostaje da uradi ?? nista)

Parametri
---------


parametri su vrijednosti koje prosljedjujemo funkcijama, tj. variable koje saljemo funkcijama, samo onda kada
funkcija treba da nesto uradi sa tim variablama/parametrima, recimo printf(); je jedna od funkcija koja za parametre
uzima niz karaktera i onda taj niz ispisuje.

Idemo napraviti lame funkciju koja ce pozvati printf() za ispis na konzolu.

```
/*
	Das lame prinf programm
*/

void pisi(char *niz){
	printf("%s",niz);
}

int main(void){
	pisi("Das is a lame print function by M.S\n");
	return 0;
}
```

+ Ne-dozvoli da te "char *niz" zbuni jer je to pointer na char.

Mozemo isto napisati funkciju koja ce ispisivati neki int (int je broj, skoro isto kao integer u pascalu)

```
/*
	Das pisi broj lame prog.
*/

void pisi_broj(int broj){
	printf("Broj je %d",broj);
}

void main(void){
	pisi_broj(5);
}
```


Kao sto vidis ova zadnja dva programa su ista, samo sto funkcije koriste drugacije tipove podataka
za parametre.


Malo komplikovaniji primjer.

```
/*
	Das saberi dva broja.
*/

int saberi(int broj1,int broj2){ // funkcija saberi vraca int, uzima dvije "int" varijable "broj1" i "broj2"
	int zbir; // lokalna varijabla zbir, u koju privremeno ostavljamo zbir
	zbir = broj1 + broj2; // ovdje vrsimo matematicku operaciju i rezultat stavljamo u "zbir" variablu
	return zbir; // magic dio, ovdje se zbir vraca u funkciju main
}

void main(void){
	int neki_broj=10; // deklaracija variable i inicializacija na 10; to sam uradio jer necu sad da citam br. iz konzole
	int jos_jedan_broj=50;// isto kao i gore samo sto je postavljen na 50
	int rezultat=0; // stavi rezultat na 0
	rezultat = saberi(neki_broj,jos_jedan_broj); // pozovi nasu funkciju i njezin return stavi u "rezultat" variablu
	printf("Zbir %d i %d je %d\n",neki_broj,jos_jedan_broj,rezultat) // kompleksni poziv printf() funkcije.
}
```


Na konzoli ce biti ovo :

Zbir 10 i 50 je 60


Isti program se moze napisati ovako

```
/*
 	Das das
*/

int saberi(int broj1,int broj2){
	return (broj1+broj2);
}

void main(void){
	int broj_neki=10;
	int broj2_neki = 50;
	printf("Zbir %d i %d je %d\n",broj_neki ,broj2_neki, saberi(broj_neki,broj2_neki) );
}
```


Ovako program izgleda puno manji i komplikovaniji :)



Nesto vise o printf();

* %d - int, tj. broj
* %c - char, tj. jedan karakter (character)
* %s - string ili niz karaktera moze i kao pointer na char -> ovako : char *moj_niz_kao_pointer_na_char ili char samo_niz_dug[512]
* ... i jos njih ali ovi su najcool.

Toliko za ovaj put..vidim da sam napisao 151 liniju.
	6:33 PM 12/7/2001 ,
--------------
Pocinjemo opet.
Malo oko tipova podataka.


int - ili broj
--------------

Ima svoju granicu, prima pozitivne i negativne brojeve.

```
int broj;
broj = 1;
broj++; // je isto kao i  broj=broj+1;
broj--; // je isto kao i broj=broj-1;
```

unsigned int broj; // je isto kao i int samo sto nema negativnih brojeva. I moze da primi vise brojeva, jer je
prostor za negativne brojeve iskoristen za pisanje dodatnih pozitivnih.


Razlika izmedju broj++ i ++broj
-------------------------------

Obe stvari u sustini imaju isti zadatak a to je da
povecaju vrijednost variable "broj" za jedan.

```
int broj;
broj = 1;
broj++;
// sad broj ima vrijednost 2;

int broj=5;
broj++;
broj++;
// sad broj ima vrijednost 7;
```


isto ovo moze i kao :

```
int broj;
broj = 1;
++broj;
// sad broj je 2


int broj=5;
++broj;
++broj;
// sad broj je 7
```


Znaci da u ovim slucajevima nema razlike i sasvim je svejedno sta koristimo jer uvjek ce rezultat biti isti,..
ALI PAZNJA !!!! ima jako bitna razlika

kako ?

```
int broj;
int broj2;

broj = 5;
broj2 = broj++;
// sada broj2 ima vrjednost 5;

int broj;
int broj2;

broj = 5;
broj2 = ++broj;
// sada broj2 ima vrjednost 6
```

Ukratko ++broj ce da variabli "broj" povisi vrijednost prije upotrebe.. dok ce broj++ prvo upotrjebiti
vrijednost "broj" variable i tek nakon toga ce povisiti njenu vrijednost za jedan. To je glavna i jedina prava
razlika izmedju broj++ i ++broj;
-------------------------------


Sigurno jedva cekas da dodjemo do onog djela kada se nesto ucitava sa konzole ili fajlova ali nemoze jos jer moras
da skontas if,i petlje..

IF
--

Hocemo da napisemo funkciju koja ce da kaze koji je broj veci.

/*
	das veci broj
*/

void pisi_veci(int broj1,int broj2){
	if (broj1>broj2){
		printf("Veci je %d",broj1);
	} else {
		printf("Veci je %d",broj2);
	}
}

void main(void){
	int a,b;
	a = 10;
	b = 20;
	pisi_veci(a,b);
}



znaci da kostur if-a ide ovako:

if (..... uslov){
	..uradi ovo ako je uslov tacan (rijec "tacan" na nasem programerskom jeziku znaci "jednak TRUE")
}


malo slozenije je :

if (uslov.....) {
	...ako uslov tacan uradi ovo
} else {
	....ako uslov nije tacan uradi ovo..
}


ili


if (uslov1){
	ako uslov1 je tacan uradi ovo
} else if(uslov2) {

	ako uslov1 nije tacan i ako je uslov2 tacan onda radi ovo

} else {

	ako uslov1 i uslov2 nisu tacni uradi ovo...

}


Ovaj gore program ima gresku a to je da ako su brojevi jednaki ponasa se kao da je onaj drugi veci..

to ispravljamo ovako:

void pisi_veci(int broj1,int broj2){
	if (broj1==broj2){
		// ako su brojevi jednaki
		printf("Brojevi jedanki!\n");
	} else if (broj1>broj2){
		//ako brojevi nisu jednaki i ako je broj1 veci od broja2
		printf("Brojevi nisu jednaki, broj1 %d je veci od %d",broj1,broj2);
	} else {
		// ako brojevi nisu jednaki i ako broj1 nije veci od broja2
		printf("Brojevi nisu jednaki, broj2 %d je veci od broja1 %d!\n",broj2,broj1);
	}
}


Puno srece ..

8:05 PM 12/7/2001
Tu sam opet, pa da se vratim na C.


Ocekujem da si sazvakao if - naredbu .ako nisi onda nisam bio dovoljno detaljan......
ipak da se malo vratim...

onaj dio "uslov1" .. i sl. to je u stvari nesto sto te zanima kod tog if-a
recimo "a" vece od "b" ide ovako : a > b
To je takozvani boolean operator ili expression. On moze imati vrijednost TRUE ili FALSE
Vrijednost odredjuje(racuna) kompijuter...
Do nas je samo da pravilno napisemo uslov..

vidi ovo :


/*
	das if test.
*/


void main(void){
	if(TRUE){
		printf("Jabuka\n");
	}
}

ovaj progy ce uvjek ispisivati jabuka jer je TRUE uvjek true... i nema smisla koristiti IF u ovom slucaju
isto tako ako zamjenis TRUE sa FALSE, program nece nikad ispisati "Jabuka" jer je false uvjek false...isto
kao i 1 je uvjek 1 i dva je uvjek 2....


mozes i ovako napisati if

if ( (a>b) == TRUE ) {
	/*uradi nesto*/
}

ovdje se dva booleova izraza porede a>b i TRUE

a > b moze biti TRUE ili FALSE

moras da gledas na to ovako:


Zamisli ovo..da postoji tip bool .. u koji mozes staviti TRUE ili FALSE


i kazes

bool uslov; // uslov je variabla tipa bool

uslov = ((a > b) == TRUE);

if (uslov) {
	//ako dodje ovdje,uslov je true
} else {
	//sada uslov nije true
}


kompijuter ce vrijednost za uslov odrediti tako sto ce prvo da vidi da li je a vece od b, ako jeste
Onda ce da a > b zamjeni sa TRUE i dobijemo ovo

TRUE == TRUE ..... logicno je da je TRUE jednako TRUE tako da citav izraz je TRUE jer je tacan,

i to se zamijeni sa TRUE
i dobijemo da je

uslov = TRUE;

kasnije se uslov zamjeni sa TRUE i dobijemo

if (TRUE) {
	//ako dodje ovdje,uslov je true... sad sigurno dolazi ovdje
} else {
	//sada uslov nije true
}

to je tako samo ako je a > b a ako nije onda se a > b mijenja sa FALSE
i dobijemo FALSE == TRUE sto je pogresno i citav izraz se mjenja sa FALSE
i dobijemo

if (FALSE) {
	//ako dodje ovdje,uslov je true..nema sanse da dodje ovdje ..
} else {
	//sada uslov nije true, i ovdje sigurno dolazi...
}

Namjerno sam koristio ono dodatno == TRUE radi ilustracije inace nema potrebe da se koristi
moze se i ovako napisati ....

bool uslov;

uslov = a > b;

i ako je a > b tacno onda se TRUE stavlja u "uslov" variablu... a ako nije tacno onda se stavlja FALSE
i ostalo je isto...stvar je u tome sto mi neznamo koje ce biti i moramo da isprogramiramo za oba slucaja
ako nas oba interesuju ili samo za jedan ako nas samo taj slucaj interesuje..

recimo ako neki broj predje neku granicu da ga vratimo na nulu a ako je ispod granice da ga
povecamo za jedan... to bi u C jeziku bilo ovako

/*
	das nesto
*/
void main(void){
	int granica=150;
	int brojac=0;
	while(brojac<granica){
		brojac++;
	}
}


ovdje se ne koristi if jer se sva provjera vrsi u while() djelu...
iako se moze napisati i ovako ...samo ovo niko nikad nece napisati
i ako nekome kazes da sam ovo napisao ...osramotit ces me :)) salim
se ..stvar je da se izbjegava "goto" sto vise ...
evo ista stvar samo u basicu ali je u biti ista
odabrao sam basic jer neznam kako ide "goto" u c-u .. jer ga nisam nikad koristio..a i nema
potrebe da se koristi.


Dim brojac as Integer
Dim granica as Integer


granica = 150
brojac = 0
ponovo:
	brojac = brojac + 1
	if brojac < granica then goto ponovo


znaci samo onda kada brojac bude jednak (ili veci samo je to u ovom slucaju nemoguce,skontaj zasto..) granici
program ce da stane... jer ga onaj if nece vratiti gore ..

Ok da rijesimo par zadataka...

Sada idu oni zeznuti...

Ok prvo na Bosanskom pa onda na C jeziku..
Bosansko-Njemacki : Das jedan prog, koji ce da kaze Daj mi slovec:
i da ispise Upisal si : <to sto si upisao>

ok
idemo

/*
	Obavezni komentar, mjesto za neku provalu ili foliranje
	i obavezno kopirajt.
*/

#include<stdio.h> // neka furka ..nikad se nezna

int main(void){
	char moj_niz[512]; // mjesto gdje cemo sakriti nas slovec (ono sto je luzer napisao)
	int ch; // privremena variabla koja cuva jedan od mnogih sloveca :)
	int pozicija=0;
	printf("Daj mi slovec : ");
	while((ch=getchar())!=EOF && ch!='\n'){
		moj_niz[pozicija++] = ch;
	}
	printf("Upisal si : %s\n",moj_niz);
	printf("Broj sloveca : %d",pozicija);
	return 0;
}


Ovo kad skontas bit ces cool. Znam da vec jesi ..jer je pravo jednostavno
isto tako ovo je prelazna granica i znam da neizgleda nimalo lagano ali
vjeruj mi lakse je nego sto mislis. Jer poslije ovoga dolaze pravo dobre stvari
i nema ti stajanja...ja sam tu da ti odgovorim na svako pitanje...



idemo dio po dio....

/*
	Samo komentar :)
*/

#include <stdio.h>

ovo je include za stdio.h standard input output ...ovo je standardni include fajl
i normalno je da se koristi jer nam mogu zatrebati neke funkcije iz njega...
ovi .h fajlovi sadrze samo definicije funkcija i tipova podataka i konstanti ...itd.. sad nas oni
neznanimaju..

int main(void) {

ova linija definise glavnu i jedinu funkciju main() koja nam treba i koja vraca int
iako nema nikakve veze moze biti i void ...trenutno sasvim svejedno..


char moj_niz[512];

ova linija kaze kompajleru da "napravi" 512 variabli tipa char (char je jedno slovo) ..sto znaci
da u moj_niz moze stati 512 slova .... jer nam trebaju kod unosa ..jer neces reci unesite jedno slovo
zato nam treba ovaj niz slova... znaci da zelimo u njemu da cuvamo ono sto luzer unese
i kasnije to ispisemo preko printf() ---vidis jednostavno..


int ch;

definisemo jednu variablu tipa int koja ce da uzme jedan karakter (slovo,char) od getchar() ..
sad je logicno pitati zasto nije tipa char ... jer uzima od getchar() a ne od getint() (getint nepostoji!)
razlog je : int moze da uzima vrijednosti manje od nule tj. negativne... isto tako
koristimo variablu za provjeru dali je doslo do kraja linije (enter) ili kraja fajla (CTL + Z na win ili CTL + D pod Linux)
( getchar(); vraca negativan broj ako dodje do greske!)


int pozicija=0;

ovo definise variablu pozicija koja cuva broj unesenih slova i ona odredjuje gdje ce iduce ucitano
slovo biti upisano, tj. njegovo mjesto u variabli moj_niz.

printf("Daj mi slovec :");

ce samo da ispise luzeru Daj mi slovec nakon cega ce luzer dati par sloveca...

while(....) petlja vrti cjelu stvar u krug sve dok luzer ne pritisne Enter ('\n') ili EOF
ukoliko ch nije '\n' ili EOF onda se vrijednost variable pozicija povecava i moj_niz proguta
vrijednost ch-a .


Da simuliramo na slici



variabla moj_niz[512] , prije koristenja tj. prije pokretanja.
pozicija=0; // govori gdje ce biti upisan sljedeci karakter

 val  | index
+-----+-------+
+     +  0    +
+-----+-------+
+     +  1    +
+-----+-------+
+     +  2    +
+-----+-------+
+     +  3    +
+-----+-------+
+     +  4    +
+-----+-------+
+     +  5    +
+-----+-------+
+     +  6    +
+-----+-------+
+     +  7    +
+-----+-------+
+     +  8    +
+-----+-------+
+     +  9    +
+-----+-------+
+     +  n    +
+-----+-------+
+ ..  +  ..   +
+-----+-------+
+ nastavlja se do 512..



variabla moj_niz[512] , nakon sto luzer upise 'A'
pozicija = 1; // govori gdje ce biti upisan sljedeci

 val  | index
+-----+-------+
+ A   +  0    +  // znaci ch postaje 65 sto je ASCII kod za 'A', ta vrijednost se prenosi ovdje ovako : moj_niz[pozicija++]=ch
+-----+-------+
+     +  1    +
+-----+-------+
+     +  2    +
+-----+-------+
+     +  3    +
+-----+-------+
+     +  4    +
+-----+-------+
+     +  5    +
+-----+-------+
+     +  6    +
+-----+-------+
+     +  7    +
+-----+-------+
+     +  8    +
+-----+-------+
+     +  9    +
+-----+-------+
+     +  n    +
+-----+-------+
+ ..  +  ..   +
+-----+-------+
+ nastavlja se do 512..


variabla moj_niz[512] , nakon sto luzer upise 'B'
pozicija = 2; // govori gdje ce biti upisan sljedeci

 val  | index
+-----+-------+
+ A   +  0    +  // znaci ch postaje 65 sto je ASCII kod za 'A', ta vrijednost se prenosi ovdje ovako : moj_niz[pozicija++]=ch
+-----+-------+
+ B   +  1    +// znaci ch postaje 65 sto je ASCII kod za 'B', ta vrijednost se prenosi ovdje ovako : moj_niz[pozicija++]=ch
+-----+-------+
+     +  2    +
+-----+-------+
+     +  3    +
+-----+-------+
+     +  4    +
+-----+-------+
+     +  5    +
+-----+-------+
+     +  6    +
+-----+-------+
+     +  7    +
+-----+-------+
+     +  8    +
+-----+-------+
+     +  9    +
+-----+-------+
+     +  n    +
+-----+-------+
+ ..  +  ..   +
+-----+-------+
+ nastavlja se do 512..

ukoliko luzer sada pritisne EOF ili Enter,
ovaj dio koda ce se izvrsiti :

printf("Upisal si : %s\n",moj_niz);
printf("Broj sloveca : %d",pozicija);

sto ce ispisati :

Upisal si : AB
Broj sloveca : 2


Vidis sve se uklapa savrseno....umoran sam moram malo da se odmorim, programirajuci..woow napisao sam 652 linije
8:57 PM 12/7/2001 ...

Evo me nazad opet
8:59 PM 12/7/2001 -- vidis koliko mi je trebalo da se odmorim :)


Primjeti kako ovaj zadnji program nema provjeru za buffer overflow.. mozda mu i netreba jer
ja mislim da nije moguce sa konzole unijeti vise od 512 karaktera bez pritiska na Enter...samo malo
da provjerim..evo Xp mi neda da upisem vise od 127 cccc.
Pod linuxom je moguce preko pipe-a ovo zaobici ...tj . ako se i pod linuxom nemoze ukucati vise od 512 char..
onda mozes ovo

#cat *.* | ./nas_prog

Normalno ovo ces uraditi u nekom direktoriju gdje ima puno velkih fajlova....
cat *.* ce da ispise sadrzaj svih fajlova u dir-u, a | je pipe koji govori da sav taj izlaz
treba da se preusmjeri u ./nas_prog ... i jadnik ce da crkne.:) normalno samo ako prima parametre...

Ja mislim da je ovo dovoljno za ovaj prvi put;EOF


Evo me opet...ovaj put nesto ranije ...to nam sad nije vazno nego da se mi bacimo na C. [11:33 AM 12/9/2001]


Idemo sa jednim programom.

/*
	Program sa kojim idemo. :)
	by Sleeping Pig() 2001 (c) CopyLeft.
*/

int main(int argc, char *argv[]){
	printf("Pozdrav od %s",argv[0]);
	return 0;
}

Hmmmm... ovaj pravo cudan program ...siguran sam da si ovakvo nesto vidio bezbroj puta...

/*
*/	komentari.. :)

int main(int argc,char *argv[]) - je linija koja definise nasu glavnu "main" funkciju i njena dva parametra..
ovo te sigurno malo zbunjuje jer ko ce da proslijedi vrijednosti ovoj funkciji ??
posto se ona "automatski" poziva .. e pa ovo nije u potpunosti tacno jer je poziva OPERATIVNI SISTEM !! , YES
I ako je poziva OS onda ce on da popuni ove vrijednosti a one su :

int argc -- ili variabla tipa "int" koja cuva broj argumenata prosliedjenih nasem programu (ARGument Count)
char *argv[] -- ili niz stringova koji cuva vrijednosti tih argumenata (ARGument Values)

napomena: argv[0] je uvjek lokacija naseg programa :)

primjer :

kada pokrenemo ovaj gore prog. dobijemo nesto ovako:

./labla
Pozdrav od labla
/home/tux/

Ok da malo zakomplikuemo, recimo da hoces da upises nesto ovako ..


./labla ABCDEF

	/home/tux/LABLA.EXE misli da si upisao 'ABCDEF' kao parametar ..
/home/tux/

Ok da napisemo program za ovo :


/*
	das labla programm
*/

int main(int argc, char *argv[]){
	if (argc > 1) {
		printf("\n\t %s misli da si upisao '%s' kao parametar ..\n",argv[0],argv[1]);
	} else {
		printf("Pogresan broj parametara!\n");
	}
}


Malo eksperimentisi i vidjet ces nesto pravo zanimljivo ...to ostavljam kao vjezbu :)
U ovom primjeru smo ubacili provjeru jer neznamo sigurno da ce luzer upisati neki parametar
a nezelimo da se nas cool progy srusi jer je pokusao da procita nesto sto nepostoji...
zato smo ubacili onaj if koji provjerava dali ima vise od jednog parametra...zasto vise od
jednog ...zato sto uvjek postoji jedan parametar a to je argv[0] koji cuva lokaciju progija
znaci ako luzer unese bar jos jedan parametar u command line-u ...argc ce biti vece od 1
i ako je vece od jedan ispisi taj parametar a ako nije vece od jedan onda upozori luzera !
sa porukom pogresan broj parametara. toliko jednostavno,.. idemo dalje

Da malo bolje ilustriram...

argv[0]                    argv[1]        argv[2]  argv[3]     argv[4]     ........itd....
     |                        |		    |         |           |
_____|__________________ _____|________ ____|_____ ___|__ ________|_________
/home/tux/linX/labla     Parametar_prvi Parametar2 param3 kako_si_mi_danas_?  ... itd....


---------
Jos kodova ,koji vam mogu mnogo pomoci prilikom pocetaka za c-om, mozete naci na nasoj stranici http://www.codelinux.com/sources/ odnosno http://www.codelinux.com/sources/c%20-%20tutorial/ .

/*

	ThE tutorial je konacno gotov, svim koderima ,linux-asima sretna nova 2002!@@! Do Sljedeceg susreta.)

*/
EOF
---------------------------------------
				                   http://ze.lugbih.org

							  Code Your Linux!
