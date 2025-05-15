# Прохождение тренажера от SQL-EX.RU
<details>
<summary><b>Задание №1:</b> Найдите номер модели, скорость и размер жесткого диска для всех ПК стоимостью менее 500 дол. Вывести: model, speed и hd.</summary>
  
  ```mysql
SELECT model, speed, hd
FROM pc
WHERE price < 500
```

</details>
<details>
<summary><b>Задание №2:</b> Найдите производителей принтеров. Вывести: maker.</summary>
  
  ```mysql
SELECT DISTINCT maker
FROM product
WHERE type = 'Printer'
```

</details>
<details>
<summary><b>Задание №3:</b> Найдите номер модели, объем памяти и размеры экранов ПК-блокнотов, цена которых превышает 1000 дол.</summary>
  
  ```mysql
SELECT model, ram, screen
FROM laptop
WHERE price > 1000
```

</details>
<details>
<summary><b>Задание №4:</b> Найдите все записи таблицы Printer для цветных принтеров.</summary>
  
  ```mysql
SELECT *
FROM printer
WHERE color = 'y'
```

</details>
<details>
<summary><b>Задание №5:</b> Найдите номер модели, скорость и размер жесткого диска ПК, имеющих 12x или 24x CD и цену менее 600 дол.</summary>
  
  ```mysql
SELECT model, speed, hd
FROM pc
WHERE (cd = '12x' OR cd = '24x') AND price < 600
```

</details>
<details>
<summary><b>Задание №6:</b> Укажите производителя и скорость для тех ПК-блокнотов, которые имеют жесткий диск объемом не менее 10 Гбайт.</summary>
  
  ```mysql
SELECT DISTINCT maker, speed
FROM product
INNER JOIN laptop ON product.model = laptop.model
WHERE hd >= 10
```

</details>
<details>
<summary><b>Задание №7:</b> Найдите номера моделей и цены всех продуктов (любого типа), выпущенных производителем B (латинская буква).</summary>
  
  ```mysql
SELECT p.model, pc.price
FROM Product p
JOIN PC pc ON p.model = pc.model
WHERE p.maker = 'B'

UNION

SELECT p.model, l.price
FROM Product p
JOIN Laptop l ON p.model = l.model
WHERE p.maker = 'B'

UNION

SELECT p.model, pr.price
FROM Product p
JOIN Printer pr ON p.model = pr.model
WHERE p.maker = 'B'
```

</details>
<details>
<summary><b>Задание №8:</b> Найдите производителя, выпускающего ПК, но не ПК-блокноты.</summary>
  
  ```mysql
SELECT maker 
FROM Product
WHERE type = 'PC'

EXCEPT

SELECT maker
FROM Product
WHERE type = 'Laptop'
```

</details>
<details>
<summary><b>Задание №9:</b> Найдите производителей ПК с процессором не менее 450 Мгц. Вывести: Maker.</summary>
  
  ```mysql
SELECT DISTINCT maker
FROM product
INNER JOIN pc ON product.model = pc.model
WHERE pc.speed >= 450
```

</details>
<details>
<summary><b>Задание №10:</b> Найдите модели принтеров, имеющих самую высокую цену. Вывести: model, price.</summary>
  
  ```mysql
SELECT model, price
FROM printer
WHERE price = (SELECT MAX(price) FROM printer)
```

</details>
<details>
<summary><b>Задание №11:</b> Найдите среднюю скорость ПК.</summary>
  
  ```mysql
SELECT AVG(speed)
FROM pc
```

</details>
<details>
<summary><b>Задание №12:</b> Найдите среднюю скорость ПК-блокнотов, цена которых превышает 1000 дол.</summary>
  
  ```mysql
SELECT AVG(speed)
FROM laptop
WHERE price > 1000
```

</details>
<details>
<summary><b>Задание №13:</b> Найдите среднюю скорость ПК, выпущенных производителем A.</summary>
  
  ```mysql
SELECT AVG(speed)
FROM pc
INNER JOIN product ON pc.model = product.model
WHERE product.maker = 'A'
```

</details>
<details>
<summary><b>Задание №14:</b> Найдите класс, имя и страну для кораблей из таблицы Ships, имеющих не менее 10 орудий.</summary>
  
  ```mysql
SELECT ships.class, ships.name, classes.country
FROM classes
INNER JOIN ships ON classes.class = ships.class
WHERE classes.numGuns >= 10
```

</details>
<details>
<summary><b>Задание №15:</b> Найдите размеры жестких дисков, совпадающих у двух и более PC. Вывести: HD.</summary>
  
  ```mysql
SELECT hd
FROM pc
GROUP BY hd
HAVING COUNT(hd) >= 2
```

</details>
<details>
<summary><b>Задание №16:</b> Найдите пары моделей PC, имеющих одинаковые скорость и RAM. В результате каждая пара указывается только один раз, т.е. (i,j), но не (j,i). Порядок вывода: модель с большим номером, модель с меньшим номером, скорость и RAM.</summary>
  
  ```mysql
SELECT DISTINCT A.model AS model, B.model AS model, A.speed, A.ram
FROM PC AS A, PC B
WHERE A.speed = B.speed AND A.ram = B.ram AND A.model > B.model
```

</details>
<details>
<summary><b>Задание №17:</b> Найдите модели ПК-блокнотов, скорость которых меньше скорости каждого из ПК. Вывести: type, model, speed.</summary>
  
  ```mysql
SELECT DISTINCT product.type, l.model, l.speed
From laptop as l, product, pc
WHERE product.type = 'Laptop' AND l.speed < ALL (SELECT speed FROM pc)
```

</details>
<details>
<summary><b>Задание №18:</b> Найдите производителей самых дешевых цветных принтеров. Вывести: maker, price.</summary>
  
  ```mysql
SELECT DISTINCT maker, price
FROM product
INNER JOIN printer ON product.model = printer.model
WHERE price = (SELECT MIN(price) FROM printer WHERE color = 'y') AND color = 'y'
```

</details>
<details>
<summary><b>Задание №19:</b> Для каждого производителя, имеющего модели в таблице Laptop, найдите средний размер экрана выпускаемых им ПК-блокнотов. Вывести: maker, средний размер экрана.</summary>
  
  ```mysql
SELECT product.maker, AVG(laptop.screen)
FROM product
INNER JOIN laptop ON product.model = laptop.model
GROUP BY product.maker
```

</details>
<details>
<summary><b>Задание №20:</b> Найдите производителей, выпускающих по меньшей мере три различных модели ПК. Вывести: Maker, число моделей ПК.</summary>
  
  ```mysql
SELECT maker, COUNT(model)
FROM product
WHERE type = 'pc'
GROUP BY maker 
HAVING COUNT(model) >= 3
```

</details>
<details>
<summary><b>Задание №21:</b> Найдите максимальную цену ПК, выпускаемых каждым производителем, у которого есть модели в таблице PC. Вывести: maker, максимальная цена.</summary>
  
  ```mysql
SELECT maker, MAX(price)
FROM pc 
INNER JOIN product ON pc.model = product.model  
GROUP BY maker
```

</details>
<details>
<summary><b>Задание №22:</b> Для каждого значения скорости ПК, превышающего 600 МГц, определите среднюю цену ПК с такой же скоростью. Вывести: speed, средняя цена.</summary>
  
  ```mysql
SELECT speed, AVG(price)
FROM pc
WHERE speed > 600
GROUP BY speed
```

</details>
<details>
<summary><b>Задание №23:</b> Найдите производителей, которые производили бы как ПК со скоростью не менее 750 МГц, так и ПК-блокноты со скоростью не менее 750 МГц. Вывести: Maker.</summary>
  
  ```mysql
SELECT DISTINCT maker
FROM product
INNER JOIN laptop ON laptop.model = product.model
WHERE laptop.speed >= 750

INTERSECT

SELECT DISTINCT maker
FROM product
INNER JOIN pc ON pc.model = product.model
WHERE pc.speed >= 750
```

</details>
<details>
<summary><b>Задание №24:</b> Перечислите номера моделей любых типов, имеющих самую высокую цену по всей имеющейся в базе данных продукции.</summary>
  
  ```mysql
WITH max_price AS (
  SELECT MAX(price) AS price FROM (
    SELECT price FROM pc
    UNION ALL
    SELECT price FROM laptop
    UNION ALL
    SELECT price FROM printer
  ) AS all_prices
)

SELECT model 
FROM pc 
WHERE price = (SELECT price FROM max_price)

UNION

SELECT model 
FROM laptop 
WHERE price = (SELECT price FROM max_price)

UNION

SELECT model 
FROM printer 
WHERE price = (SELECT price FROM max_price)
```

</details>
<details>
<summary><b>Задание №25:</b> Найдите производителей принтеров, которые производят ПК с наименьшим объемом RAM и с самым быстрым процессором среди всех ПК, имеющих наименьший объем RAM. Вывести: Maker.</summary>
  
  ```mysql
SELECT DISTINCT product.maker
FROM product
INNER JOIN pc ON pc.model = product.model
WHERE pc.ram = (SELECT MIN(ram) FROM pc) AND pc.speed = (SELECT MAX(speed) FROM pc WHERE ram = (SELECT MIN(ram) FROM pc))

INTERSECT

SELECT maker
FROM product
WHERE type = 'printer'
```

</details>
<details>
<summary><b>Задание №26:</b> Найдите среднюю цену ПК и ПК-блокнотов, выпущенных производителем A (латинская буква). Вывести: одна общая средняя цена.</summary>
  
  ```mysql
SELECT AVG(price)
FROM (
  SELECT pc.price
  FROM product
  INNER JOIN pc ON pc.model = product.model
  WHERE product.maker = 'A'

  UNION ALL

  SELECT laptop.price
  FROM product
  INNER JOIN laptop ON laptop.model = product.model
  WHERE product.maker = 'A'
) as t
```

</details>
<details>
<summary><b>Задание №27:</b> Найдите средний размер диска ПК каждого из тех производителей, которые выпускают и принтеры. Вывести: maker, средний размер HD.</summary>
  
  ```mysql
SELECT product.maker, AVG(pc.hd)
FROM product
INNER JOIN pc ON pc.model = product.model
WHERE product.maker IN (
  SELECT maker
  FROM product
  WHERE type = 'printer'
)
GROUP BY product.maker
```

</details>
<details>
<summary><b>Задание №28:</b> Используя таблицу Product, определить количество производителей, выпускающих по одной модели.</summary>
  
  ```mysql
SELECT COUNT(*)
FROM (
  SELECT maker
  FROM product
  GROUP BY maker
  HAVING COUNT(*) = 1
) as t
```

</details>
<details>
<summary><b>Задание №29:</b> В предположении, что приход и расход денег на каждом пункте приема фиксируется не чаще одного раза в день [т.е. первичный ключ (пункт, дата)], написать запрос с выходными данными (пункт, дата, приход, расход). Использовать таблицы Income_o и Outcome_o.</summary>
  
  ```mysql
SELECT income_o.point, income_o.date, inc, out
FROM income_o
LEFT JOIN outcome_o ON income_o.point = outcome_o.point
AND income_o.date = outcome_o.date

UNION

SELECT outcome_o.point, outcome_o.date, inc, out
FROM income_o 
RIGHT JOIN outcome_o ON income_o.point = outcome_o.point
AND income_o.date = outcome_o.date
```

</details>
<details>
<summary><b>Задание №30:</b> В предположении, что приход и расход денег на каждом пункте приема фиксируется произвольное число раз (первичным ключом в таблицах является столбец code), требуется получить таблицу, в которой каждому пункту за каждую дату выполнения операций будет соответствовать одна строка. Вывод: point, date, суммарный расход пункта за день (out), суммарный приход пункта за день (inc). Отсутствующие значения считать неопределенными (NULL).</summary>
  
  ```mysql
WITH Inc AS (
    SELECT point, date, SUM(inc) AS suminc
    FROM Income
    GROUP BY point, date
),
Outc AS (
    SELECT point, date, SUM(out) AS sumout
    FROM Outcome
    GROUP BY point, date
)

SELECT 
    COALESCE(Inc.point, Outc.point) AS point,
    COALESCE(Inc.date, Outc.date) AS date,
    Outc.sumout,
    Inc.suminc
FROM Inc
FULL OUTER JOIN Outc ON Inc.point = Outc.point AND Inc.date = Outc.date
ORDER BY point, date
```

</details>
<details>
<summary><b>Задание №31:</b> Для классов кораблей, калибр орудий которых не менее 16 дюймов, укажите класс и страну.</summary>
  
  ```mysql
SELECT class, country
FROM Classes
WHERE bore >= 16
```

</details>
<details>
<summary><b>Задание №32:</b> Одной из характеристик корабля является половина куба калибра его главных орудий (mw). С точностью до 2 десятичных знаков определите среднее значение mw для кораблей каждой страны, у которой есть корабли в базе данных.</summary>
  
  ```mysql
WITH с AS (
    SELECT country, classes.class, bore, name
    FROM classes
    LEFT JOIN ships ON classes.class = ships.class

    UNION ALL

    SELECT DISTINCT country, class, bore, ship AS name
    FROM classes t1
    LEFT JOIN outcomes t2 ON t1.class = t2.ship
    WHERE ship = class AND ship NOT IN (SELECT name FROM ships)
)

SELECT 
    country, 
    CAST(AVG(POWER(bore, 3) / 2.0) AS numeric(6, 2)) AS weight
FROM с
WHERE name IS NOT NULL
GROUP BY country
```

</details>
<details>
<summary><b>Задание №33:</b> Укажите корабли, потопленные в сражениях в Северной Атлантике (North Atlantic). Вывод: ship.</summary>
  
  ```mysql
SELECT ship
FROM Outcomes
INNER JOIN Battles ON Battles.name = Outcomes.battle
WHERE Outcomes.result = 'sunk' AND Battles.name = 'North Atlantic'
```

</details>
<details>
<summary><b>Задание №34:</b> По Вашингтонскому международному договору от начала 1922 г. запрещалось строить линейные корабли водоизмещением более 35 тыс.тонн. Укажите корабли, нарушившие этот договор (учитывать только корабли c известным годом спуска на воду). Вывести названия кораблей.</summary>
  
  ```mysql
Select name
FROM classes
INNER JOIN Ships ON Ships.class = Classes.class
WHERE launched >= 1922 AND displacement > 35000 AND type='bb'
```

</details>
<details>
<summary><b>Задание №35:</b> В таблице Product найти модели, которые состоят только из цифр или только из латинских букв (A-Z, без учета регистра). Вывод: номер модели, тип модели.</summary>
  
  ```mysql
SELECT model, type
FROM product 
WHERE model NOT LIKE '%[^a-z]%' OR model NOT LIKE '%[^0-9]%'
```

</details>
<details>
<summary><b>Задание №36:</b> Перечислите названия головных кораблей, имеющихся в базе данных (учесть корабли в Outcomes).</summary>
  
  ```mysql
SELECT name
FROM ships
WHERE class = name   

UNION  

SELECT ship
FROM classes, outcomes
WHERE classes.class = outcomes.ship
```

</details>
<details>
<summary><b>Задание №37:</b> Найдите классы, в которые входит только один корабль из базы данных (учесть также корабли в Outcomes).</summary>
  
  ```mysql
SELECT class
FROM (
    SELECT name, class
    FROM ships 

    UNION

    SELECT class AS name, class
    FROM classes
    JOIN outcomes ON classes.class = outcomes.ship
) as t
GROUP BY class
HAVING COUNT(name) = 1
```

</details>
<details>
<summary><b>Задание №38:</b> Найдите страны, имевшие когда-либо классы обычных боевых кораблей ('bb') и имевшие когда-либо классы крейсеров ('bc').</summary>
  
  ```mysql
SELECT DISTINCT country
FROM Classes
WHERE type = 'bb'

INTERSECT

SELECT DISTINCT country
FROM Classes
WHERE type = 'bc'
```

</details>
<details>
<summary><b>Задание №39:</b> Найдите корабли, `сохранившиеся для будущих сражений`; т.е. выведенные из строя в одной битве (damaged), они участвовали в другой, произошедшей позже.</summary>
  
  ```mysql
SELECT DISTINCT o1.ship
FROM Outcomes o1
JOIN Outcomes o2 ON o1.ship = o2.ship
JOIN Battles b1 ON o1.battle = b1.name
JOIN Battles b2 ON o2.battle = b2.name
WHERE o1.result = 'damaged' AND b2.date > b1.date
```

</details>
<details>
<summary><b>Задание №40:</b> Найти производителей, которые выпускают более одной модели, при этом все выпускаемые производителем модели являются продуктами одного типа.
Вывести: maker, type.</summary>
  
  ```mysql
SELECT maker, type
FROM Product
GROUP BY maker, type
HAVING COUNT(model) > 1 AND maker IN (SELECT maker FROM Product GROUP BY maker HAVING COUNT(DISTINCT type) = 1)
```

</details>
<details>
<summary><b>Задание №41:</b> Для каждого производителя, у которого присутствуют модели хотя бы в одной из таблиц PC, Laptop или Printer, определить максимальную цену на его продукцию. Вывод: имя производителя, если среди цен на продукцию данного производителя присутствует NULL, то выводить для этого производителя NULL, иначе максимальную цену.</summary>
  
  ```mysql

```

</details>
<details>
<summary><b>Задание №42:</b> Найдите названия кораблей, потопленных в сражениях, и название сражения, в котором они были потоплены.</summary>
  
  ```mysql
SELECT ship, battle
FROM outcomes
WHERE result = 'sunk'
```

</details>
<details>
<summary><b>Задание №43:</b> Укажите сражения, которые произошли в годы, не совпадающие ни с одним из годов спуска кораблей на воду.</summary>
  
  ```mysql
SELECT DISTINCT name
FROM Battles
WHERE YEAR(date) NOT IN (SELECT launched FROM Ships WHERE launched IS NOT NULL)
```

</details>
<details>
<summary><b>Задание №44:</b> Найдите названия всех кораблей в базе данных, начинающихся с буквы R.</summary>
  
  ```mysql
SELECT name
FROM Ships
WHERE name LIKE 'R%'

UNION

SELECT ship
FROM Outcomes
WHERE ship LIKE 'R%'
```

</details>
<details>
<summary><b>Задание №45:</b> Найдите названия всех кораблей в базе данных, состоящие из трех и более слов (например, King George V). Считать, что слова в названиях разделяются единичными пробелами, и нет концевых пробелов.</summary>
  
  ```mysql
SELECT name
FROM Ships
WHERE name LIKE '% % %'

UNION

SELECT ship
FROM Outcomes
WHERE ship LIKE '% % %'
```

</details>
<details>
<summary><b>Задание №46:</b> Для каждого корабля, участвовавшего в сражении при Гвадалканале (Guadalcanal), вывести название, водоизмещение и число орудий.</summary>
  
  ```mysql
SELECT out.ship, displacement, numGuns
FROM (SELECT name AS ship, displacement, numGuns
FROM Ships s JOIN Classes c ON c.class = s.class

UNION

SELECT class AS ship, displacement, numGuns
FROM Classes) AS ttt

RIGHT JOIN Outcomes out ON out.ship = ttt.ship
WHERE battle = 'Guadalcanal'
```

</details>
<details>
<summary><b>Задание №47:</b> Определить страны, которые потеряли в сражениях все свои корабли.</summary>
  
  ```mysql

```

</details>
<details>
<summary><b>Задание №48:</b> Найдите классы кораблей, в которых хотя бы один корабль был потоплен в сражении.</summary>
  
  ```mysql
SELECT DISTINCT classes.class
FROM Outcomes
LEFT JOIN ships ON outcomes.ship = ships.name
INNER JOIN classes ON (outcomes.ship = classes.class OR ships.class = classes.class)
WHERE result = 'sunk'
```

</details>
<details>
<summary><b>Задание №49:</b> Найдите названия кораблей с орудиями калибра 16 дюймов (учесть корабли из таблицы Outcomes).</summary>
  
  ```mysql
SELECT name
FROM Ships
INNER JOIN Classes ON Classes.class = Ships.class
WHERE bore = 16

UNION

SELECT ship
FROM Outcomes 
INNER JOIN classes ON Outcomes.ship = Classes.class
WHERE bore = 16
```

</details>
<details>
<summary><b>Задание №50:</b> Найдите сражения, в которых участвовали корабли класса Kongo из таблицы Ships.</summary>
  
  ```mysql
SELECT DISTINCT Battles.name
FROM Battles
INNER JOIN Outcomes ON Battles.name = Outcomes.battle
INNER JOIN Ships ON Outcomes.ship = Ships.name
WHERE Ships.class = 'Kongo'
```

</details>
<details>
<summary><b>Задание №51:</b> .</summary>
  
  ```mysql

```

</details>
