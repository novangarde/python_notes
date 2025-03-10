
## pd.cut()

Функция в библиотеке Pandas, которая используется для разделения непрерывных числовых данных на дискретные интервалы или категории. Она позволяет преобразовать непрерывные переменные в категориальные, что может быть полезно для анализа данных, создания гистограмм или сегментации пользователей.

### Основные параметры и возможности:

- **bins**: Определяет границы интервалов. Может быть массивом чисел или количеством равных интервалов.
- **labels**: Присваивает метки каждому интервалу.
- **right**: Указывает, включать ли правую границу каждого интервала (по умолчанию `True`).
- **include_lowest**: Позволяет включить самую низкую точку в первый интервал (по умолчанию `False`).

#### Пример

```Python
bins = [0, 4, 7, 11, 17, 20, 24]

labels = ['night', 'early morning', 'morning', 'afternoon', 'early evening', 'evening']

df['daytime'] = pd.cut(df['hour'], bins=bins, labels=labels)
```

В этом примере, данные колонки hour будут разбиты на интервалы от 0 до 4, от 4 до 6, от 7 до 10, от 11 до 16, от 17 до 19, от 20 до 23 при помощи `bins`

Затем, при помощи `labels` каждому из интервалов присвоится нужное значение и сохранится в новую колонку `daytime`.

#### Практика применения

Допустим, есть задача, разбить часы на следующие интервалы:
* ночь с 0:00:00 до 03:59:59
* утро с 04:00:00 до 09:59:59
* день с 10:00:00 до 16:59:59
* вечер с 17:00:00 до 23:59:59

Выделяем из даты колонку hour со значением часа, затем разбиваем его следующим образом:

```Python
bins = [-1, 3, 9, 16, 24]
labels = ['night', 'morning', 'afternoon', 'evening']
checker['daytime'] = pd.cut(checker['hour'], bins=bins, labels=labels)
```

> Начинаем с -1, чтобы в диапазон `night` попал 0-ой час.
> Второй цифрой идет 3, чтобы попало все до 03:59 и не затронуло 4
> Завершаем 24, потому что все равно нет 24-го часа

## df.describe()

Используется для генерации сводной таблицы с основными статистическими показателями для числовых столбцов DataFrame.

Пример:

```Python
stats = df['hour'].describe()
print(f"Basic statistics:\n{stats}")

# вернет статистические показатели по колонке hour
```

Статистика от `describe()`:

| Значение | Описание                                          |
| -------- | ------------------------------------------------- |
| count    | количество значений в колонке                     |
| mean     | медианное значение                                |
| min      | минимальное                                       |
| 25%      | значение на рубеже первого и второго квартиля     |
| 50%      | значение на рубеже второго и третьего квартиля    |
| 75%      | значение на рубеже третьего и четвертого квартиля |
| max      | максимальное                                      |
