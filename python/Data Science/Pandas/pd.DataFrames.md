import pandas as pd

import sqlite3

import matplotlib.pyplot as plt

  

con = sqlite3.connect('../data/checking-logs.sqlite')

  

ab = pd.read_csv('../data/ab-test.csv')

ab = ab.loc[ab['group'] == 'test']

ab = ab.groupby('uid').mean('diff').reset_index()

# print(ab)

  

query = """

SELECT uid, COUNT(*) AS commits

FROM checker

WHERE labname != 'project1' AND uid LIKE 'user_%'

GROUP BY uid

"""

checker = pd.read_sql(query, con)

# print(checker.sort_values('uid'))

  

query = """

SELECT uid, COUNT(*) AS pageviews

FROM pageviews

WHERE uid LIKE 'user_%'

GROUP BY uid

"""

pageviews = pd.read_sql(query, con)

# print(pageviews.sort_values('uid'))

  

combine = pd.merge(ab, pageviews, how='left', on='uid')

combine = pd.merge(combine, checker, how='left', on='uid')

print(combine)

  

con.close()
**DataFrame** — это одна из основных структур данных в библиотеке pandas, предназначенная для работы с табличными данными. Его можно представить как двумерную таблицу, аналогичную таблицам в базах данных или листам в Excel.

```Python
import pandas as pd
data = {
    'Имя': ['Анна', 'Борис', 'Виктор'],
    'Возраст': [28, 34, 29],
    'Город': ['Москва', 'Санкт-Петербург', 'Новосибирск']
}
df = pd.DataFrame(data)
```

**DataFrame можно создать из словаря**, у которого в ключах строковые значения колонок, а в значениях - серии или списки. То есть, если мы предоставим такой словарь методу `pd.DataFrame(<наш словарь>)`, то конструктор преобразует `Series` и списки в единообразные `Series` внутри `DataFrame`.

**Series** — это одномерная структура данных Pandas.

### pd.set_option()

Используется для установки различных параметров, которые влияют на поведение и отображение данных. Эти параметры могут быть связаны с вычислениями, отображением данных или другими аспектами работы с DataFrame.

**Параметры**: Существует множество доступных параметров, которые можно изменить с помощью `.set_option()`. Например:

* `display.max_rows`: Количество строк для отображения.
* `display.max_columns`: Количество столбцов для отображения.
* `display.float_format`: Формат вывода чисел с плавающей запятой.

**Синтаксис**:
```Python
pd.set_option('parameter_name', value)
```

**Пример:**
```Python
pd.set_option('display.float_format', lambda x: '%.2f' % x)
# устанавливает для всех float-значений отображение дробей до сотых
```

Сбрасывается методом [[#pd.reset_option()]]

### pd.reset_option()

Сбрасывает опции, установленные в [[#pd.set_option()]]

```Python
pd.reset_option('display.float_format')
# сбросит настройки, установленные для float
```

### df.sample()

Позволяет получить случайную подвыборку из DataFrame или Series. Он используется для выбора определенного количества строк или доли данных из исходного набора.

В NumPy есть [[NumPy#^np.random.seed(<число>)|метод]], который работает похожим образом.

```Python
df.sample(n=None, frac=None, replace=False, weights=None)

# n - Количество строк для выборки.
# frac - Доля данных для выборки (например, 0.5 для половины данных).
# replace - Позволяет повторно выбирать строки (`True`) или нет (`False`).
# weights - Вектор весов для каждого элемента (должен быть нормализован).
```

**Пример:**

```Python
df = df.sample(n=200, replace=True, random_state=21)

# n - создаем новую выборку из 200 случайных записей
# replace - означает, что будем использовать записи повторно
# random_state - используется для обеспечения воспроизводимости результатов
```

**Несколько слов о random_state**:

* **Псевдослучайные числа**: Когда вы вызываете метод `.sample()`, Pandas использует генератор псевдослучайных чисел для выбора строк из DataFrame. Эти числа не являются истинно случайными, а скорее предопределенной последовательностью чисел.
* **Начальное состояние**: Параметр `random_state` задает начальное состояние этого генератора. Если вы используете одно и то же значение для `random_state`, то каждый раз при запуске кода будет получаться одна и та же последовательность псевдослучайных чисел.
* Использование `random_state=21` означает, что каждый раз при вызове: `unique_combinations.sample(n=200, replace=True, random_state=21)` вы будете получать одну и ту же выборку из 200 строк из вашего набора данных (`unique_combinations`). Это полезно для отладки или сравнения результатов разных экспериментов.
* Если бы вы не указали значение для `random_state`, то каждая новая выборка была бы другой (если только вы явно не установите seed NumPy с помощью функции `np.random.seed()`).

### pd.concat()

Используется для объединения объектов Pandas (например, DataFrame или Series) вдоль определенной оси. Эта ось может быть либо по строкам (`axis=0`), либо по столбцам (`axis=1`).

**Пример:**

```Python
con_cat_rows_df = pd.concat([df, new_df], ignore_index=True)

# ignore_index=True используется, если исходные индексы не имеют значения или вы хотите сбросить их на последовательность
```

### pd.series()

Используется для создания одномерного массива данных с метками или индексами. Это одна из основных структур данных в Pandas, наряду с DataFrame.

```Python
import pandas as pd

# Создание Series из списка
data = pd.Series([1, 2, 3])
print(data)

# Создание Series со своим индексом
indexed_data = pd.Series([10, 20], index=['a', 'b'])
print(indexed_data)

# Создание Series из словаря
dict_data = {'x': 1000}
series_from_dict = pd.Series(dict_data)
print(series_from_dict)
```

### pd.merge()

Используется для объединения двух DataFrame по общему столбцу или набору столбцов. Это мощный инструмент для работы с данными, позволяющий выполнять различные типы соединений между таблицами.

**Основные параметры**

- **`left` и `right`**: Левый и правый DataFrame для объединения.
- **`on`, `left_on`, `right_on`**: Колонки, по которым будет происходить соединение.
	* Если колонки имеют одинаковые названия в обоих DataFrame, то можно использовать просто `on`.
    - Если названия колонок разные, то используйте `left_on` и `right_on`.

- **`how='inner'`, `'left'`, `'right'`, `'outer'`: Тип соединения**:    
    - **Inner Join**: Возвращает только строки с совпадающими значениями в обоих DataFrame.
    - **Left (Outer) Join**: Возвращает все строки из левого DataFrame плюс соответствующие им строки из правого. Если нет совпадений — значения будут NaN.
    - **Right (Outer) Join**: Аналогично левому, но берет все строки из правого DataFrame.
    - **Full Outer Join (`how='outer'`)`: Возвращает все возможные комбинации строк из обоих наборов данных.

```Python
inner_join_result = pd.merge(fines[['CarNumber']], owners[['CarNumber', 'SURNAME']], on='CarNumber')

left_join_result = pd.merge(fines[['CarNumber']], owners[['CarNumber', 'SURNAME']], how='left', on='CarNumber')

right_join_result = pd.merge(fines[['CarNumber']], owners[['CarNumber', 'SURNAME']], how='right', on='CarNumber')

outer_join_result = pd.merge(fines[['CarNumber']], owners[['CarNumber', 'SURNAME']], how='outer', on='CarNumber')
```

### pd.pivot_table()

Используется для преобразования данных из длинной формы в широкую, создавая сводные таблицы. Она позволяет агрегировать данные по различным категориям и применять различные функции агрегации (например, сумма, среднее значение) к значениям.

**Основные параметры**

- **`index`**: Указывает столбцы или индекса DataFrame, которые будут использоваться как строки результирующей таблицы.
- **`columns`**: Определяет столбцы или категории данных, которые станут новыми столбцами в сводной таблице.
- **`values`**: Указывает на те данные, которые будут агрегированы и заполнены в ячейках новой таблицы.
- **`aggfunc='sum'`, `'mean'`, `'max'`, etc.**`: Функция агрегации для обработки дублирующихся записей.

**Пример:**

Был DataFrame `fines`:

```Python
CarNumber Refund Fines Make Model Year
0 Y163O8161RUS 2 3200.00 Ford Focus 1989.00
1 E432XX77RUS 1 6500.00 Toyota Camry 1995.00
2 7184TT36RUS 1 2100.00 Ford Focus 1984.00
3 X582HE161RUS 2 2000.00 Ford Focus 2015.00
4 92918M178RUS 1 5700.00 Ford Focus 2014.00
```

Я перегруппировал данные таким образом:

```Python
grouped_fines = fines.groupby(['Make', 'Model', 'Year'])['Fines'].sum().reset_index()
```

Теперь вывод `grouped_fines` выглядит так:

```Python
Make Model Year Fines
0 Audi 2003.004200.00
1 BMW 1987.00 2200.00
2 BMW 2012.00 3000.00
3 BMW 2015.00 8594.59
4 BMW 2018.00 6500.00
```

Из этого состояния я могу вызвать `pivot_table()`, чтобы пересобрать таблицу нужным мне образом:

```Python
pivoted_fines = pd.pivot_table(grouped_fines,
                               index=['Make', 'Model'],
                               columns='Year',
                               values='Fines',
                               aggfunc='sum')
```

Теперь у нас есть DataFrame `pivoted_fines` следующего содержания:

```Python
Year           1980.00 1981.00 1982.00 1983.00 1984.00 1985.00
Make Model
Audi           NaN     NaN     NaN     NaN     NaN     NaN
BMW            NaN     NaN     NaN     NaN     NaN     NaN
Ford Focus     82094.59 425489.17 160583.76 55900.00 97289.17 121183.76
	 Mondeo    NaN     NaN     NaN     NaN     NaN     NaN
Skoda Octavia  1900.00 NaN 6900.00 11594.59 NaN 10294.59
Toyota Camry   13500.00 8594.59 NaN 7200.00 NaN NaN
	   Corolla NaN     NaN     2000.00 1100.00 NaN     NaN
Volkswagen     NaN     NaN     NaN     NaN     NaN     NaN
	   Golf    30900.00 NaN    NaN     8594.59 300.00  24000.00
	   Jetta   NaN     NaN     NaN     NaN     NaN     NaN
	   Passat  600.00  1600.00 NaN     3200.00 10000.00 5000.00
	   Touareg NaN     NaN     NaN     NaN     NaN     5800.00
Volvo          NaN     NaN     6800.00 NaN     NaN     NaN
```

### df.copy()

Создает копию DataFrame. По умолчанию (`deep=True`) он производит глубокую копию, что означает создание нового объекта с отдельной копией данных и индексов. Это позволяет изменять копию независимо от оригинала и наоборот.

**Основные особенности**

1. **Глубокая копия**:
    
    - Когда `deep=True`, изменения в оригинале не влияют на копию.
    - Этот режим является стандартным для `copy()`.
    
2. **Поверхностная (мелкая) копия**:
    
    - Если указать `deep=False`, то будет скопирована только ссылка на данные.
    - Изменения в одном объекте повлияют на другой.
    
3. **Применение**:
    
    - Используйте для создания независимых версий DataFrame, чтобы избежать непредвиденных изменений исходных данных

```Python
new_df = df.copy()
```
