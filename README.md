# Задачи регрессии

Привет! В этом репозитории лежат мои первые проекты по задачас регрессии, которые я загружал на [kaggle](https://www.kaggle.com/agleev). Я брал данные, делал проект в Jupiter Notebook и выгружал на сайт. Только после этого я решил загрузить сюда, на github. В них нет контроля версий, нет отдельных файлов с заданными функциями и даже нет файла readme. Честно признаться, и некоторые проекты имеют недостатки, которые я увидел лишь спустя время.

Как оказалось потом, большая часть данных по задачам классификации и регрессии - искусственные, не очень интересно работать с ними дальше. Если прогнать их по алгоритмам с дефолтными настройками, то они покажут отличные показатели метрик качества даже без предобработки данных.

Ниже расскажу о каждом проекте и недостатках, которые в нем есть. Отдельная папка - отдельный проект с файлом данных .csv и файлом проекта.

## 02_prices_for_ford_cars_r2_0.94

[100,000 UK Used Car Data set](https://www.kaggle.com/adityadesai13/used-car-dataset-ford-and-mercedes) - набор данных поддержанных автомобилей, у которых нужно спрогнозитровать цену. Весь набор содержит 15 файлов .csv соответсвующие отдельной марки авто, я работал только с одни - Ford.

1.Разбил модели, виды трансмиссии и тип двигателя на отдельные признаки.  
2. Распределение целевой переменной `price` близко к нормальному, поэтому я убрал выбросы используя 3 стандартных отклонения.  
3. Провел регрессионыый анализ и убрал признаки, где значение `p-value` было больше 0.05.  
4. Запустил обучение на 11 моделях, выбрал лучшие результат: `XGBRegressor`, R2 = 0.932.  
5. После настройки алгоритма `XGBRegressor`, улучшил результат до R2 = 0.941  

[Prices for Ford cars. R2 score: 0.941](https://www.kaggle.com/agleev/prices-for-ford-cars-r2-score-0-941) - мой проект на kaggle.

## 03_medical_cost_prediction_r2_0.89

[Medical Cost Personal Datasets](https://www.kaggle.com/mirichoi0218/insurance) - набор данных клиентов, где нужно предсказать расходя на медицинскую страховку. Признаки - пол, возраст, индекс массы тела, сколькго детей, курит или нет, и целевая - расходы по страховке.

Анализ данных показал, что существует линейная зависимость между расходами по страховке `charges` и индексом массы тела `bmi` у курильщиков. То есть, если человек курит и имеет избыточный вес, то расходы по его страховке возрастают. Если человек не курит, но так же имеет избыточный вес, то у большинства клиентов размер `charges` не превышает 15 000.  
Для наглядности график ниже:

![scatterplot charges and bmi](https://www.kaggleusercontent.com/kf/80048443/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..a4JhfI3MuYP9VrG02V76Aw.me38R2NaW9bU2GCn56BsfExGZSTL4F39NBzL80eq4EOl0df_XMJ-znN-BcqV-mqY9UCBBuEYXxjskGn4k5XGHcl8RLrsl0TDyI2w1p_WHXqbsObN6KMhXgNjRjbs2KFHYzgaCCYXFBH92o_T9ADzr8utOf_gN0I_7fBbtkB4fcGWhBpctnbJ5_nPHRhdj4z1QF_KJvthH4Zt_phJykGS4Nb_vvpArF-Ekm8QJTOnU_2vF7sdjaSw6yaqKbVPEKEvzj6Dhj6AkcTJ8GvWwE6KwQfaDKlGWb_QcAiRZ5zWScJfJzh6_skmFBYDVcgU4nucJZPvMK2sy1TrbBQgp4lOdgw--prSPh5mhfrxvSmWO0GejU6iViw6cJ5arW8savt6Ncfs6rJErYEwzMn3G44XiNebh3Jm3EZiBhmGBRpDzSU5MQiGXjjtDmjV9JTbUb2u4rdtfXQq4gHlY3LMVtVMccNK6R21dYxFeOOqDBpekHw90dgtZVZKBMYtPsimw3j5UmMSSxevQwWvux9roDe_Kx_3cHZeWjX21wyovmwxTlDsLeBalpY7zkP0rzCQAcTWMSFThA3TbWaf7s-HLT30eqjDK21JMjoxTK9MLEexZZINEs47nQYXb_FM_QTPGMDmsq8rReBaOPu5Vf-JuB5W--qmHC4p98CZ6Lw1REkZEqs.PA_Jpltkay_3CTZIcUYksQ/__results___files/__results___58_1.png "scatterplot")

Дальнейшая работа с данными:
1. Прологорифмировал целевую переменную, чтобы привести ее к нормальному распределению.
2. Прошкалировал непрерывные переменные.
3. Обучил на нескольких алгоритмах, лучшие результат: `RandomForestRegressor`, R2 = 0.893

