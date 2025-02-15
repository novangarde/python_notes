
Модуль `json` в Python предназначен для работы с данными в формате JSON (JavaScript Object Notation), который является популярным форматом для обмена данными между клиентом и сервером, а также для хранения данных.

## Основные функции модуля `json`

### Кодирование (Serialization)

Функция `json.dumps()` позволяет преобразовать объекты Python (например, словари и списки) в строку формата JSON. Это полезно для сохранения данных в текстовом формате или передачи их по сети.

```Python
import json data = {'name': 'Alice', 'age': 30}
	json_data = json.dumps(data)
	print(json_data)  # Вывод: {"name": "Alice", "age": 30}
```

### Декодирование (Deserialization)

Функция `json.loads()` позволяет преобразовать строку формата JSON обратно в объекты Python. Это используется для загрузки данных из JSON-формата, например, из API или файлов.

```Python
json_data = '{"name": "Bob", "age": 25}
data = json.loads(json_data)
print(data)  # Вывод: {'name': 'Bob', 'age': 25}
```

### Работа с файлами

Модуль также предоставляет функции для чтения и записи данных в JSON-файлы:

* `json.dump()` записывает объекты Python в файл в формате JSON.
* `json.load()` загружает данные из файла формата JSON и преобразует их в объекты 

```Python
# Запись в файл
with open('data.json', 'w') as f:
	json.dump(data, f)
		
# Чтение из файла
with open('data.json', 'r') as f:
	loaded_data = json.load(f)
	print(loaded_data)`
```
