# lab_09
## Zadanie 1
```sql

DELIMITER //
CREATE TRIGGER before_insert_update_kreatura
BEFORE INSERT ON kreatura
FOR EACH ROW
BEGIN
    IF NEW.waga <= 0 THEN
        SET NEW.waga = 1;
    END IF;
END;
//
DELIMITER ;

```
## Zadanie 2

```sql
 CREATE TABLE archiwum_wypraw LIKE wyprawa;
 DESC archiwum_wypraw;
 ALTER TABLE archiwum_wypraw
 MODIFY COLUMN kierownik VARCHAR(1000);
 DELIMITER //
 CREATE TRIGGER wyprawa_przed_usunienciem
 BEFORE DELETE ON wyprawa
 FOR EACH ROW
 BEGIN
     INSERT INTO archiwum_wypraw (id_wyprawy, nazwa,
     data_rozpoczecia, data_zakonczenia, kierownik)
     SELECT w.id_wyprawy, w.nazwa, w.data_rozpoczecia, w.data_zakonczenia, k.nazwa
     FROM wyprawa w
     JOIN kreatura k ON k.idKreatury = w.kierownik
     WHERE id_wyprawy = OLD.id_wyprawy;
 END;
 //
 DELIMITER ;
```
