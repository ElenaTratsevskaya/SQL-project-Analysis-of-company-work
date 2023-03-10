# SQL-project-Analysis-of-company-work
Анализ работы компании с целью масштабирования бизнеса / Analysis of company work to scale business


**[Финальный проект / SQL-project-Analysi](https://docs.google.com/document/d/1Ix89fG4nWibCJfOFcJwpOQcSqrW2ntnRdz_qAmhKg9I/edit#)**<br>

ФОРМАЛИЗОВАННАЯ ЗАДАЧА
Оценить динамику продаж и распределение выручки по товарам.<br>
Составить портрет клиента, а для этого — выяснить, какие клиенты приносят больше всего выручки.<br>
Проконтролировать логистику компании (определить, все ли заказы доставляются в срок и в каком штате лучше открыть офлайн-магазин). <br>

Исходные данные предсттавлены в следующих таблицах:<br>
Таблица **store_customers** - справочник клиентов<br>
Таблица **store_products** - справочник товаров<br>
Таблица **store_carts** - список товаров в заказе, их количество, а также скидка для каждого товара<br>
Tаблица **store_delivery** - информация о заказах и их доставке<br><br>

**1. Определение эффективности продаж**
**1.1** Расчет выручки<br>
Составляю запрос, который выведет сумму выручки по месяцам:<br>
date (месяц заказа) ― тип date;<br>
revenue (объем выручки) ― округление значения до целых с помощью round.<br>
Сортировка запроса по дате заказа<br>

![ГитХаб_SQL_01](https://user-images.githubusercontent.com/110056199/219683366-657f694b-87cb-4394-8223-67aa163c60b7.jpg)<br>
![#27 5 1](https://user-images.githubusercontent.com/110056199/219685995-d05ea771-ca0d-4575-9962-8211efb09365.jpg)<br>
**В Ы В О Д Ы:**   
линия графика имеет ломаный характер с выраженными максимальными и минимальными показателями. Можно говорить о сезонности: пики продаж приходятся на ноябрь, спад наблюдается в первые два месяца года. Линия тренда положительная.<br><br>
**1.2** Расчет выручки по категориям<br>
Составляю запрос, который выведет:<br>
category (категория товара);<br>
subcategory (подкатегория товара);<br>
revenue (объем выручки) ― округлите до целых с помощью round.<br>
Сортировка по убыванию выручки.<br><br>
![ГитХаб_SQL_02](https://user-images.githubusercontent.com/110056199/219694238-68258341-8c15-4350-bbde-010cdc6c19a6.jpg)<br>
**В Ы В О Д Ы:**
результат запроса показал, что первую строку по сумме выручки со значением  ― 235318 занимает category (категория товара) ― Furniture; subcategory (подкатегория товара) ― Chairs;<br>

**1.3** Оценка товаров по выручке<br>
Пишу запрос, который выведет данные топ-25 товаров по объёму выручки в следующем формате:<br>
product_nm — наименование товара;<br>
revenue — объём выручки; quantity — количество проданных товаров; Не забудьте просуммировать количество!<br>
percent_from_total — доля от общей выручки в процентах.<br><br>
![ГитХаб_SQL_03](https://user-images.githubusercontent.com/110056199/219694818-0d06c9c7-8e67-468a-92b7-e0be7e404504.jpg)<br>
**В Ы В О Д Ы:**<br>
Первую позицию по выручке с отрывом более чем в 2 раза от второй занимает - Canon imageCLASS 2200 Advanced Copier.<br><br>
![#27 5 7](https://user-images.githubusercontent.com/110056199/219695378-24d2c306-4011-458a-9032-80f75237cbe8.jpg)<br><br>

**В Ы В О Д Ы:**<br>
топ-25 даёт 15,35% выручки. Убедительный показатель, если сделать вывод таблицы без ограничения LIMIT 25, то мы увидим общее количество товарных позиций через количество строк - 1 818 строк.<br><br>

**2. Составление портрета клиента**<br>
**2.1** Определение количества клиентов и выручки по категориям клиента<br>
Пишу запрос, который выведет:<br>
category (категория клиента);<br>
cust_cnt (количество клиентов);<br>
revenue (объем выручки) ― округляю до целых с помощью round.<br>
Запрос отсортирован по убыванию выручки.<br>
Примечание: поскольку в таблице store_customers нет ключа к таблицам store_carts и store_products, но есть ключ к таблице store_delivery, я  решила добавить в CTE таблицу store_delivery и включить в вывод CTE cust_id, с тем чтобы извлечь затем необходимые данные.<br><br>
![ГитХаб_SQL_04](https://user-images.githubusercontent.com/110056199/219696681-20720b13-3bee-44f3-8afb-d36e500d4a81.jpg)<br><br>
![#27 6 1 (1)](https://user-images.githubusercontent.com/110056199/219696970-6efc1e2b-17f2-479a-8657-4f8e34461575.jpg)<br><br>
**В Ы В О Д Ы:**<br>
Выручка от корпоративных клиентов существенно превышает выручку от заказов розничных покупателей, график по количеству клиентов аналогичен визуально по столбцам графику по выручке.
<br><br>
**2.2** Определение количества новых клиентов по месяцам<br>
Пишу запрос, который выведет:<br>
month (месяц) ― тип date;<br>
new_custs (количество новых клиентов).<br>
Сортирую запрос по первому столбцу (по дате) в порядке возрастания.<br><br>
![ГитХаб_SQL_04 (2)](https://user-images.githubusercontent.com/110056199/219697481-ac51aabc-a042-4c15-8341-7ed8fcfaf14c.jpg)<br><br>
![#27 6 2 (1)](https://user-images.githubusercontent.com/110056199/219697753-bd3dd04c-aa5a-4b4e-836e-1de9f9099c87.jpg)<br><br>
**В Ы В О Д Ы и Р Е К О М Е Н Д А Ц И И:**
График показывает динамику изменений количества новых клиентов с резким падением в январе 2018 года, несущественными подъемами на протяжении 2018 года и далее спад к единичным показателям. 2017 год успешный. Пик приходится на сентябрь 2017 года. Даже по низким столбцам графика по годам 2018-2020 очевидно, что после Рождественских каникул подъем приходится на март.<br> 
При этом график выше — (#27.5.1) Сумма выручки по месяцам имеет положительную линию тренда. Следовательно компания работает за счёт уже привлеченных клиентов, что говорит о доверии потребителя к компании. Стоит детально изучить период на границе 2017/2018  для выявления причин такого срыва показателей по количеству новых корпоративных клиентов.<br>

**2.3** Составление характеристики B2B-клиентов<br>
Сколько в среднем различных товаров в заказах у корпоративных клиентов?<br>
Какая в среднем сумма заказов у корпоративных клиентов?<br>
Сколько в среднем различных офисов у корпоративных клиентов?<br>

*Примечание:* <br>
поскольку таблицы связаны между собой через разные ключи, так таблица store_customers связана с таблице store_delivery по ключу, а ответ на вопрос в таблице store_carts, то я  решила собрать их в одну таблицу, а затем извлекать необходимые последовательно. В в pgAdmin avg_count_product выводится именно как указано в условии задания — 2.0<br>

Создаю CTE, откуда получаю первые два показателя.<br><br>
![ГитХаб_SQL_05 (2)](https://user-images.githubusercontent.com/110056199/219698270-20ba0c02-a2db-4e92-a5d3-1b2fb22e87bc.jpg)<br>
Для получения данных по офисам, оставляю в CTE две таблицы: store_delivery и store_customers.<br><br>
![ГитХаб_SQL_06 (2)](https://user-images.githubusercontent.com/110056199/219698716-c6d41a3e-feb3-4bb7-869e-43cb1d44e2ec.jpg)<br>
**В Ы В О Д Ы:**<br>
В результате получена следующая характеристика В2В-клиента (портрет покупателя):<br>
среднее количество товаров в заказе — 2,0<br>
средняя сумма заказа — 285,9<br>
средний показатель по количеству офисов у В2В-клиентов — 6,2<br><br>

**3. Анализ логистики компании**<br>
Необходимо оценить текущую картину по логистике доставок и найти штат, в котором лучше всего открыть офлайн-магазин.
Формализованная задача:<br>
1. Насколько эффективно выполняются текущие доставки?<br>
2. Как распределяются доставки и выручка по штатам и городам? <br>

Определение эффективность доставки необходимо начать с оценки текущей эффективности.<br>

Поле **ship_mode** таблицы **store_delivery** содержит четыре различных значения.
<br>
<table>
<thead>
<tr><th>Тип доставки</th><th>Описание</th><th>Планируемое время доставки</th></tr>
</thead>
<tbody>
<tr><td>Standard Class</td><td>Стандартная доставка</td><td>Доставка в течение шести дней</td></tr>
<tr><td>Second Class</td><td>Доставка вторым классом</td><td>Доставка в течение четырех дней</td></tr>
<tr><td>First Class</td><td>Доставка первым классом</td><td>Доставка в течение трех дней</td></tr> 
<tr><td>Same Day</td><td>Экспресс-доставка</td><td>Экспресс-доставка в тот же день</td></tr>
</tbody>
</table>
<br><br>
Если заказ был оформлен вечером, когда его уже нельзя отправить, то в базу данных записывается дата, следующая за датой заказа. Таким образом, дата заказа — дата, когда заказ был взят в работу.<br><br>

**3.1** Определение, какая доля заказов выполняется в срок по каждой категории<br><br>
Пишу запрос, который выведет:<br>
- тип доставки;<br>
- общее количество заказов (orders_cnt);<br>
- количество заказов, которые не были доставлены вовремя (late_orders_cnt);<br>
- долю выполненных вовремя заказов, в процентах (% success), округленную до двух знаков после запятой.<br>

Сортировка запроса по четвертому столбцу в порядке возрастания.<br>
![ГитХаб_SQL_07 (2)](https://user-images.githubusercontent.com/110056199/220073811-c9fd4cfe-2a8b-4b74-88de-dbe92ce17964.jpg)<br>
**В Ы В О Д Ы и Р Е К О М Е Н Д А Ц И И:**
Чаще всего нарушаются сроки доставки вторым классом (Second Class), нарушение сроков в 21% случаев. Второе место по нарушению сроков занимает стандартная доставка (Standard Class) с показателем успешных доставок 89,68%. При этом количество заказов с таким способом доставки максимальное — 2994. То есть большинство покупателей выбирает именно этот способ доставки не смотря на нарушение сроков доставки в чуть менее 11% случаев.<br>
Необходимо более детально изучить, что происходит с доставкой вторым классом, чтобы снизить показатель доставки с нарушением сроков. <br><br>

**3.2** Определение доли заказов, отправленных вторым классом и доставленных с опозданием<br>
Пишу запрос, чтобы вывести долю заказов, отправленных вторым классом, которые были доставлены с опозданием, по кварталам и построю график<br><br>
![ГитХаб_SQL_08 (2)](https://user-images.githubusercontent.com/110056199/220075252-7df2092a-d08c-4fe9-abe4-ceab84b2c640.jpg)<br>
![ГитХаб_SQL_11 (3)](https://user-images.githubusercontent.com/110056199/220077894-5099d4e9-0fa2-4f65-8b92-00b3844632ff.jpg)<br><br>

**Выбор оффлайн точки продаж**<br>

Сейчас есть только склад, откуда отправляются все товары, — находится он в городе Хьюстон, штат Техас (Houston, Texas).<br>
С помощью оффлайн-магазина можно привлечь больше клиентов и снизить стоимость доставки, нужно только выбрать, где его открыть. Для этого нахожу город и штат, куда совершается больше всего доставок.<br>

**3.4**  Какой штат наиболее популярный по количеству доставок <br><br>
![ГитХаб_SQL_09 (2)](https://user-images.githubusercontent.com/110056199/220078261-554597d7-3cd0-440b-8938-7a49b28bfd6c.jpg)<br><br>
**3.5**  Какой город наиболее популярный по количеству доставок <br><br>
![ГитХаб_SQL_10 (2)](https://user-images.githubusercontent.com/110056199/220078512-57e82625-3dda-41b7-9fc4-c7adc0d1bb23.jpg)<br><br>

**Визуализация данных по доставке**<br>
![ГитХаб_SQL_12 (3)](https://user-images.githubusercontent.com/110056199/220078912-258e1765-ab2d-44ff-856c-3263c1581986.jpg)

**В ходе работы над проектом были сделаны следующие выводы:**<br>
1. Эффективность продаж<br>
Расчет выручки показал, что пики продаж приходятся на ноябрь, спад наблюдается в первые два месяца года, можно говорить о сезонности. Динамика положительная.
Расчет выручки по категориям выявил лидеров продаж: первую строку по сумме выручки со значением  ― 235318 занимает category (категория товара) ― Furniture; subcategory (подкатегория товара) ― Chairs;<br>
Оценка товаров по выручке показал, что первую позицию по выручке с отрывом более чем в 2 раза от второй занимает ― Canon imageCLASS 2200 Advanced Copier. А топ-25 даёт 15,35% выручки. <br>

2. Портрета клиента<br>
Расчёт количества клиентов и выручки по категориям клиента показал, что выручка от корпоративных клиентов существенно превышает выручку от заказов розничных покупателей, а график по количеству клиентов аналогичен визуально по столбцам графику по выручке.<br>
Определение количества новых клиентов по месяцам и построенный график демонстрирует динамику изменений количества новых клиентов с резким падением в январе 2018 года, несущественными подъемами на протяжении 2018 года и далее спад к единичным показателям. <br>
При этом график выше — Выручка по месяцам имеет положительную линию тренда. Следовательно компания работает за счёт уже привлеченных клиентов, что говорит о доверии потребителя к компании. Стоит детально изучить период на границе 2017/2018  для выявления причин такого срыва показателей по количеству новых корпоративных клиентов.
Составление характеристики B2B-клиентов<br>
В результате получена следующая характеристика В2В-клиента (портрет покупателя):<br>
- среднее количество товаров в заказе — 2,0<br>
- средняя сумма заказа — 285,9<br>
- средний показатель по количеству офисов у В2В-клиентов — 6,2<br><br>

3. Анализ логистики компании<br>
Определение доли заказов выполненных в срок по каждой категории<br>
Чаще всего нарушаются сроки доставки вторым классом (Second Class), нарушение сроков в 21% случаев. Второе место по нарушению сроков занимает стандартная доставка (Standard Class) с показателем успешных доставок 89,68%. При этом количество заказов с таким способом доставки максимальное — 2994. То есть большинство покупателей выбирает именно этот способ доставки не смотря на нарушение сроков доставки в чуть менее 11% случаев.<br>
Выявление доли заказов, отправленных вторым классом и доставленных с опозданием<br>
Чаще всего нарушаются сроки доставки вторым классом в 4 квартале. Если посмотреть график выручки по месяцам, то очевидно, что на ноябрь и декабрь приходится пик заказов, кроме того есть явный всплеск в августе, и это объясняет тот факт, что второе место по нарушению сроков доставки - 3 квартал. Имеет место сезонность. Решением проблемы возможно станет открытие офлайн точки, чтобы снизить нагрузку с департамента доставки.<br>

**В итоге рекомендуется место для офлайн магазина в штате Калифорния.**












