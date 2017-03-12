---
layout: post
title:  "Setup Ubunutu Bash na Windows 10"
author: admir
date:   2017-03-12 09:47:10 +0100
categories: linux windows bash
---

### Instaliranje Linux podsistema na Windows

Bash na Ubuntu na Windows je ime linux podsistema koji je u beta fazi za Windows OS. 
Dozvoljava da se pokrene Linux na Windows-u bez programa za Virtualne Masine (VM).

Trenutno je ovaj update dostupan samo za one sa "Fast" opcijom na Windows Insider programu. 
Potrebno se prilkljuciti Windows Insider programu i postaviti Insider level na "Fast".

Ovako se mozete prikljuciti [Windows Insider programu.](http://www.pcworld.com/article/3038430/windows/how-to-join-the-windows-10-insider-preview-program.html)

Prvi korak je omoguciti  "Developer mode" u Windowsu. Ovo se moze postici tako sto otvorimo Settings -> Update & Security -> "For Developers".  
Kliknuti na "Developer mode" da bi se opcija oznacila.

![developer_mode-1.png]({{ site.url }}/assets/images/podesavanje-ubunutu-bash-na-windows-10/developer_mode-1.png)

Sada trebamo omoguciti Windows Subsystem za Linux. Otvorimo Contol Panel, zatim Programs i kliknuti na "Turn Windows Features On or Off". Potraziti opciju "Windows Subsystem for Linux" i oznaciti kvadratic pored opcije.

![2]({{ site.url }}/assets/images/podesavanje-ubunutu-bash-na-windows-10/2.png)

U slucaju da opcija "Windows Subsystem for Linux(Beta)" nije dostupna provjerite da li ste dio Windows Insider programa i da je update postavljen na "Fast", restartujte sistem, ili sacekajte para dana da opcija bude dostuona. Ponekad je potrebno da prodje i dva dana prije nego opcija bude dostupna nakon sto se ukljuci Developer mode. U svakom slucaju probajte par ovih opcija dok ne uspijete.

Nakon sto instalirate i restartujete sistem mozemo poceti podesavati Bash za Ubuntu na Windows-u.

Pocnite tako sto cete upisati "bash" u search box.

![3]({{ site.url }}/assets/images/podesavanje-ubunutu-bash-na-windows-10/3.png)

Dalje, slijedimo korake instalacije da postavimo Bash za Ubuntu na Windows.

![4]({{ site.url }}/assets/images/podesavanje-ubunutu-bash-na-windows-10/4.png)

Kada je to zavrseno, otvorite Start meni i upisite u search box  "Bash". Ovaj put ce imati Ubuntu logo.

![5]({{ site.url }}/assets/images/podesavanje-ubunutu-bash-na-windows-10/5.png)

Sada imate funkcionalnu Ubuntu Linux instalaciju pokrenutu na svojoj Windows masini!

![6]({{ site.url }}/assets/images/podesavanje-ubunutu-bash-na-windows-10/6.png)

Od ovog koraka mozete slijediti normalnu instalaciju Ruby, Rails i Database za Ubunutu Linux operativni sistem.
