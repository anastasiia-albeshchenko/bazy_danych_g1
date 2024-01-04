# lab_08
## Zadanie 1
### 1
``` sql
create table kreatura as select * from wikingowie.kreatura;
create table uczestnicy as select * from wikingowie.uczestnicy;
create table etapy_wyprawy as select * from wikingowie.etapy_wyprawy;
create table sektor as select * from wikingowie.sektor;
create table wyprawa as select * from wikingowie.wyprawa;
```
### 2
``` sql
select k.nazwa from kreatura k left join wyprawa w 
on k.idKreatury=id_wyprawy where w.id_wyprawy is null ;
```
### 3
``` sql
select w.nazwa, sum(e.ilosc) from wyprawa w inner join ekwipunek e on w.id_wyprawy=e.idEkwipunku 
inner join uczestnicy u on w.id_wyprawy=u.id_wyprawy group by w.nazwa;
```
## Zadanie 2
### 1
``` sql
select w.nazwa, count(u.id_uczestnika), group_concat(k.nazwa) from wyprawa w inner join uczestnicy u on w.id_wyprawy=u.id_wyprawy inner join kreatura k 
on u.id_uczestnika=k.idKreatury group by w.nazwa;
```
### 2
``` sql
select w.id_wyprawy, ew.sektor, s.nazwa, ew.kolejnosc, w.data_rozpoczecia, k.nazwa from etapy_wyprawy ew 
inner join sektor s on ew.sektor=s.id_sektora inner join wyprawa w on w.id_wyprawy=ew.idWyprawy 
inner join kreatura k on k.idKreatury=w.kierownik order by w.data_rozpoczecia asc, ew.kolejnosc asc;

```
## Zadanie 3
### 1
``` sql
select s.nazwa, ifnull(count(ew.sektor), 0)
from sektor s left join etapy_wyprawy ew on s.id_sektora=ew.sektor
group by s.nazwa;
```
### 2
``` sql
select k.nazwa, if(count(u.id_uczestnika)> 0, 'prawda', 'falsz')
from uczestnicy u right join kreatura k on k.idKreatury=u.id_uczestnika group by k.nazwa;
```
## Zadanie 4
### 1
``` sql
select w.nazwa, sum(length(ew.dziennik)) from wyprawa w inner join etapy_wyprawy ew on w.id_wyprawy=ew.idWyprawy 
group by w.nazwa having sum(length(ew.dziennik))<400;
```
### 2
``` sql

```
## Zadanie 5
### 1
``` sql

```
