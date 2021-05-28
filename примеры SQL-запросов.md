* [Примеры баг-репортов](https://github.com/PavlovEvgeny16/portfolio/blob/master/%D0%BF%D1%80%D0%B8%D0%BC%D0%B5%D1%80%D1%8B%20%D0%B1%D0%B0%D0%B3-%D1%80%D0%B5%D0%BF%D0%BE%D1%80%D1%82%D0%BE%D0%B2.md)
* [Примеры тест-кейсов](https://github.com/PavlovEvgeny16/portfolio/blob/master/%D0%BF%D1%80%D0%B8%D0%BC%D0%B5%D1%80%D1%8B%20%D1%82%D0%B5%D1%81%D1%82-%D0%BA%D0%B5%D0%B9%D1%81%D0%BE%D0%B2.md)
* [Примеры чек-листов](https://github.com/PavlovEvgeny16/portfolio/blob/master/%D0%BF%D1%80%D0%B8%D0%BC%D0%B5%D1%80%D1%8B%20%D1%87%D0%B5%D0%BA-%D0%BB%D0%B8%D1%81%D1%82%D0%BE%D0%B2.md)

## Примеры SQL запросов
<br>
Задания взяты с сайта sql-academy.org

<h3>Пример 1.</h3>
<h4>Задание:</h4>
Сколько и кто из семьи потратил на развлечения (entertainment). Вывести статус в семье, имя, сумму

<h4>Решение:</h4>
SELECT status, member_name, SUM(unit_price*amount) AS costs
<br>
FROM  FamilyMembers
<br>
INNER JOIN Payments JOIN Goods JOIN GoodTypes ON FamilyMembers.member_id = Payments.family_member
<br>
AND Payments.good = Goods.good_id AND Goods.type = GoodTypes.good_type_id
<br>
WHERE good_type_name = 'entertainment'
<br>
GROUP BY member_name, status

<h3>Пример 2.</h3>
<h4>Задание:</h4>
Найдите максимальный возраст (колич. лет) среди обучающихся 10 классов 

<h4>Решение:</h4>
SELECT MAX(((YEAR(CURRENT_DATE) - YEAR(birthday)) - 
<br>
(DATE_FORMAT(CURRENT_DATE, '%m%d') < DATE_FORMAT(birthday, '%m%d')))) as max_year
<br>
FROM Student INNER JOIN Student_in_class JOIN Class ON Student.id = Student_in_class.student AND Student_in_class.class = Class.id
<br>
WHERE name LIKE '%10%'

<h3>Пример 3.</h3>

<h4>Задание:</h4>
Какой(ие) кабинет(ы) пользуются самым большим спросом?

<h4>Решение:</h4>
SELECT classroom FROM (
<br>
SELECT classroom, COUNT(*) AS cnt FROM Schedule GROUP BY classroom) AS cnt 
<br>
WHERE cnt = (SELECT MAX(cnt) FROM (
<br>
SELECT classroom, COUNT(*) AS cnt FROM Schedule GROUP BY classroom) AS cnt)
