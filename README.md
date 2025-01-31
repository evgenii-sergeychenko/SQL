### SQL exercises (sql-ex.ru)
---

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

**5. Найдите номер модели, скорость и размер жесткого диска ПК, имеющих 12x или 24x CD и цену менее 600 дол.**
```
SELECT model, speed, hd
FROM pc
WHERE cd IN ('12x', '24x')
         AND price < 600;
```
---

**6. Для каждого производителя, выпускающего ПК-блокноты c объёмом жесткого диска не менее 10 Гбайт, найти скорости таких ПК-блокнотов. Вывод: производитель, скорость.**
```
SELECT DISTINCT product.maker, laptop.speed
FROM product
JOIN laptop ON product.model = laptop.model
WHERE hd >= 10;
```
---

**7. Найдите номера моделей и цены всех имеющихся в продаже продуктов (любого типа) производителя B (латинская буква).**
```
SELECT pc.model, pc.price
FROM pc
JOIN product ON pc.model = product.model
WHERE product.maker = 'B'
UNION
SELECT laptop.model, laptop.price
FROM laptop
JOIN product ON laptop.model = product.model
WHERE product.maker = 'B'
UNION
SELECT printer.model, printer.price
FROM printer
JOIN product ON printer.model = product.model
WHERE product.maker = 'B';
```
---

**8. Найдите производителя, выпускающего ПК, но не ПК-блокноты.**
```
SELECT maker
FROM product
WHERE type = 'PC'
EXCEPT
SELECT maker
FROM product
WHERE type = 'Laptop';
```
---

**9. Найдите производителей ПК с процессором не менее 450 Мгц. Вывести: Maker.**
```
SELECT DISTINCT product.maker
FROM product
JOIN pc ON product.model = pc.model
WHERE speed >= 450;
```
---

**10. Найдите модели принтеров, имеющих самую высокую цену. Вывести: model, price.**
```
SELECT model, price
FROM printer
WHERE price = (SELECT MAX(price)
               FROM printer);
```
---
