
Стандартная библиотека, которая обеспечивает интерфейс для работы с базами данных SQLite. SQLite — это легковесная дисковая база данных SQL, не требующая отдельного серверного процесса для своей работы. Она позволяет хранить данные в локальных файлах, что делает ее удобным выбором для приложений с небольшими объемами данных.

## sqlite3.connect()

Метод, который используется для создания соединения с базой данных SQLite. Эта функция возвращает объект класса `Connection`, который позволяет взаимодействовать с базой данных, выполнять SQL-запросы и управлять транзакциями.

```Python
con = sqlite3.connect('../data/checking-logs.sqlite')
query = "PRAGMA table_info(pageviews);"
df_schema = pd.read_sql(query, con)
print(df_schema)
```

## con.close()

Метод, который используется для закрытия соединения с базой данных SQLite. Этот метод вызывается на объекте соединения (`con`) после завершения работы с базой данных.

```Python
con = sqlite3.connect('../data/checking-logs.sqlite')
con.close()
```

### con.cursor()

Создаёт объект курсора (`cur`), который используется для выполнения SQL-запросов к базе данных.

```Python
cur = con.cursor()
```

### cur.execute()

Выполняет указанный SQL-запрос на базе данных.

```Python
cur.execute("DROP TABLE IF EXISTS datamart;")
```

### con.commit()

Сохраняет изменения, сделанные в базе данных после последнего вызова метода commit(). Если вы не вызываете этот метод, ваши изменения не будут сохранены.

**Пример**: После выполнения запроса на добавление или изменение данных: `con.commit()`

```Python
con.commit()
```

## sqlite_master

Это системная таблица в SQLite, которая содержит информацию о схеме базы данных. В ней хранятся метаданные обо всех объектах базы данных, таких как таблицы, представления, индексы и триггеры.

В этой таблице есть несколько полезных столбцов:
- `type`: Тип объекта (таблица, индекс, представление, триггер).
- `name`: Имя объекта.
- `tbl_name`: Имя таблицы, к которой относится объект.
- `sql`: SQL-запрос, использованный для создания объекта.

```SQLite
SELECT * FROM sqlite_master WHERE type='table';
/* Вернет все таблицы, находящиеся в базе данных */
```

