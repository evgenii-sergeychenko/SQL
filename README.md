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
