 # «ML-Based Индекс страха и жадности российского фондового рынка»

## 📊 Описание продукта  
Веб-приложение (c API) и телеграм-бот для отслеживания настроения российского фондового рынка (индекса страха и жадности), которое использует ML-модель анализирующую данные о торгах акций индекса MOEX50, индексы IMOEX,RTS и данные фьючерсов на доллар и золото.

Индекс страха и жадности (Fear & Greed Index) — это индикатор настроений инвесторов, показывающий, преобладает ли на рынке страх или жадность. Он помогает определить, переоценивают ли инвесторы активы и накапливают позиции (жадность) или наоборот массово бегут с рынка (страх) и закрывают их.

---

## Бизнес-цель проекта:

Создать индикатор технического анализа, который поможет более качественно оценить инвесторам точки входа и выхода из сделки в торговле ценными бумагами, следовательно, уменьшить их убытки и увеличить прибыль.

## 🧑‍💼 Целевой пользователь сервиса

1) Инвесторы и трейдеры, осуществляющие сделки с ценными бумагами через любого из брокеров на российском фондовом рынке и желающие уменьшить степень неопределенности относительно настроения рынка, находясь в сделке. (Рядовой инвестор без знания основ API, может получать рассылку через Telegram).
2) Алгоритмические трейдеры, желающие усовершенствовать собственные стратегии с помощью добавления дополнительного признака. (Для получения исторических данных и парсинга может использоваться API)
3) Инвест-СМИ, сервисы-аггрегаторы рыночных данных, брокеры желающие интегрировать решение на собственные платформы.


## Существующие готовые решения и актуальность:

На данный момент существует единый признанный индекс страха и жадности для американского фондового рынка ([https://edition.cnn.com/markets/fear-and-greed](https://edition.cnn.com/markets/fear-and-greed)), рассчитываемый с 2013 года и состоящий из 7 показателей:

| №  | Компонент           | Описание                                                                                                       |
| :- | :------------------ | :------------------------------------------------------------------------------------------------------------- |
| 1  | Stock Price Momentum| Сравнение текущего уровня S&P 500 с его 125-дневной скользящей средней                                        |
| 2  | Stock Price Strength| Кол-во акций на NYSE, обновивших 52-недельные максимумы по сравнению с минимумами                                  |
| 3  | Stock Price Breadth | Объём торгов по акциям с ростом против объёма по падающим акциям                                                  |
| 4  | Put/Call Ratio      | Соотношение объёма опционов Put к Call (больше — страх, меньше — жадность)                                      |
| 5  | Market Volatility   | Измеряется через индекс VIX — "индекс страха"                                                                 |
| 6  | Safe Haven Demand | Сравнение доходности акций и облигаций (например, S&P 500 против 10-летних казначейских облигаций)                     |
| 7  | Junk Bond Demand  | Разница между доходностью высокодоходных (junk) и инвестиционных облигаций (спред риска)                        |

Также существует множество локальных индексов, рассчитываемых конкретно для одной из американских акций и не несущих широкой предсказательной силы.

Вторым по популярности является индекс страха и жадности крипторынка ([https://coinmarketcap.com/charts/fear-and-greed-index/](https://coinmarketcap.com/charts/fear-and-greed-index/))

## Данные разработки имеют несколько существенных недостатков, с точки зрения российского инвестора:

1.  Российский инвестор не в силах использовать американский F&G-индекс, так как после санкций розничные инвесторы столкнулись с невозможностью аллоцировать капитал в иностранные ЦБ.
2.  Трудность налогообложения и не до конца урегулированное законодательство в сфере криптовалют, а также высокая волатильность крипторынка делают инвестирование в них привлекательным лишь для малого числа инвесторов.
3.  Американский и крипто-индексы рассчитываются ежедневно (Минимальный для наблюдения таймфрейм - D), что делает невозможным их использование в более высокочастотной торговле на минутных и часовых данных (М1,M5,M15,H1,H4 и др.)
4.  Состав предикторов крипто F&G-индекса остаётся засекреченным. Инвесторы видят лишь финальное значение, без возможности понять методологию расчётов. Вместо интерпретируемого, индекс становится похож на black-box.
5.  Индекс страха и жадности американского рынка известен своей открытой методологией, однако не меняется в течение 12 лет и состоит лишь из 7 объясняющих переменных, что может быть недостаточно для объяснения всей картины рынка.
6.  Не все из сервисов, размещающих индекс, предоставляют удобный API для взаимодействия

## Учитывая вышеописанные недостатки, предлагаются следующие нововведения:

1.  Разработка индекса на данных российского рынка
2.  Использование интерпретируемого ML-алгоритма, который сможет обработать 8 летние временные ряды российских акций и индексов (В данный момент обучающая выборка собрана за период с 2017-07-03 по 2025-03-03 и насчитывает 563827 минутных свечей).
3.  Использование более чем 7 объясняющих переменных. В данный момент в модели 140 признаков: данные Open,High,Low,Close,Volume минутных японских свечей для 23 акций из индекса московской биржи, индексов IMOEX, RTS, фьючерсов SI и GOLD. Планируется увеличение числа признаков до 150-200 шт.
4.  Расчёт индекса на минутных данных, что сделает возможным его использование в внутридневных (интрадей) торговых системах.
5.  Проект разрабатывается единолично @notfound143 (Bерещагин Иван)

продукт предоставляет пользователю (инвестору) удобный способ получать обощенную и сгруппированную информацию о рынке и возможность адаптировать свои инвестиционные стратегии с учетом новой информации — зарабатывать больше, терять меньше.

Пользуясь сервисом, инвестор может отойти от абстрактной оценки настроения рынка и возможных логических заблуждений, вызванных эмоциями. Вместо этого предлагается количественная оценка сентимента, поддающаяся интерпретации.


## Данные и ресурсы проекта

### Доступность железа:

Проект разрабатывается преимущественно локально. Для EDA и Feature Engineering 'a используется локальная среда разработки, обучение модели предполагается в Google Colab / Kaggle Notebook в случае нехватки ресурсов.

### Данные:

Датасет собирался автором проекта самостоятельно при помощи нескольких источников данных:

1.  Библиотека finam.py ([https://github.com/cia76/FinamPy](https://github.com/cia76/FinamPy)) – отсюда загружены временные ряды акций из списка индекса московской биржи
2.  Сервис «Экспорт данных» брокера Финам ([https://www.finam.ru/quote/moex/imoex/export/](https://www.finam.ru/quote/moex/imoex/export/)) – были загружены остальные данные, «склеены» и обработанные при помощи python.

### Документация датасета:

1.  23 акции из списка индекса московской биржи (из 50 были выбраны тикеры с наибольшим количеством доступным данных ) : AFLT, CHMF, FEES, GAZP, GMKN, HYDR, IRAO, LKOH, MAGN, MTSS, NLMK, NVTK, ROSN, RTKM, SBERP, SNGSP, SNGS, TATN, VTBR. Каждый из тикеров представлен в датасете 5 признаками: рядом цен открытия свечи, закрытия, минимума и максимума, а также рядом объёмов для каждой свечи. (Вместе 23 \* 5 = 115 признаков)
2.  Те же 5 признаков для индекса RTS, индекса IМОЕХ, фьючерсов SI (Фьючерс на доллар), GOLD (на золото), индекса волатильности RVI (5\*5=25 признаков)

Предполагается хранить данные локально, в дальнейшем использовать систему DvC S3 MiniO для версионирования датасета. Переобучение планируется производить раз в полгода - за этот момент может прибавиться 3-7% данных.

Исходный датасет частично собран «руками», однако уже найдены способы получения real-time данных всех признаков, которые могут добавляться в него.

В проекте используются полностью бесплатные данные из открытого доступа брокера «ФИНАМ»

### Риски проекта:

1.  Отсутствие данных по корпоративным облигациям, ОФЗ, опционам, что может негативно повлиять на предсказательную способность модели. На данный момент настроение рынка моделируется в основном на основании анализа акций, индексов и самых популярных фьючерсов.
2.  Предсказываемая переменная (Цена закрытия RVI rvi_close, отмасштабируемая в диапазон от 0 до 100) имеет данные с 2017 по 2025 год, что делает невозможным использование данных признаков за 2014-2017 год, как и предполагалось ранее. 2014 год очень важен для обучения модели, ведь именно в этот момент наблюдалась сильная волатильность таргета. Фактор также может негативно повлиять на предсказательную способность модели. Сейчас для модели остались 2 значимых периода для обучения - 2022 и 2020 годы.
3.  Главный риск - итог пунктов (1) и (2) – низкое качество предсказаний, в виду чего отсутствие интереса к использованию у ЦА, потенциальные убытки при использовании в торговых системах.

## Решаемые задачи с точки зрения аналитики

### Метрика

Будет использовано 3 типа моделей для сравнительного анализа их предсказательной способности: линейные и полиномиальные регрессии, бустинги, табформеры.

Будет использована метрика для задачи регрессии – МАРЕ.
Использование MSE нежелательно из-за низкой интерпретируемости из-за квадратичных значений. MAE / RMSE - более удачный вариант, но заранее нельзя представить желаемое значение метрики. МАРЕ измеряется в %, поэтому такой проблемы нету.

Так как предполагается тестировать модель в реальной торговле, она должна быть точно откалибрована и быстро реагировать на изменения на рынке. «Таргетом» по МАРЕ будет выступать отметка в 0.005 (в среднем прогноз должен отклоняться от фактического значения на 0,5%.)


## 3. История экспериментов и обучение модели

Перед обучением модели были проделаны следующие преобразования:
1) Преобразование временных рядов в log-return ряды.
2) Интерполяция пропущенных значений
3) Разбиение на train/val выборку в отношении 80/20. Для сохранения распределения таргета в обучающей и валидационной выборках количественный Target был преобразован в категориальную переменную ( с разбивкой на 20 бинов ), которая была подана в параметр stratify train_test_split ) 
4) Масштабирование при помощи RobustScaler

На итоговых данных был обучен табформер TabNet без гиперпараметров на 100 эпохах. Лучшие из метрик были получены при минимизации loss-функции MSE; CoshLoss и L1Loss(MAE) не смогли привести к удовлетворительным результатам.
Метрики на валидационной выборке: MAPE - 4,07 % , MAE - 0,7672 

Было принятно решение провести Feature Engineering:
1) Из log-return признаков были удалены inf значения, которые появились в ходе преобразований.
2) Были сгенерированы дополнительные признаки - скользящие средние порядка 30,60,120,240,720,1000,1440 (1 день) ,1440*1.5, 1440 * 2 ... 1440 * 7
3) Удалены пропущенные значения во всем датафрейме, которые были в новых признаках
4) В виду сложности проведения Feature Selection путём L1, Feature importance из RF, был выбран простой метод оценки влияния признаков на таргет - подсчёт их корреляции с ним. В итоге из датафрейма были
удалены признаки которые имеют слабую корреляции с таргетом (Коэф. корреляции Пирсона < 0.2). В итоговом датасете осталось 290 признаков.

Обучении TabNet на отфильтрованных данных дало лучшие результаты.
Метрики на валидационной выборке: MAPE - 2.5 % , MAE - 0.48

Для сравнения на отфильтрованных данных был обучен бустинговый алгоритм CatBoost с параметрами iterations = 15000 , early_stopping_rounds = 200, loss_function = RMSE 
Модель показала лучшие результаты, чем TabNet.
Метрики на валидационной выборке: MAPE - 1.45 % , MAE - 0.28

В модели бустинга изначально не был указан learning_rate, модель подобрала его сама. Было принято решение подобрать этот гиперпараметр с помощью Optuna.





 





