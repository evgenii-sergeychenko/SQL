### SQL exercises (sql-ex.ru)
---

**1. Найдите номер модели, скорость и размер жесткого диска для всех ПК стоимостью менее 500 дол. Вывести: model, speed и hd.**
```
SELECT model, speed, hd  
FROM pc  
WHERE price < 500;    
```

**2. Найдите производителей принтеров. Вывести: maker.**
```
SELECT DISTINCT maker
FROM product
WHERE type = 'Printer';   
```

**3. Найдите номер модели, объем памяти и размеры экранов ПК-блокнотов, цена которых превышает 1000 дол.**
```
SELECT model, ram, screen
FROM laptop
WHERE price > 1000;   
```

**4. Найдите все записи таблицы Printer для цветных принтеров.**
```
SELECT * 
FROM printer
WHERE color = 'y'; 
```

**5. Найдите номер модели, скорость и размер жесткого диска ПК, имеющих 12x или 24x CD и цену менее 600 дол.**
```
SELECT model, speed, hd
FROM pc
WHERE cd IN ('12x', '24x')
         AND price < 600;
```

**6. Для каждого производителя, выпускающего ПК-блокноты c объёмом жесткого диска не менее 10 Гбайт, найти скорости таких ПК-блокнотов. Вывод: производитель, скорость.**
```
SELECT DISTINCT product.maker, laptop.speed
FROM product
JOIN laptop ON product.model = laptop.model
WHERE hd >= 10;
```

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

**9. Найдите производителей ПК с процессором не менее 450 Мгц. Вывести: Maker.**
```
SELECT DISTINCT product.maker
FROM product
JOIN pc ON product.model = pc.model
WHERE speed >= 450;
```

**10. Найдите модели принтеров, имеющих самую высокую цену. Вывести: model, price.**
```
SELECT model, price
FROM printer
WHERE price = (SELECT MAX(price)
               FROM printer);
```

**11. Найдите среднюю скорость ПК.**
```
SELECT AVG(speed)
FROM pc;
```

**12. Найдите среднюю скорость ПК-блокнотов, цена которых превышает 1000 дол.**
```
SELECT AVG(speed)
FROM laptop
WHERE price > 1000;
```

**13. Найдите среднюю скорость ПК, выпущенных производителем A.**
```
SELECT AVG(speed)
FROM pc
JOIN product ON pc.model = product.model
WHERE product.maker = 'A';
```

**14. Найдите класс, имя и страну для кораблей из таблицы Ships, имеющих не менее 10 орудий.**
```
SELECT ships.class, ships.name, classes.country
FROM ships
JOIN classes ON ships.class = classes.class
WHERE numGuns >= 10;
```

**15. Найдите размеры жестких дисков, совпадающих у двух и более PC. Вывести: HD.**
```
SELECT hd
FROM pc
GROUP BY hd
HAVING COUNT(hd) >= 2;
```

**16. Найдите пары моделей PC, имеющих одинаковые скорость и RAM. В результате каждая пара указывается только один раз, т.е. (i,j), но не (j,i), Порядок вывода: модель с большим номером, модель с меньшим номером, скорость и RAM.**
```
SELECT DISTINCT pc.model, pc1.model, pc.speed, pc.ram
FROM pc
JOIN pc AS pc1 ON pc.model > pc1.model
               AND pc.model <> pc1.model
               AND pc.speed = pc1.speed
               AND pc.ram = pc1.ram;
```

**17. Найдите модели ПК-блокнотов, скорость которых меньше скорости каждого из ПК. Вывести: type, model, speed.**
```
SELECT DISTINCT product.type, laptop.model, laptop.speed
FROM product
JOIN laptop ON product.model = laptop.model
WHERE laptop.speed < ALL (SELECT speed
                          FROM pc);
```

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

**19. Для каждого производителя, имеющего модели в таблице Laptop, найдите средний размер экрана выпускаемых им ПК-блокнотов. Вывести: maker, средний размер экрана.**
```
SELECT DISTINCT product.maker, AVG(screen)
FROM product
JOIN laptop ON product.model = laptop.model
GROUP BY product.maker;
```

**20. Найдите производителей, выпускающих по меньшей мере три различных модели ПК. Вывести: Maker, число моделей ПК.**
```
SELECT DISTINCT maker, COUNT(model)
FROM product
GROUP BY maker
HAVING COUNT(model) >= 3;
```

**21. Найдите максимальную цену ПК, выпускаемых каждым производителем, у которого есть модели в таблице PC. Вывести: maker, максимальная цен.**
```
SELECT DISTINCT product.maker, MAX(price)
FROM product
JOIN pc ON product.model = pc.model
GROUP BY product.maker;
```

**22. Для каждого значения скорости ПК, превышающего 600 МГц, определите среднюю цену ПК с такой же скоростью. Вывести: speed, средняя цена.**
```
SELECT speed, AVG(price)
FROM pc
WHERE speed > 600
GROUP BY speed;
```

**23. Найдите производителей, которые производили бы как ПК со скоростью не менее 750 МГц, так и ПК-блокноты со скоростью не менее 750 МГц. Вывести: Maker.**
```
SELECT product.maker
FROM product
JOIN pc ON product.model = pc.model
WHERE pc.speed >= 750

INTERSECT

SELECT product.maker
FROM product
JOIN laptop ON product.model = laptop.model
WHERE laptop.speed >= 750;
```

**24. Перечислите номера моделей любых типов, имеющих самую высокую цену по всей имеющейся в базе данных продукции.**
```
SELECT model
FROM (SELECT model, price FROM pc
      UNION
      SELECT model, price FROM laptop
      UNION
      SELECT model, price FROM printer) AS S
      WHERE S.price = (SELECT MAX(X.price)
                       FROM (SELECT price FROM pc                         
                             UNION
                             SELECT price FROM laptop                           
                             UNION
                             SELECT price FROM printer) AS X);
```

---
---

### SQL Academy
---

**1. Вывести имена всех людей, которые есть в базе данных авиакомпаний.**
```
SELECT name
FROM passenger;
```

**2. Вывести названия всеx авиакомпаний.**
```
SELECT name
FROM company;
```

**3. Вывести все рейсы, совершенные из Москвы.**
```
SELECT *
FROM trip
WHERE town_from = 'Moscow';
```

**4. Вывести имена людей, которые заканчиваются на "man".**
```
SELECT name
FROM passenger
WHERE name LIKE '%man';
```

**5. Вывести количество рейсов, совершенных на TU-134.**
```
SELECT COUNT(*) AS count
FROM trip
WHERE plane = 'TU-134';
```

**6. Какие компании совершали перелеты на Boeing.**
```
SELECT DISTINCT name
FROM company
JOIN trip ON company.id = trip.company
WHERE plane = 'Boeing';
```

**7. Вывести все названия самолётов, на которых можно улететь в Москву (Moscow).**
```
SELECT DISTINCT plane
FROM trip
WHERE town_to = 'Moscow';
```

**8. В какие города можно улететь из Парижа (Paris) и сколько времени это займёт?**
```
SELECT town_to, TIMEDIFF(time_in, time_out) AS flight_time
FROM trip
WHERE town_from = 'Paris';
```

**9. Какие компании организуют перелеты из Владивостока (Vladivostok)?**
```
SELECT company.name
FROM company
JOIN trip ON company.id = trip.company
WHERE town_from = 'Vladivostok';
```

**10. Вывести вылеты, совершенные с 10 ч. по 14 ч. 1 января 1900 г.**
```
SELECT *
FROM trip
WHERE time_out BETWEEN '1900-01-01 10:00:00.000' AND '1900-01-01 14:00:00.000';
```
