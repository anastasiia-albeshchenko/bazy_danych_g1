# lab_05
## Zadanie 1
### a
``` sql
delete from postac where rodzaj='wiking' and nazwa <> 'Bjorn' order by data_ur asc limit 2;
```
### b
 krok 1 usunencie auto_incr
``` sql
alter table postac change id_postaci id_postaci int;
alter table postac modify id_postaci int;
```
 krok 2 usunencie klucza ob
``` sql
alter table walizka drop foreign key walizka_ibfk_1;
alter table izba drop foreign key izba_ibfk_1;
alter table przetwory drop foreign key przetwory_ibfk_2;
```
wracamy do 1 krok,
krok 3 usunencie klucza gl
``` sql
alter table postac drop primary key;
```
## Zadanie 2
### a
``` sql
alter table postac add column pesel char(11) first;
update postac set pesel='45637265437' + id_postaci;
```
dodajemy kl gl
``` sql
alter table postac add primary key(pesel);
```
### b
``` sql
alter table postac modify rodzaj enum('wiking','ptak','kobieta', 'serena');
```
### c
``` sql
INSERT INTO postac (pesel, id_postaci, nazwa, rodzaj, data_ur, wiek) VALUES ('95748392789', 4, 'Gertruda Nieszczera', 'serena', '1893-07-04', 76);
```
## Zadanie 3
### a
``` sql
update postac set statek='Samara' where nazwa like '%a%';
```
### b
``` sql
update statek set max_ladownosc=max_ladownosc * 0.7 where year(data_wodowania) between 1900 and 2020;
```
### c
``` sql
alter table postac add check (wiek <= 1000);
```
## Zadanie 4
### a
``` sql
alter table postac modify rodzaj enum('wiking','ptak','kobieta', 'serena', 'węz');
insert into postac (pesel, id_postaci, nazwa, rodzaj, data_ur, wiek) values('95748392341', 5, 'Loko', 'węz', '1000-01-01', 843);
```
### b
``` sql
insert into marynarz select * from postac where statek is not null;
```
### c
``` sql
alter table marynarz add primary key(pesel);
alter table marynarz add foreign key(statek) references statek(nazwa_statku);
```
## Zadanie 5
### a
``` sql
delete from postac where statek is not null;
```
### b
``` sql
delete from postac where rodzaj='wiking' and nazwa='Astrid';
```
### c
``` sql
delete from statek;
```
### d
``` sql
drop table statek;
alter table postac drop foreign key postac_ibfk_1;
alter table marynarz drop foreign key marynarz_ibfk_1;
```
### e
``` sql
create table zwierz (id int primary key auto_increment, nazwa varchar(40), wiek int);
```
### f
``` sql
insert into zwierz (id, nazwa, wiek) select id_postaci, nazwa, wiek from postac;
```

