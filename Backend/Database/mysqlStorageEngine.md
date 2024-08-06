# MySQL Storage Engine

- posebnosti arhitekture relacijskog sustava za upravljanje bazom podataka MySQL je u tome što najniži sloj (`MySQL Storage Engine - MSE`) omogućava korištenje različitih modula za pristup podacima zapisanim na disku

![MySQL system arhitecture](https://sistemac.srce.hr/sites/sistemac.srce.hr/files/docs/2017/mysql-dbe-1.png)

- dostupnih, ujedno i najpopularnijih modula za MSE su
  - MyISAM
  - InnoDB
  - Memory
  - NDB
- moduli imaju određene prednosti, ali i nedostatke
  - u istoj bazi moguće je istovremeno koristiti različite MSE module za definiranje tablice - ako za takvo rješenje nema posebnih razloga, bolje je cijelu bazu izgraditi na istom MSE modulu
- različiti moduli mođusobno ne komuniciraju izravno, već to rade preko višeg sloja koji sadrži parser, optimizer i druge module za analizu i izvođenje SQL upita
  - komunikacija se izvodi preko sustava Storage API

## Usporedni prikaz karakteristika

![Usporedba nekoliko najpoznatijih MSE modula](https://sistemac.srce.hr/sites/sistemac.srce.hr/files/docs/2017/mysql-dbe-3.png)

### MyIsam

#### Napredna svojstva

- full-text indeksi
- kompresija podataka
- podrška za prostorno orijentirane tipove podataka

#### Nedostaci

- izostanak podrške za transakcije
- najmanji opseg zaključavanja podataka
- slaba obnovljivost podataka

#### Korištenje u rješenjima

- read-only orijentirana rješenja - kada se većina operacija odnosi samo na čitanje ili pretraživanje postojećih podataka

### InnoDB

#### Napredna svojstva

- ugrađena je većina naprednih mogućnosti koje se očukuju od relacijskih baza podataka
- podrška za korištenje transakcija
- zaključavanje resursa na razini slogova
- poboljšana otpornost na eventualne havarije sustava

### Memory

#### Napredna svojstva i ograničenja

- svi podaci kojima se pristupa nalaze se u RAM memoriji računala
- zbog orijentiranosti na korištenje RAM memorije računala, MSE donosi nekoliko bitnih ograničenja
  - podaci se gube nakon ponovnog pokretanja servera
  - ograničenost kapaciteta RAM memorije
  - nije podržan dio standardnih tipova podataka - tablice s takvim podacima se ne mogu implementirati izravno

### NDB

- namijenjen za korištenje u distribuiranim okruženjima s većim brojem servera
- kao i InnoDB podržava brojne napredne osobine podrazumijevane kod relacijskih baza

### Archive

- MSE moduli zasnovani na Archive tehnologiji namijenjeni su za spremanje i naknadni pristup vrlo velikoj količini neindeksiranih podataka (takozvane arhive podataka)
  - kako bi se smanjilo zauzeće prostora na diskovima, prilikom spremanja podataka izvodi se njihova automatska kompresija korištenjem zlib biblioteke

### Blackhole

- MSE modul omogućava pripremu tablica u koju vlastito rješenje može zapisivati podatke, ali tako da ti podaci stvarno ne budu nigdje trajno zapisani
  - zbog takve mogućnosti Blackhole može biti primjenjiv kod različitih (automatskih) oblika testiranja nekog projekta, gdje zapravo nema smisla trajno čuvati privremene testne podatke

### CSV

- kao što samo naziv znači - podaci se čuvaju u obliku tekstualnih tablica u CSV formatu (Comma-Separated Values)
  - tekstualno orijentranim podacima, kakvim se u praksi susreću tijekom ETL (Extract, Transform and Load) projekata
    - MySQL baza i ETL projekti
