Программная библиотека на языке Python, предназначенная для обработки и анализа структурированных данных. Она особенно полезна для работы с табличными данными, такими как CSV-файлы или Excel-таблицы.

## Dataframe

**DataFrame** — это одна из основных структур данных в библиотеке pandas, предназначенная для работы с табличными данными. Его можно представить как двумерную таблицу, аналогичную таблицам в базах данных или листам в Excel.

```Python
import pandas as pd
data = {
    'Имя': ['Анна', 'Борис', 'Виктор'],
    'Возраст': [28, 34, 29],
    'Город': ['Москва', 'Санкт-Петербург', 'Новосибирск']
}
df = pd.DataFrame(data)
print(df)
```

Существует множество методов для работы с DataFrames. Разберем основные:
### read_csv

Метод для чтения файлов формата .csv, файлов, в которых столбцы отделены между собой табуляцией. Пример:

```Python
import pandas as pd

filepath = "../data/feed-views.log"
df = pd.read_csv(filepath, skiprows=[2, 3], skipfooter=2, engine='python', header=None, names=['datetime', 'user'])

print(df)
```

`skiprows` - пропускает строки под индексами 2 и 3 (в нашем примере)

`skipfooter` - пропускает последние две строки (в нашем случае)

`engine='python'` - указываем движок `Python`, потому что когда вы используете аргументы `skiprows` и `skipfooter`, Python-движок часто является обязательным для корректной работы этих функций. Это связано с тем, что движок Python позволяет более гибко обрабатывать строки и футер.

`header=None, names=['date_time', 'user']` - указывает на отсутствие заголовков в файле и сразу добавляет их в виде `date_time` и `user`.

`df.set_index('datetime', inplace=True)` - устанавливает колонку datetime индексной колонкой.

### set_index()

Вернемся к примеру выше и установим одну из колонок в качестве индекса

```Python
import pandas as pd

filepath = "../data/feed-views.log"
df = pd.read_csv(filepath, skiprows=[2, 3], skipfooter=2, engine='python', header=None, names=['datetime', 'user'])

print(df)
```

### reset_index()


### rename()


### Конвертируем .csv в .xls

```Python
import pandas as pd
# Чтение CSV файла
df = pd.read_csv('ваш_файл.csv')
# Сохранение в формате XLS
df.to_excel('ваш_файл.xls', index=False)
```

