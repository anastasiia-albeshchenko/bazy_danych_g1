### Lab_3_zadania_1.md
## 1
``` sql
lab_3_zadania_1.md
```
## 2
``` sql
select imie, nazwisko, (year(curdate()) - year(data_urodzenia)) , data_urodzenia from pracownik;
lub
select imie, nazwisko, 2024 - year(data_urodzenia) , data_urodzenia from pracownik;
```
## 3
``` sql
select d.nazwa, count(p.id_pracownika) as ilosc_pracownikow from dzial d
inner join pracownik p on d.id_dzialu=p.dzial group by d.nazwa;
```
## 4
``` sql
select k.nazwa_kategori, count(t.id_towaru) as ilosc_towaru from kategoria k 
inner join towar t on k.id_kategori=t.kategoria group by k.nazwa_kategori;
```
## 5
``` sql
select k.nazwa_kategori, group_concat(t.nazwa_towaru) from kategoria k 
inner join towar t on k.id_kategori=t.kategoria group by k.nazwa_kategori;```
## 6
``` sql
select round(avg(pensja), 2) from pracownik;
```
## 7
``` sql
select round(avg(pensja), 2) from pracownik where data_zatrudnienia < subdate(data_zatrudnienia, interval 5 year);
```
## 8
``` sql
select t.nazwa_towaru, p.towar, sum(p.ilosc) from towar t inner join pozycja_zamowienia p 
on t.id_towaru=p.towar group by p.towar order by sum(p.ilosc) desc limit 10;
 lub
select t.nazwa_towaru, count(p.towar) from towar t inner join pozycja_zamowienia p 
on t.id_towaru=p.towar group by p.towar order by count(p.towar) desc limit 10;
```
## 9
``` sql
select z.numer_zamowienia, sum(pz.ilosc*pz.cena)
from zamowienie z inner join pozycja_zamowienia pz on z.id_zamowienia=pz.zamowienie 
where quarter(z.data_zamowienia)=1 and year(z.data_zamowienia)=2017
group by z.numer_zamowienia;
```
## 10
``` sql
select p.imie, p.nazwisko, sum(pz.ilosc*pz.cena) from zamowienie z inner join pozycja_zamowienia pz on z.id_zamowienia=pz.zamowienie 
inner join pracownik p on p.id_pracownika=z.pracownik_id_pracownika
group by p.id_pracownika order by wartosc desc;
```
