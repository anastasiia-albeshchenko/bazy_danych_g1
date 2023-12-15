# lab_04
## Zadanie 1
### 1
``` sql
CREATE TABLE postac (
id_postaci INT PRIMARY KEY AUTO_INCREMENT,
nazwa VARCHAR(40),
rodzaj enum("wiking", "ptak", "kobieta"),
data_ur DATE,
wiek int unsigned);
```
### 2
``` sql
INSERT INTO postac VALUES(default, 'Bjorn', 'wiking', '1700-11-09', 413);
```
### 3 
``` sql
update postac set wiek=88 where id_postac =3;
```
## Zadanie 2
### 1
``` sql
CREATE TABLE walizka (
    id_walizki INT PRIMARY KEY AUTO_INCREMENT,
    pojemnosc INT UNSIGNED,
    kolor enum('rozowy', 'czerwony', 'teczowy', 'zolty'),
    id_wlasciciela int,
    FOREIGN KEY (id_wlasciciela) REFERENCES postac(id_postaci) ON DELETE CASCADE);
```
### 2
```sql
ALTER TABLE walizka ALTER kolor SET default 'rozowy';
```
### 3
``` sql
insert into walizka values(default, 50, 'rozowy', 2);
insert into walizka values(default, 70, 'czerwony', 1);
```
## Zadanie 3
### 1
``` sql
CREATE TABLE Izba (
    adres_budynku VARCHAR(255),
    nazwa_izby VARCHAR(255),
    metraz DECIMAL(10, 2) UNSIGNED,
    wlasciciel INT,
    PRIMARY KEY (adres_budynku, nazwa_izby),
    FOREIGN KEY (wlasciciel) REFERENCES Postac(id_postaci) ON DELETE SET NULL);
```
### 2

### 3

## Zadanie 4
### 1 
``` sql
CREATE TABLE Przetwory (
    id_przetworu INT PRIMARY KEY AUTO_INCREMENT,
    rok_produkcji SMALLINT DEFAULT 1654,
    id_wykonawcy INT DEFAULT NULL,
    zawartosc VARCHAR(40),
    dodatek VARCHAR(60) DEFAULT 'papryczka chilli',
    id_konsumenta INT,
    FOREIGN KEY (id_wykonawcy) REFERENCES Postac(id_postac),
    FOREIGN KEY (id_konsumenta) REFERENCES Postac(id_postac));
```
### 2

## Zadanie 5
### 1

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
insert into statek values('Santa Maria', 'galeon', '2010-01-01', 13);
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
















