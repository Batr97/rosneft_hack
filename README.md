# rosneft_hack

Задача:

На основе предоставленных данных построить модель прогнозирования дебита жидкости (признак ‘Q_OIS’) после геолого-технического мероприятия (ГТМ) – итенсификация добычи нефти (ИДН). Прогноз необходимо сделать на дату выхода скажины на режим (дата ВНР). Точка прогноза однозначно задается бинарным признаком ‘VNR’ (точка прогноза – VNR=1).

Каждому событию ИДН предшествует своя история, однозначно определяемая признаком ‘id’. В тренировочном датасете ‘contest_train_df.csv’ для каждого факта ИДН (признак ‘id’) известно значение дебита жидкости ‘Q_OIS’ на дату ВНР (VNR=1), а в тестовом датасете ‘contest_test_df.csv’ , соответственно, нет.

Также в качестве дополнительной информации дана таблица со всеми типами ГТМ, проведенными на исследуемых скважинах.

Необходимо сделать прогноз на тестовых данных и загрузить таблицу с прогнозами в соотвествии с форматом ‘submit_sample.csv’.
Примечание. В качестве фактов ИДН рассматриваются типы ГТМ: ИДН (код 2) и ППР (код 7).

Оценка качества алгоритма
В качестве метрики используется Mean Average Percentage Error (MAPE)

Решение:

В качестве решения врмеенных рядов используется классичесий ML-подход, где данные обрабатываются следующим образом:

![image](https://user-images.githubusercontent.com/79765625/151449329-ee13716c-65de-4d44-9b94-3d21593c74a6.png)

Здесь представлен дебит скважины с одним id в течение определенного промежутка времени, то есть одним испытанием ИДН.
![image](https://user-images.githubusercontent.com/79765625/151449090-77cbd7dd-f81e-4011-907e-0fff3f75bf63.png)

В качестве метрики используется MAPE: 
![image](https://user-images.githubusercontent.com/79765625/151449627-180720b3-ac0f-4798-bb1a-2c1c474f199a.png)

Предсказательная модель - XGBRegressor.
