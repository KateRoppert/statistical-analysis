# statistical-analysis
# Статистический анализ для определения перспективного тарифа телеком-компании
Яндекс.Практикум, Модуль №2, Проект №1

**Заказчик исследования:** Компания «Мегалайн» — федеральный оператор сотовой связи.

**Описание проекта:** Клиентам предлагают два тарифных плана: «Смарт» и «Ультра». Чтобы скорректировать рекламный бюджет, коммерческий департамент хочет понять, какой тариф приносит больше денег.

**Данные:** В вашем распоряжении данные 500 пользователей «Мегалайна»: кто они, откуда, каким тарифом пользуются, сколько звонков и сообщений каждый отправил за 2018 год.

**Задача:** Проанализировать тарифы и поведение клиентов, использующих их, и сделать вывод — какой тариф лучше.

**РАЗДЕЛ 1. ИЗУЧЕНИЕ ДАННЫХ**

У нас есть несколько датасетов с информацией о пользователях сотовой связи: users содержит справочную информацию о самом пользователе и тарифе, который он выбрал; calls, messages и internet содержат информацию об израсходованных минутах, сообщениях, интернет-траффике соответственно. А так же есть таблица tariffs с информацией о каждом тарифе. В нашем распоряжении информация о 500 пользователях, количество строк в данных со звонками, сообщениями и интернет-траффике везде разное. В датасете internet обнаружена и удалена лишняя колонка с дубликатами индексов Unnamed: 0.

**РАЗДЕЛ 2. ПРЕДОБРАБОТКА ДАННЫХ***

2.1 Проверка типов данных
В этом разделе изучили все датасеты на типы данных: все даты привели к типу datetime, идентификационные номера - к целочисленному типу, количество минут тоже привели к целочисленному типу с округлением вверх.

2.2 Изучение пропусков
Пропуски есть только в churn_rate - это дата прекращения пользования тарифом. Если она пропущена, значит, тариф ещё действовал на момент выгрузки данных. Больше пропусков в данных нет.

2.3 Изучение значений по столбцам

Идентификаторы пользователей в таблице представлены от 1000 до 1499.
Возраст пользователей распределяется от 18 до 75 лет. Средний возраст - 46 лет.
Длительность звонков распределяется от 0 минут (это пропущенные звонки) до 38 минут. Средняя длительность - 7 минут.
Количество исрасходованных мБ интернет-трафика распределяется от 0 до 1725 мБ. Среднее значение - 370 мБ. Нулевые значения могут говорить о неудачных попытках выхода в интернет. Таких значений 13%, из них 11 - это тариф "смарт".
2.4 Подготовка данных
На этом этапе были посчитаны средние значения в месяц по минутам, сообщениям, трафику и выручке для каждого пользователя и добавлены в таблицу users.

**РАЗДЕЛ 3. ИССЛЕДОВАТЕЛЬСКИЙ АНАЛИЗ ДАННЫХ**

3.1 Описательная статистика

3.1.1 Количество израсходованных минут для тарифа "ультра"

Среднее: 559 минут
Медиана: 533 минуты
Стандартное отклонение: 268 минут

Распределение стремится к нормальному, данные немного скошены вправо, большое стандартное отклонение.
99% значений лежат в интервале до 1279 минут, что в 2 раза меньше 3000 минут, входящих в пакет.
42% значений лежат в интервале до 500 минут.
Наибольшая вероятность (20%) приходится на интервал 500-600 минут.

3.1.2 Количество израсходованных минут для тарифа "смарт"

Среднее: 425 минут
Медиана: 431 минута
Стандартное отклонение: 148 минут

Распределение стремится к нормальному, данные немного скошены влево, стандартное отклонение в два раза меньше, чем у тарифа "ультра".
99% значений лежат в интервале до 869 минут.
69% значений лежат в интервале до 500 минут и укладываются в пакет.
Наибольшая вероятность (30%) приходится на интервал 400-500 минут.

3.1.3 Количество израсходованных сообщений для тарифа "ультра"

Среднее: 65 сообщений
Медиана: 59 сообщений
Стандартное отклонение: 42 сообщения

Данные скошены влево, есть единичный выброс, но он входит в итервалы трёх сигм.
99% значений лежат в интервале до 193 сообщений - это намного меньше количества сообщений в пакете.
36% значений лежат в интервале до 50 сообщений.
Наибольшая вероятность (30%) приходится на интервал 25-50 сообщений.

3.1.4 Количество израсходованных сообщений для тарифа "смарт"

Среднее: 38 сообщений
Медиана: 33 сообщения
Стандартное отклонение: 25 сообщений

Данные скошены вправо, есть 4 выброса, 2 из которых входят в интервалы трёх сигм.
99% значений лежат в интервале до 112 сообщений.
68% значений лежат в интервале до 50 сообщений.
Наибольшая вероятность (18%) приходится на интервал 10-20 сообщений.

3.1.5 Объём израсходованного интернет-трафика для тарифа "ультра"

Среднее: 20 гБ
Медиана: 19 гБ
Стандартное отклонение: 8 гБ

Данные немного скошены вправо, выбросов нет.
99% значений лежат в интервале до 43 гБ.
89% значений лежат в интервале до 30 гБ.
Наибольшая вероятность (30%) приходится на интервал 15-20 гБ.

3.1.6 Объём израсходованного интернет-трафика для тарифа "смарт"

Среднее: 16 гБ
Медиана: 16 гБ
Стандартное отклонение: 4 гБ

Данные распределены нормально, есть небольшие выбросы в обе стороны.
99% значений лежат в интервале до 28 гБ.
40% значений лежат в интервале до 15 гБ.
Наибольшая вероятность (18%) приходится на интервал 15-16 гБ.

3.2 Проверка гипотез
Гипотеза 1
Нулевая гипотеза: средняя выручка пользователей тарифов «Ультра» и «Смарт» одинакова.
Альтернативная гипотеза: средняя выручка пользователей тарифов «Ультра» и «Смарт» различается.

Вероятность равенства средних выручек двух тарифов стремится к нулю, значит, нулевая гипотеза отвергается в пользу альтернативной.

Гипотеза 2
Нулевая гипотеза: средняя выручка пользователей из Москвы не отличается от выручки пользователей из других регионов. Альтернативная гипотеза: средняя выручка пользователей из Москвы отличается от выручки пользователей из других регионов.

Вероятность того, что выручка пользователей из Москвы и других регионов будет одинакова, очень велика - принимается нулевая гипотеза.

**ИТОГ:** тариф "ультра" выгоднее для компании, а "смарт" - для пользователей. Тариф "ультра" стоит дороже и приносит в среднем больше выручки, потому что все пользователи выборки переплачивают за ненужные минуты, сообщения и интернет, входящие в пакет, и никогда не успевают использовать его целиком. Всего лишь 47 пользователей тарифа "смарт" приносят выручку больше стоимости базового пакета "ультра" за 1950.

