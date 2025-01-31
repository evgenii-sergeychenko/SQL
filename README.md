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

**11. Найдите среднюю скорость ПК.**
```
SELECT AVG(speed)
FROM pc;
```
---

**12. Найдите среднюю скорость ПК-блокнотов, цена которых превышает 1000 дол.**
```
SELECT AVG(speed)
FROM laptop
WHERE price > 1000;
```
---

**13. Найдите среднюю скорость ПК, выпущенных производителем A.**
```
SELECT AVG(speed)
FROM pc
JOIN product ON pc.model = product.model
WHERE product.maker = 'A';
```
---

**14. Найдите класс, имя и страну для кораблей из таблицы Ships, имеющих не менее 10 орудий.**
```
SELECT ships.class, ships.name, classes.country
FROM ships
JOIN classes ON ships.class = classes.class
WHERE numGuns >= 10;
```
---

**15. Найдите размеры жестких дисков, совпадающих у двух и более PC. Вывести: HD.**
```
SELECT hd
FROM pc
GROUP BY hd
HAVING COUNT(hd) >= 2;
```
---

**16. Найдите пары моделей PC, имеющих одинаковые скорость и RAM. В результате каждая пара указывается только один раз, т.е. (i,j), но не (j,i), Порядок вывода: модель с большим номером, модель с меньшим номером, скорость и RAM.**
```
SELECT DISTINCT pc.model, pc1.model, pc.speed, pc.ram
FROM pc
JOIN pc AS pc1 ON pc.model > pc1.model
               AND pc.model <> pc1.model
               AND pc.speed = pc1.speed
               AND pc.ram = pc1.ram;
```
---

**17. Найдите модели ПК-блокнотов, скорость которых меньше скорости каждого из ПК. Вывести: type, model, speed.**
```
SELECT DISTINCT product.type, laptop.model, laptop.speed
FROM product
JOIN laptop ON product.model = laptop.model
WHERE laptop.speed < ALL (SELECT speed
                          FROM pc);
```
---

**18. Найдите производителей самых дешевых цветных принтеров. Вывести: maker, price.**
```
SELECT DISTINCT product.maker, printer.price
FROM product
JOIN printer ON product.model = printer.model
WHERE price = (SELECT MIN(price)
               FROM printer
               WHERE color ='y')
AND color = 'y';
```
---
