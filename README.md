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

![scatterplot charges and bmi](https://raw.githubusercontent.com/agleev/regression/master/03_medical_cost_prediction_r2_0.89/scatterplot.png "scatterplot")

Дальнейшая работа с данными:
1. Прологорифмировал целевую переменную, чтобы привести ее к нормальному распределению.
2. Прошкалировал непрерывные переменные.
3. Обучил на нескольких алгоритмах, лучшие результат: `RandomForestRegressor`, R2 = 0.893

## 04_pizza_price_prediction_r2_0.94

[Pizza Price Prediction](https://www.kaggle.com/knightbearr/pizza-price-prediction) - набор данных, где нужно было предсказать цену на пиццу. Признаки - название компании, размер, диаметр, название пиццы, топпинги и какое содержание грибов, сыра и соуса в составе.

1. Я удалил категориальные признаки размер пиццы и и топпинги. Потому что вместо размера(маленькая, большая, средняя) есть точный признак - диаметр, вместо топпинга - вариант пиццы, который зависит от топпинга. Одна и та же начинка может быть в разных видах пицц.
2. Запустил несколько моделей, лучшие результат: `GradientBoostingRegressor`, R2 score = 0.94.

Ошибки, которые я допустил: не привел таргет к нормальному распределению и не прошкалировал непрерывные переменные.

[Pizza: OLS, groupby, 12 models. GBR: R2 score 0.94](https://www.kaggle.com/agleev/pizza-ols-groupby-12-models-gbr-r2-score-0-94) - мой проект на kaggle.
