
### pd.to_datetime()

Этот метод преобразует выбранный столбец в формат `datetime64[ns]`, формат даты и времени, принятый в Pandas и NumPy:

```Python
df['datetime'] = pd.to_datetime(df['datetime'])

# df['datetime'] указывает на нужный столбец в объекте
```

После преобразования мы можем создать в объекте новые столбцы, присваивая им значение из вложенного объекта dt и соответствующего атрибута:

```Python
df['year'] = df['datetime'].dt.year
df['month'] = df['datetime'].dt.month
df['day'] = df['datetime'].dt.day
df['hour'] = df['datetime'].dt.hour
df['minute'] = df['datetime'].dt.minute
df['second'] = df['datetime'].dt.second
df['datetime'] = df['datetime'].dt.date # дата, без времени и микросекунд
```

### df.astype()

Используется для явного преобразования типа данных столбцов или всего DataFrame. Он позволяет изменить тип данных элементов в массиве или серии на другой тип, например, из целых чисел в числа с плавающей запятой или из строк в целые числа.

```Python
df = fines

for col in ['Fines', 'Year', 'NewColumn']:
    df[col] = df[col].astype('float32')

df.info(memory_usage='deep')
```

