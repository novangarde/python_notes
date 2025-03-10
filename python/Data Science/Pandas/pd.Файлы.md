
### pd.read_csv

Метод для чтения файлов формата .csv, файлов, в которых столбцы отделены между собой табуляцией. Пример:

```Python
import pandas as pd

filepath = "../data/feed-views.log"

df = pd.read_csv(filepath, skiprows=[2, 3], skipfooter=2, engine='python', header=None, names=['datetime', 'user'])

# skiprows - пропускает строки под индексами 2 и 3 (в нашем примере)

# skipfooter - пропускает последние две строки (в нашем случае)

# engine='python' - указываем движок `Python`, потому что когда вы используете аргументы `skiprows` и `skipfooter`, Python-движок часто является обязательным для корректной работы этих функций. Это связано с тем, что движок Python позволяет более гибко обрабатывать строки и футер.

# header=None, names=['date_time', 'user'] - указывает на отсутствие заголовков в файле и сразу добавляет их в виде `date_time` и `user`.
```

После прочтения файл сохраняется в переменную `df`, с которой мы дальше можем работать, изменяя заголовки, назначая индексы и т.д.

> Также при чтении файла может понадобиться указать параметр `sep='\t'`, чтобы метод разделил колонки по разделителю, иначе вся строка может попасть в одну колонку. 

### df.to_csv()

Объект pandas можно сохранить в .csv формате и сразу установить разделитель

```Python
df.to_csv('output.csv', sep=';')

# Параметр sep (separator) - устанавливает разделитель между колонками
```

### df.to_excel()

```Python
df.to_excel('ваш_файл.xls', index=False)
```

### df.to_json()

```Python
df.to_json('../data/auto.json', orient='records')
```

**`orient='records'`**: Этот параметр указывает Pandas сохранять данные так, чтобы каждая строка была представлена как отдельный словарь (запись). Это соответствует вашему желаемому формату.
