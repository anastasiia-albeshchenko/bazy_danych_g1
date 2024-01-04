# lab_04
## Zadanie 1
### 1
``` sql
 create table postac(
     id_postaci int  primary key auto_increment,
     nazwa varchar(40),
     rodzaj enum('wiking', 'ptak', 'kobieta'),
     data_ur date,
     wiek int unsigned);
```
### 2
``` sql
insert into postac values(default, 'Bjorn', 'wiking', '1700-11-09', 413);
```
### 3 
``` sql
update postac set wiek=88 where id_postac =3;
```
## Zadanie 2
### 1
``` sql
create table walizka (
    id_walizki int primary key,
    pojemnosc int unsigned,
    kolor enum('rozowy', 'czerwony', 'teczowy', 'zolty'),
    id_wlasciciela int,
    foreign (id_wlasciciela) references postac(id_postaci) on delete cascade);
```
### 2
```sql
alter table walizka alter column kolor set default 'rozowy';
```
### 3
``` sql
insert into walizka (pojemnosc, kolor, id_wlasciciela) values('50', 'czerwony',
(select id_postaci from postac where id_postaci = 1));
```
## Zadanie 3
### 1
``` sql
create table Izba (
    adres_budynku varchar(255),
    nazwa_izby varchar(255),
    metraz decimaL(10, 2) unsigned,
    wlasciciel int,
    primary key(adres_budynku,nazwa_izby),
    foreign key(wlasciciel) references postac(id_postaci) on delete set null);```
### 2
``` sql
alter table izba add column kolor varchar(100) default 'czarny' after matraz;
```
### 3 
``` sql
insert into izba(adres_budynku, nazwa_izby) value('warszawska','spizarnia');
## Zadanie 4
### 1 
``` sql
CREATE TABLE Przetwory (
    id_przetworu INT PRIMARY KEY AUTO_INCREMENT,
    rok_produkcji SMALLINT DEFAULT '1654',
    id_wykonawcy INT DEFAULT NULL,
    zawartosc VARCHAR(40),
    dodatek VARCHAR(60) DEFAULT 'papryczka chilli',
    id_konsumenta INT,
    FOREIGN KEY (id_wykonawcy) REFERENCES Postac(id_postac) ON DELETE SET NULL,
    FOREIGN KEY (id_konsumenta) REFERENCES Postac(id_postac)) ON DELETE SET NULL;
```
### 2
INSERT INTO przetwory(zawartosc, dodatek) values('bigos','papryczka chilli');
## Zadanie 5
### 1
INSERT INTO postac(nazwa, rodzaj, wiek) values('Biron','wiking', '23');
INSERT INTO postac(nazwa, rodzaj, wiek) values('Anna','wiking', '69');
INSERT INTO postac(nazwa, rodzaj, wiek) values('Olif','wiking', '13');
### 2 
``` sql
create table statek (
nazwa_statku varchar(50) primary key,
rodzaj_statku enum('galeon','wioslowy', 'wojskowy'),
data_wodowania date,
max_ladownosc int unsigned);
```
### 3
``` sql
insert into statek values('Kara', 'wojskowy', '2010-01-01', 13);
insert into statek values('Sant Marry', 'galeon', '2010-01-01', 13);
```
### 4 
``` sql
alter table postac add column funkcja varchar(40);
```
### 5 
``` sql
update postac set funkcja='kapitan' where nazwa='Bjorn';
```
### 6 
``` sql
alter table postac add foreign key(statek) references statek(nazwa_statku);
```
### 7
``` sql
updete postac set postac_statek = 'SantMarry' where nazwa = 'Drozda';
updete postac set postac_statek = 'kara' where nazwa = 'Biron';
```
### 8
``` sql
delete from izba where nazwa_izby = 'spizarnia';
```
### 9
``` sql
drop table izba;
```
















