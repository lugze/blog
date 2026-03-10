---
layout: post
title:  "Sortiranje nizova u Pascalu - maturski rad"
author: grungy
date:   2002-06-01 12:00:00 +0100
categories: blog
---

Opca gimnazija Zenica, 2002. god.

Maturski rad iz informatike na temu: "Sortiranje nizova u Pascalu"

Ucenik: Nedim Hadzimahmutovic, V-2, grungy@linux.org.ba

Mentor: Seno Pilic

## Sadrzaj

1. Uvod
2. Uvod u programiranje i informatiku
3. Uvod u pascal
4. Sintaksa
   - Struktura programa i Write funkcija
   - Readln funkcija
   - Osnovni tipovi podataka
   - Pridruzivanje
5. Sortiranje nizova i algoritmi za sortiranje

---

## 1. Uvod u programiranje i informatiku

Programiranje je slozen proces. U osnovi predstavlja proces kreiranja niza (skupa) logickih koraka s ciljem rijesavanja odredjenog problema. Ovaj niz koraka naziva se program.

Optimalni koraci kod razvoja programa:

1. Analiza problema
2. Izbor rijesenja
3. Implementacija rijesenja
4. Testiranje.

U procesu programiranja covjek koristi programski jezik koji u osnovi predstavlja nacin komunikacije izmedju covjeka i racunara. Termin koji je veoma vazan prilikom ovog procesa je "kompajler" (kompilator, eng. compiler). Kompajler je program koji prevodi instrukcije koje pise programer u formu citljivu kompijuteru (masinski jezik). Zaklucujemo, da je uvijek potrebno reci kompjuteru kako ce da nesto uradi i kompjuter ce to slijepo uraditi bez postavljanja pitanja, a jezik koji koristimo prilikom te komunikacije (covjek-racunar) je programski jezik. Dakle, programer = ucitelj masine. Masina je u stanju uraditi samo onoliko koliko programer moze da prenese na masinu, drugim rijecima: sposobnost masine zavisi od sposobnosti programera.

Neko ce reci : "Napravi program pomocu kojeg ce kompijuter letjeti".

To je svakako moguce, ako bi uspjeli napraviti komad hardvera koji ce podici kompijuter i to spojili sa kompijuterom onda bi stvarno napravili program koji ce analizirati okruzenje i omoguciti kompijuteru da leti. Ovo bi bilo moguce samo uz odgovarajuci hardver. Samo sto bi se to drugacije zvalo "Avion kojeg upravlja kompijuter" a ne "Kompijuter koji leti"

Da ponovim, programiranje je detaljno davanje instrukcija kompijuteru, nepostoji ni jedan korak koji kompijuter moze sam da uradi.(te instrukcije ostaju zapisane i nemoraju se unositi ponovo, potrebno je samo pokrenuti taj program,tj. instrukcije).

Kompijuter nemoze proizvesti nista novo, moze uraditi samo ono sto sto mu covjek moze i zna da naredi, moze analizirati ali nema moc da predpostavi povezanost ili tacnost, moze samo da asistira covjeka u radu sa necim vec poznatim. (predhodno definiranim)

Kompijuter se moze smatrati kako mehanizam na principu akcija - reakcija. Covjek uvjek pocne prvi davajuci "akciju" na koju kompijuter reaguje samo ako je dizajniran za to i ako je prepozna.

Zamislite ovaj problem:

Imamo dvije case boje, nazovimo ih Casa A i Casa B. Casa A ima crvenu boju a Casa B ima plavu boju. Problem je kako zamjeniti sadrzaj casa? Kako smjestiti plavu boju u Casu A a crvenu u Casu B ?

Nakon malo razmisljanja dolazi nam rijesenje a to je koristenje pomocne case C

Logicki niz koraka (algoritam) koji cemo slijediti je

1. premjesti sadrzaj case B (ili A ) u casu C
2. posto je casa B prazna u nju premjesti sadrzaj case A
3. posto je sada casa A prazna u nju premjesti sadrzaj case C
4. Kraj

Tako smo dobili zamjenu sadrzaja.

Ovo isto se moze uraditi i u pascalu, samo sto necemo koristiti case nego Variable i necemo koristiti boju nego brojeve koji ce oznacavati neku boju.

Ovaj problem se moze ovako postaviti:

Napisati program (u pascalu) koji ce zamijeniti sadrzaj variable A i B tipa byte. (Variabla - promjenljiva, mjesto gdje mozemo cuvati odredjenu kolicinu podataka)

```pascal
var
a,b : byte;
c : byte; {pomocna variabla}
begin
a := 5;
b := 9;

c := a;
a := b;
b := c;
end.
```

Izgled "programa" koji rade istu stvar u razlicitim programskim jezicima:

Napisati program koji ispisuje "Kako si ?" na terminal (konzolu).

**Pascal:**

```pascal
Program Ispisi_Nesto_Na_Konzolu;
Begin
Writeln('Kako si ?');
End.
```

**QBasic:**

```basic
PRINT "Kako si ?"
```

**C:**

```c
#include<stdio.h>
void main(void){
printf("Kako si ?\n");
}
```

**Perl:**

```perl
#!usr/bin/perl
printf("Kako si ?\n");
```

**PHP:**

```php
<?php
echo "Kako si ?\n";
?>
```

**TASM (Borland Turbo Assembler):**

```asm
.MODEL TINY
.STACK
.DATA
nesto db "Kako si ?"
.CODE
main:
MOV AX,SEG nesto
MOV DS,AX

MOV DX,OFFSET nesto
MOV AH,09h
INT 21h

MOV AH,4Ch
INT 21h
ENDS
end main
```

Ono sto nas zanima na pocetku ucenja nekog programskog jezika jeste SINTAKSA i nacin na koji programski jezik rukuje sa podatcima, tome jos dodamo malo logike i spremni smo da pisemo programe.

## 4. Sintaksa

Sintaksa nekog programskog jezika je skup pravila koja se moraju postovati da bi pisali programe za taj programski jezik.

Kostur najjednostavnijeg pascal programa:

```pascal
Program Ime_Programa;
Begin
End.
```

Prvo pravilo je to, dakle da svaki program mora da pocne sa kljucnom rijecju "Program" poslije koje treba da se stavi vazece ime programa.

Svaka komanda u Pascalu mora da zavrsava sa ";" izuzetci su: Zadnji End u programu, Var, Type, Begin, Const... i drugi, koje cemo kasnije analizirati.

Dozvoljena imena bilo variabli, konstanti, tipova podataka, imena programa, imena procedura i funkcija, itd. su samo ona koja pocinju sa nekim od slova (malih ili velkih), mogu sadrzati brojeve i znak "_", nesmiju imati razmak " " i nesmiju se vise puta upotrebljavati.

Napomena: Pascal ne razlikuje velika i mala slova tako da variabla broj i BROJ su identicne i pascal ih smatra istom variablom. (broj = broJ = BrOj= Broj)

### a. Struktura programa i Write funkcija

```pascal
Program Ispisi_Hello;   {Program koji ispisuje Hello}
Begin                   { Pocetak programa }
Write('Hello');         { Jedina komanda }
End.                    { Kraj programa}
```

Ovaj program ce ispisati Hello na ekran.

Write ili WriteLn se koristi za ispis na ekran. Razlika izmedju Write i WriteLn je u tome sto nakon ispisa Write ne prelazi u novi red dok WriteLn prelazi.

```pascal
Program Testiraj_Write;
Begin
Write('Prva linija ');
Write('Druga linija ');
WriteLn('Treca linija ');
WriteLn('Cetvrta linija ');
End.
```

Izlaz:

```
Prva linija Druga linija Treca linija
Cetvrta linija
```

Pascal podrzava 4 osnovne matematicke operacije nad brojcanim konstantama: + sabiranje, - oduzimanje, * mnozenje, / djeljenje.

### b. Readln funkcija

ReadLn (read line - citaj liniju)

Procedura koju koristimo za "unos" podataka sa tastature jeste Read ili ReadLn.

```pascal
Program moj_prvi_program_sa_readln;
var
ime : String;
Begin
Write('Kako se zoves ? ');
Readln(ime);
Writeln('HEJ! da se ti slucajno ne zoves ',ime,' ??');
End.
```

Izlaz:

```
Kako se zoves ? Mirza
HEJ! da se ti slucajno ne zoves Mirza ??
```

### c. Osnovni tipovi podataka

Numericki (brojcani):

- Byte : 0..255
- Word : 0..65535
- ShortInt: -128..127
- Integer : -32768..32767
- LongInt : -2147483648..2147483647

Simbolicki:

- Char
- String

### d. Pridruzivanje

To je u biti smjestanje neke konstante ili sadrzaja neke druge variable unutar neke variable. Za to se koristi `:=`, a ne `=`.

```pascal
Program moj_program2;
Var
broj1, broj2, zbir : byte;
Begin
broj1 := 5;
broj2 := 11;
zbir := broj1 + broj2;
Writeln(zbir);
End.
```

Izlaz: `16`

## 5. Sortiranje nizova

### Pronalazenje najmanjeg ili najveceg broja u nizu

```pascal
Program najveci_manji;
Var
najv,najm,temp : Word;
Begin
najv := 0;
najm := (MaxInt*2)+1;
Writeln('Za kraj unosa unesite 0 ..');
repeat
  Write('Unesite broj : ');
  Readln(temp);
  if temp > najv then najv := temp;
  if temp < najm then najm := temp;
until temp = 0;
Writeln('Najveci broj je : ',najv);
Writeln('Najmanji broj je : ',najm);
Readln;
End.
```

### Sortiranje niza brojeva

```pascal
Program sort_niz;
const
  max = 50;
type
  MojNiz = Array[0..max] of Word;
Var
  niz : MojNiz;
  broj, trenutni_index, i : Word;
  kraj : Boolean;
Begin
  Writeln('Unesite brojeve (za kraj 0) : ');
  trenutni_index := 0;
  repeat
    inc(trenutni_index);
    Write('Broj : ');
    Readln(broj);
    niz[trenutni_index] := broj;
    niz[0] := trenutni_index;
  until (broj = 0) or (trenutni_index = max);
  Writeln('Broj unesenih elemenata : ',niz[0]);
  repeat
    kraj := true;
    For trenutni_index := 1 to niz[0] do begin
      For i := trenutni_index + 1 to niz[0] do begin
        if niz[trenutni_index] > niz[i] then begin
          broj := niz[trenutni_index];
          niz[trenutni_index] := niz[i];
          niz[i] := broj;
          kraj := false;
        end;
      end;
    end;
  until kraj;
  Writeln('Sortiran niz : ');
  For i := 1 to niz[0] do begin
    Write(niz[i]);
    if i mod 15 = 0 then Writeln;
  End;
  Readln;
End.
```

### QuickSort algoritam

QuickSort algoritam je rekurzivan i kao takav trosi dosta memorije.

```pascal
program QSort;
{$R-,S-}
const
  Max = Maxint div 2;
type
  TNiz = array[1..Max] of byte;
var
  niz : TNiz;
  i : Word;

procedure QuickSort(var A: Tniz; Lo, Hi: Word);

  procedure Sort(l, r: Word);
  var
    i, j, x, y: Word;
  begin
    i := l; j := r; x := a[(l+r) DIV 2];
    repeat
      while a[i] < x do i := i + 1;
      while x < a[j] do j := j - 1;
      if i <= j then begin
        y := a[i];
        a[i] := a[j];
        a[j] := y;
        i := i + 1;
        j := j - 1;
      end;
    until i > j;
    if l < j then Sort(l, j);
    if i < r then Sort(i, r);
  end;

begin
  Sort(Lo,Hi);
end;

begin
  Write('Generisem ',Max,' slucajnih brojeva...');
  Randomize;
  for i := 1 to Max do niz[i] := Random(254)+1;
  Writeln;
  Write('Sortiram...');
  QuickSort(niz, 1, Max);
  Writeln;
  for i := 1 to Max do Write(niz[i]:8);
end.
```

### Sortiranje pomocu datoteka

Algoritam koji slijedi je najsporiji od svih navedenih ali zato stedi memoriju i moze da sortira jako veliku kolicinu podataka.

Svi "podaci" se cuvaju u datotekama na disku. Algoritam koristi ukupno 4 datoteke (zajedno sa pocetnom), oznacimo ih sa P - pocetna, A, B i C su privremene.

Prvi korak je podjela P datoteke na A i B tako da jedna polovica P datoteke je smjestena u A a druga u B datoteku. Brojevi se prepisuju u datoteku A sve dok ne remete pravila sortiranja (od manjeg ka vecem ili obratno) kada naidje broj koji ne zadovoljava kriterije sortiranja on se zapisuje u B datoteku. Ovaj proces rastavljanja datoteke C na A i B, zatim spajanje A i B u C se ponavlja sve dok je moguce rastaviti C na dvije datoteke jer samo tada postoji broj koji nije na svom mjestu.

```pascal
while rastavi(c) do begin
  sastavi(a,b);
end;
```

Kada rastavi vrati false to znaci da nije u stanju da rastavi datoteku sto istovremeno oznacava kraj sortiranja.

### Bubble Sort algoritam

```pascal
Program bsort;
Uses Sorting;
Var
  niz : Tniz;

Procedure Sort;
Var
  i, j, temp : Integer;
  kraj : Boolean;
Begin
  Write('BSORT ...');
  prolaz := 0;
  For i := MAX-1 downto 1 do begin
    kraj := true;
    For j := 1 to i do begin
      if niz[j] > niz[j+1] then begin
        temp := niz[j];
        niz[j] := niz[j+1];
        niz[j+1] := temp;
        kraj := False;
      end;
      Inc(prolaz);
    end;
    if kraj then Break;
  end;
  Writeln(' Done.');
End;

Begin
  NizInit(niz);
  Sort;
  Writeln(prolaz);
  Readln;
End.
```

### Insertion Sort algoritam

```pascal
Program InsertionSort;
Const
  MAX = 10000;
Var
  niz : Array[1..MAX] of Integer;
  prolaz : Longint;

Procedure Sortiraj;
Var
  i, j, temp : Integer;
Begin
  Write('ISORT...');
  prolaz := 0;
  For i := 1 to MAX do begin
    j := i;
    While (j>1) and (niz[j]<niz[j-1]) do begin
      temp := niz[j];
      niz[j] := niz[j-1];
      niz[j-1] := temp;
      Dec(j);
      Inc(prolaz);
    end;
  end;
  Writeln(' Done.');
End;

Begin
  NizInit;
  Sortiraj;
  Writeln(prolaz);
  Readln;
End.
```

### Selection Sort algoritam

```pascal
Program SelectionSort;
Const
  MAX = 10000;
Var
  niz : Array[1..MAX] of Integer;
  prolaz : Longint;

Procedure Sortiraj;
Var
  i, j, temp : Integer;
Begin
  Write('SSORT... ');
  prolaz := 0;
  For i := 1 to MAX-1 do begin
    For j := i+1 to MAX do begin
      if niz[i] > niz[j] then begin
        temp := niz[j];
        niz[j] := niz[i];
        niz[i] := temp;
      end;
      Inc(prolaz);
    end;
  end;
  Writeln('Done.');
End;

Begin
  NizInit;
  Sortiraj;
  Writeln(prolaz);
  Readln;
End.
```

## Literatura

- PASCAL "AN INTRODUCTION TO THE ART AND SCIENCE OF PROGRAMMING", Fourth Edition by Walter Savitch
- Algoritmi u Programskom Jeziku C

---
*Izvor: Maturski rad, Opca gimnazija Zenica, 2002.*
