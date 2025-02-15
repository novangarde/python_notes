
### df.apply()

Используется для применения пользовательской функции к каждому элементу, столбцу или строке DataFrame. Он позволяет выполнять операции над данными без использования циклов, что делает код более компактным и читаемым.

#### Принцип работы

- **Применение к столбцам или строкам**: Метод `apply()` может применяться как к столбцам (`axis=0`), так и к строкам (`axis=1`) DataFrame. Это зависит от значения параметра `axis`.
- **Обработка данных**: Передаваемая функция принимает Series (в случае обработки по столбцам) или ряды (при обработке по строкам) и выполняет над ними необходимые действия.
- **В передаваемую функцию передается value**: когда мы вызываем функцию для обработки значений колонки или строки, в параметры этой функции передается переменная `value`, с которой и нужно работать. Она, как в цикле, обрабатывает строки/колонки.
- **Вернуть нужно pd.Series:** передаваемая функция должна возвращать `pd.Series()`, потому что все ряды/колонки обрабатываются циклами и сохраняют серии.

```Python
def split_make_model(value):
    parts = value.split()
    if len(parts) >= 2:
        make = parts[0]
        model = ' '.join(parts[1:])
    else:
        make = parts[0]
        model = ''
    return pd.Series({'Make': make, 'Model': model})

df[['Make', 'Model']] = df['Make_n_model'].apply(split_make_model)
```

В методе apply не обязательно вызывать какую-то отдельную функцию. Можно прописать логику прямо внутри окошка аргументов, используя lambda-функцию:

```Python
fines_apply = fines

fines_apply['NewColumn'] = fines_apply.apply(lambda x: x['Fines'] / x['Refund'] * x['Year'], axis=1)

print(fines_apply)
```

### df.itrows()

Позволяет итерировать по строкам DataFrame. Он возвращает итератор, генерирующий пары `(index, Series)`, где `index` — индекс строки, а `Series` — объект Series, содержащий данные этой строки.

```Python
fines_iterrows = fines.copy()

def calculate_fines_refund_year_iterrows(df):
    result = []
    for index, row in df.iterrows():
        value = row['Fines'] / row['Refund'] * row['Year']
        result.append(value)
    return result
    
fines_iterrows['NewColumn'] = calculate_fines_refund_year_iterrows(fines_iterrows)

print(fines_iterrows)
```
