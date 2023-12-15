# lad_06
## Zadanie 1
### 1
``` sql
create table kreatura as select * from wikingowie.kreatura;
create table zasob as select * from wikingowie.zasob;
create table ekwipunek as select * from wikingowie.ekwipunek;
```
### 2
``` sql
insert into zasob select* from wikingowie.zasob;
select * from zasob;
```
### 3
``` sql
select * from zasob where rodzaj = 'jedzenie';
```
### 4
``` sql
select idZasobu, ilosc from zasob where idZasobu=1 or idZasobu=3 or idZasobu=5;
select idZasobu, ilosc from zasob where idZasobu in (1, 3, 5) ;
```

## Zadanie 2
### 1
``` sql
insert into kreatura select * from wikingowie.kreatura;
select * from kreatura where not rodzaj='wiedzma' and waga >= 50;
```
### 2
``` sql
select * from zasob where waga >= 2 and waga<=5;
```
### 3
``` sql
select * from wikingowie.kreatura where nazwa like '%or%' and udzwig >=30 and udzwig <=70;
```
## Zadanie 3
### 1
``` sql
select * from zasob where month(dataPozyskania) between 7 and 8;
```
### 2
``` sql
select * from zasob order by waga asc;
```
### 3
``` sql
select * from kreatura where dataUr is not null order by dataUr asc limit 5 ;
```
## Zadanie 4
### 1
``` sql
select distinct rodzaj from zasob;
```
### 2
``` sql
select concat(nazwa, '-', rodzaj) as nazwa_i_rodzaj 
from kreatura where rodzaj like 'wi%';
```
### 3
``` sql
select nazwa, ilosc, waga, ilosc * waga as calkowita_waga from zasob
where year(dataPozyskania) between 2000 and 2007;
```
## Zadanie 5
### 1
``` sql
select nazwa, waga *0.7 as masa_jedzenia, waga * 0.3 as waga_odpadkow from kreatura;
```
### 2
``` sql
select * from zasob where rodzaj is null;
```
### 3
``` sql
select distinct rodzaj from zasob where nazwa like 'Ba%' or nazwa like '%os' order by rodzaj asc; 
```
