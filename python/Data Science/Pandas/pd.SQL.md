
Для работы с SQL сначала нужно подключиться к базе данных и создать соединение. К примеру, если мы работаем с SQLite, используем методы модуля [[sqlite3]].

## pd.read_sql()

Позволяет считывать SQL-запросы или таблицы базы данных в DataFrame. Эта функция является удобной оберткой вокруг двух других: `read_sql_table()` для чтения таблиц напрямую по имени и `read_sql_query()` для выполнения произвольных SQL-запросов.

```Python
import pandas as pd
import sqlite3

con = sqlite3.connect('../data/checking-logs.sqlite')
query = "PRAGMA table_info(pageviews);"
df_schema = pd.io.sql.read_sql(query, con) # pd.read_sql(query, con) - то же самое

print(df_schema)

con.close()
```

Принимает два параметра:
* Запрос
* Соединение

