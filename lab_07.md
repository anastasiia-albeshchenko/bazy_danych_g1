# lab_07
## Zadanie 1
### 1
``` sql
select avg(waga) from kreatura where rodzaj='wiking';
```
### 2
``` sql
 select rodzaj, avg(waga), count(*) from kreatura group by rodzaj;
```
### 3 
``` sql
select year(curdate()) -  year(dataUr) as wiek from kreatura group by rodzaj;
```
## Zadanie 2
### 1
``` sql
select rodzaj, sum(waga) from zasob group by rodzaj;
```
### 2
``` sql
select rodzaj, avg(waga) from zasob where ilosc >= 4 group by rodzaj having sum(waga) > 10;
```
### 3 
``` sql

```
## Zadanie 3
### 1
``` sql

```
### 2
``` sql

```
### 3 
left join + warunek z null
``` sql
select k.nazwa, e.idZasobu, z.nazwa, e. ilosc from kreatura k
left join ekwipunek e on k.idKreatury = e.idKreatury left join zasob z on e.idZasobu=z.idZasobu;
select k.nazwa, e.idZasobu, k.nazwa, e.ilosc from kreatura k
left join ekwipunek e on k.idKreatury = e.idKreatury where e.idKreatury is null;
```
lub podzapytanie
``` sql
select nazwa, idKreatury from kreatura
where idKreatury not in (select distinct idKreatury from ekwipunek where idKreatury is not null);
select distinct idKreatury from ekwipunek;

```
## Zadanie 4
### 1
``` sql

```
### 2
``` sql
select k.nazwa, k.dataUr, z.rodzaj from kreatura k inner join ekwipunek e on k.idKreatury=e.idKreatury 
inner join zasob z on e.idZasobu=z.idZasobu where z.rodzaj='jedzenie' order by k.dataUr desc limit 5;
```
### 3 
``` sql
select concat(k1.nazwa, '-', k2.nazwa) from kreatura k1 inner join kreatura k2 
on k1.idKreatury-k2.idKreatury = 5;
```
lub tak
``` sql
select concat(k1.nazwa, '-', k2.nazwa) from kreatura k1 inner join kreatura k2 
on abs(k1.idKreatury-k2.idKreatury) = 5;
```
## Zadanie 5
### 1
``` sql
 select k.rodzaj, avg(e.ilosc * z.waga) from kreatura k
 inner join ekwipunek e on k.idKreatury = e.idKreatury inner join zasob z 
 on e.idZasobu=z.idZasobu where k.rodzaj not in ('malpa', 'waz') and e.ilosc < 30 group by rodzaj;
```
### 2
``` sql
 select k.rodzaj, k.nazwa, n.najstarsza, n.najmlodsza from 
 (select rodzaj, min(dataUr) najstarsza, max(dataUr) najmlodsza
 from kreatura group by rodzaj) n, kreatura k where n.najstarsza = k.dataUr or n.najmlodsza=k.dataUr;
```
