# Исследование итогов курсов в образовательном учреждении
## Описание задачи 
В ходе анализа предлагалось выполнить следующие задачи:
1. Выяснить, сколько студентов успешно сдали только один курс.
2. Выявить самый сложный и самый простой экзамен: найди курсы и экзамены в рамках курса, которые обладают самой низкой и самой высокой завершаемостью.
3. По каждому предмету определить средний срок сдачи экзаменов (под сдачей понимаем последнее успешное прохождение экзамена студентом).
4. Выявить самые популярные предметы (ТОП-3) по количеству регистраций на них. А также предметы с самым большим оттоком (ТОП-3).
5. В период с начала 2013 по конец 2014 выявить семестр с самой низкой завершаемостью курсов и самыми долгими средними сроками сдачи курсов.

Также было необходимо провести RFM-анализ аудитории.

# Стек
- Python 
- Pandas
- Seaborn
- Matplotlib

# Ход работы
Сначала я провела разведочный анализ, чтобы определить, что будет считаться курсом. 

Далее я ответила на поставленные вопросы и приступила к основной части работы - постройке адаптированных RFM-кластеров студентов для оценки аудитории.

В адаптированной кластеризации я выбрала следующие метрики:

- R - среднее время сдачи одного экзамена,
- F - завершаемость курсов,
- M - среднее количество баллов, получаемое за экзамен.

### Recency (R) - среднее количество дней, потраченное на курсы:

Я посмотрела на распределение по децилям и на график распределения среднего времени, потраченого на курсы. Выделила 3 зоны: примерно до 240, которая характеризуется колебаниями; от 240 до ~250, где показатели стабильно высокие; более 250 с самыми низкими показателями. Эти данные и выступили сигментами.

1: менее 240 дней

2: от 240 до 250 дней

3: более 250 дней

### Frequency (F) - завершаемость курсов:

Взяла значения завершаемости, уже присутствующие в данных. 

1: 1

2: 0.5

3: 0

### Monetary (M) - среднее количество баллов, получаемое за экзамен:

Для кластеризации среднего количества баллов я взяла условия задания, где балл меньше 40 - незачет, и стандартное распределение баллов в университете с некоторым упрощением (без оценки "удовлетворительно").

1: 80 и более - отлично

2: 40-80 - хорошо

3: менее 40 - незачет

Затем я написала функции для распределения сегментов в кластерах и для характеризации студентов. Далее объединила получившиеся кластеры в логические группы, по которым дала рекомендации.

# Выводы
### Ответы на поставленные задачи:
1. 3802 студента успешно сдали только один курс.
2. Самым сложным экзаменом оказался 25340 : курс 'DDD-2013B' : CR = 0.84.

   Самым простым экзаменом оказался 25361 : курс 'DDD-2014B' : CR = 0.93.
4. На экзамен по CCC потрачено в среднем 239.35 дней.

   На экзамен по DDD потрачено в среднем 237.98 дней.
5. Топ-3 предмета по популярости: BBB, FFF, DDD

   Топ-3 предмета по оттоку: CCC, DDD, FFF

   При этом больше всего человек ушли с BBB, FFF, DDD
6. Семестр с самой низкой завершаемостью: 2013B

   Семестр с самым долгим средним сроком сдачи курсов: 2014J

## Итоги RFM-анализа:
В результате проведенного RFM-анализа аудитории учебного заведения были сформированы 6 групп студентов.
![распределение](https://github.com/ValeriaGlushkova/E-learning/blob/main/Groups.png)

Одназначно можно выделить группу _"Умнички"_, которая состоит из студентов, сдавших экзамен на хорошо и отлично в ранние или оптимальные сроки. Приоритетным будет удержать их на этом уровне или поднять выше. Для этого можно использовать различные бонусы в виде, например, повышенных стипендий.

Группа _"Лучшие из лучших"_ вторая по количеству студентов, что является потрясающим результатом, т.к. это те студенты, которые являются отличниками, сдавшими экзамены в числе первых. Задача стоит такая же - удержать их на уровне. Бонусы: также повышенная стипендия, подарки и т.п.

Эти две группы являюся амбассадорами курсов, которые потенциально могут привести других студентов, т.е. клиентов.

Примерно на равне с лучшими по количеству находится группа _"Поняли, что курс не их"_, что удручает. Довольно большое количество студентов решили не сдавать курс. Можно провести опрос, что студента не устроило в курсе, почему он решил не сдавать экзамен и,возможно, предложить ему альтернативы.

Далее идут группы _"Молодцы, но нужно быть порасторопнее"_, которая состоит из хорошистов и отличников, которые сдали экзамен в последний момент, и _"Хорошо постарались, но есть к чему стремиться"_, в которой находятся студенты, которые смогли окончить только половину курсов. Это те студенты, у которых появились трудности во время прохождения курсов, но при этом которые хотят учиться. Во-первых, мативаторами для них могут выступить первые две группы. Во-вторых, можно предоставить им, например, скидку на альтернативные курсы, тем самым и "показав заботу", и заработав.

Последняя группа - _"Они пытались"_ - очень малочислена. Это те, кто до последнего старался сдать все курсы, но у них не получилось. Можно также дать им скидку на альтернативные курсы перед эти также провести опрос на тему трудностей, с которыми эти студенты столкнулись. Но тут появляется дилемма: с одной стороны - это лишний спосоность заработать, с другой стороны такие студенты могут понизить рейтинг учебного заведения.
