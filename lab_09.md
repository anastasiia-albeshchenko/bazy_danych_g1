# lab_09
## Zadanie 1
```sql

delimiter //
create trigger kreatura_befor_insert 
before insert on kreatura 
for each row
begin 
  if new.waga <= 0
  then 
     set new.waga = 1; 
  end if; 
end
//
delimiter ;

```
## Zadanie 2

```sql
delimiter //
create trigger archiwum_wypraw 
before delete on wyprawa3
for each row
begin
     insert into archiwum_wypraw
	 select w.id_wyprawy, w.nazwa, w.data_rozpoczecia, w.data_zakonczenia, k.nazwa 
     from wyprawa3 w 
     inner join kreatura k on k.idKreatury=w.kierownik
	 where id_wyprawy = old.id_wyprawy; 
end

//
delimiter ;
```
## Zadanie 3
### 1
``` sql
delimiter //
create procedure eliksir_sily (in id int)
  begin
    update kreatura set udzwig = udzwig * 1.2 where idKreatury = id;
  end//
delimiter ;
```
### 2
``` sql
create function wielkie_litery (t text)
  returns text
  return upper(t);
```
## Zadanie 4
### 1
``` sql
create table system_alarmowy(
id_alarmu int primary key auto_increment,
wiadomosc text);
```
### 2
``` sql
delimiter //
create trigger system_alarmowy_after_insert on uczestnicy
  for each row
  begin
    if @tesciowa in
      (select id_uczestnika from uczestnicy where id_wyprawy=new.id_wyprawy)
    then
      set czy_tesc = true;
    end if;
    if @dziad in
      (select sektor from etapy_wyprawy where id_wyprawy=new.id_wyprawy)
    then
      set czy_dziad = true
    end if;

    if czy_tesc and czy_dziad then
      insert into system_alarmowy values(default, 'Tesciowa nadchodzi !!!', default);
    end if;
  end//
delimiter ;
```
