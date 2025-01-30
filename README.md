**1. Найдите номер модели, скорость и размер жесткого диска для всех ПК стоимостью менее 500 дол. Вывести: model, speed и hd.**
```
SELECT model, speed, hd  
FROM pc  
WHERE price < 500;    
```
---

**2. Найдите производителей принтеров. Вывести: maker.**
```
SELECT DISTINCT maker
FROM product
WHERE type = 'Printer';   
```
---

**3. Найдите номер модели, объем памяти и размеры экранов ПК-блокнотов, цена которых превышает 1000 дол.**
```
SELECT model, ram, screen
FROM laptop
WHERE price > 1000;   
```
---

**4. Найдите все записи таблицы Printer для цветных принтеров.**
```
SELECT * 
FROM printer
WHERE color = 'y'; 
```
---
