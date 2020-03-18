# Обзор моделей

## K Nearest Neighbors

### Принцип работы

Модель рассчитывает растояние от объекта (точки данных) до всех объектов обучающей выборки и выбирает из них k ближайших. На основании этого выбирает искомый класс для точки данных. Обычно путем выбора преобладающего класса среди k ближайших.

### Основные параметры настройки

|   Параметры   |    Описание     |  Диапазон  |  
| :-----------: | :-------------: | :--------: |
| k 			| Кол-во соседей  | *1-N*      |

### Особенности работы с моделью

- При использовании алгоритма ближайших соседей важно выполнить предварительную обработку данных


### Достоинства

- Модель легко интерпретировать
- Построение происходит очень быстро

### Недостатки

- Не так хорошо работает, когда речь идет о наборах данных
с большим количеством признаков
- Особенно плохо работает в ситуации, когда подавляющее число признаков в большей части наблюдений имеют нулевые значения

## Multinomial logistic regression

### Принцип работы

Модель разделяет пространоство объектов с помощью гиперплоскости, которая строится путем минимизации функции потерь. 

### Основные параметры настройки

|   Параметры   |    Описание     		 |  Диапазон  |  Пояснение 					    |
| :-----------: | :-------------: 		 | :--------: | :-----------------------------: |
| C 			| Степень регуляризации  | *0-Inf*    | Больше C - меньше регуляризация |
| penalty		| Способ регуляризации   |['l1', 'l2']| l1 может обрщать веса модели в 0|

### Особенности работы с моделью

- При мультиклассовой классификации общераспространненным подходом является метод *one-vs-all*, где для
каждого класса строится бинарная модель, которая пытается отделить этот класс от всех остальных
- Если для модели важны лишь некоторые признаки или полезна интепретируемость, следует использовать L1-регуляризацию; в противном случае L2 регуляризацию
- Работает хорошо, когда количество признаков превышает количество наблюдений


### Достоинства

- Быстро обучается 
- Быстро прогнозирует

### Недостатки

- Если набор данных содержит высоко коррелированные признаки, то коэффициенты сложно интерпретировать
- Работает хуже в низкоразмерном пространстве признаков


## Support vector machine

### Принцип работы

Отличием данной модели от обычной линейной заклчается в том, что она получает расширенное пространство признаков без фактического добавления новых признаков, вычисляя скалярное произведение между объектами.

### Основные параметры настройки

|   Параметры   |    Описание     		 	 |  Диапазон  		   |  Пояснение 					   		  |
| :-----------: | :-------------------: 	 | :--------: 		   | :-------------------------------:		  |
| C 			| Степень регуляризации  	 | *0-Inf*    		   | Больше C - меньше регуляризация 		  |
| kernel		| Выбор типа ядра			 |‘linear’,‘poly’,‘rbf’| 										  |
| gamma			| Ширина гауссовского ядра   |'scale' или *0-Inf*  | Меньше gamma - точки рассм-ся как близкие|


### Особенности работы с моделью

- Высокое значение 'gamma' дает более сложную модель
- SVM требует, чтобы все признаки были измерены в одном и том же масштабе

### Достоинства

- Обладает мощной прогнозной силой
- Позволяет строить сложные решающие границы 

### Недостатки

- Плохо масштабируется с ростом объема данных
- Требует тщательной предварительной обработки данных и настройки параметров

## Multinominal naive bayes

### Принцип работы

Модель оценивает признаки, рассматривая каждый отдельно, и по каждому признаку собирает статистики классов (в данном случае среднее значение каждого признака для каждого класса), на основе которых выносит решение.

### Основные параметры настройки

|   Параметры   |    Описание     		 	 |  Диапазон  		   |  Пояснение 					   		  |
| :-----------: | :-------------------: 	 | :--------: 		   | :-------------------------------:		  |
| alpha			| Сложность модели		  	 | *0-Inf*    		   | Больше alpha - больше сглаживание модели |

### Особенности работы с моделью

- Используется в основном на рареженных дискретных данных или на очень больших наборах данных  
- Существуют также Gaussian и Bernoulli класификаторы. Bernoulli принимает бинарные значения, а Gaussian записывает среднее значение, а также стандартное отклонение каждого признака для каждого класса. Gaussian используется для данных с очень высокой размерностью  

### Достоинства

- Быстро обучается
- Быстро прогнозирует
- Процесс обучения очень легко интерпретировать
- Хорошо работает с высокоразмерными разреженными данными
- Относительно устойчива к изменениям параметров 

### Недостатки

- Плохо работает на низкоразмерных данных

## Random forest

### Принцип работы

Модель строит множество деревьем решений, где каждое дерево немного отличается от остальных. На основе решений каждого из деревьев модель выносит свой прогноз.

### Основные параметры настройки

|   Параметры   |    Описание     		 	 |  Диапазон  		   |  Пояснение 					   		  |
| :-----------: | :-------------------: 	 | :--------: 		   | :-------------------------------:		  |
| n_estimators	| Кол-во деревьев		  	 | *1-Inf*    		   | 								 		  |
| bootstrap		| Использование bootstrap выборки | True, False| Удаление одних элементов и дублирование других|
| max_features	| Кол-во используемых признаков | *1-M*  | Изменение кол-ва признаков рассм-ых в одной вершине|
| min_samples_split| Мин. кол-во объектов для разбиения вершины|*1-N*| Ограничивает высоту дерева			  |
| min_samples_leaf| Мин. кол-во объектов в листе|*1-N*	| Ограничивает высоту дерева			|


### Особенности работы с моделью

-  Случайность, лежащая в основе случайного леса, заставляет алгоритм рассматривать множество возможных интерпретаций

### Достоинства

- Обладает высокой прогнозной силой
- Часто дает хорошее качество модели без настройки параметров
- Не требует масштабирования данных
- Хорошо работает на очень больших наборах данных
- Обучение можно распараллелить между несколькими ядрами процессора 

### Недостатки

- Плохо работает на данных очень высокой размерности
- Медленно обучается