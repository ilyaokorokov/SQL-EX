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

```

</details>
<details>
<summary><b>Задание №30:</b> .</summary>
  
  ```mysql

```

</details>
<details>
<summary><b>Задание №31:</b> .</summary>
  
  ```mysql

```

</details>
<details>
<summary><b>Задание №32:</b> .</summary>
  
  ```mysql

```

</details>
<details>
<summary><b>Задание №33:</b> .</summary>
  
  ```mysql

```

</details>
<details>
<summary><b>Задание №34:</b> .</summary>
  
  ```mysql

```

</details>
<details>
<summary><b>Задание №35:</b> .</summary>
  
  ```mysql

```

</details>
