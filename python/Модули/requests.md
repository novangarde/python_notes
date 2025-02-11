
Модуль **Requests** в Python — это мощная и удобная библиотека, предназначенная для работы с HTTP-запросами. Он упрощает процесс отправки запросов к веб-серверам и обработки ответов, делая его интуитивно понятным и доступным для разработчиков.

Аналог: [[httpx]]

## Основные возможности модуля Requests

1. **Отправка различных типов запросов**:
    
    - Requests поддерживает основные HTTP-методы, такие как:
        
        - **GET**: используется для получения данных с сервера.
        - **POST**: отправляет данные на сервер, например, при заполнении форм.
        - **PUT**: обновляет существующие ресурсы.
        - **DELETE**: удаляет указанные ресурсы.
        
    
2. **Обработка ответов**:
    
    - После отправки запроса вы получаете объект `Response`, который содержит всю информацию о ответе сервера, включая:
        
        - Код состояния (например, 200 для успешного запроса).
        - Заголовки ответа.
        - Тело ответа (например, данные в формате JSON).
        
    
3. **Работа с параметрами и заголовками**:
    
    - Вы можете легко передавать параметры в запросах, используя аргумент `params` для GET-запросов и `data` для POST-запросов.
    - Requests также позволяет устанавливать пользовательские заголовки.
    
4. **Загрузка и отправка файлов**:
    
    - Модуль позволяет загружать файлы с сервера и отправлять файлы на сервер через POST-запросы.
    
5. **Обработка ошибок**:
    
    - Requests предоставляет удобные методы для обработки ошибок, такие как `raise_for_status()`, который поднимает исключение при возникновении ошибки HTTP.

## Отправка GET-запроса

```Python
import requests

response = requests.get('https://api.example.com/data')
print(response.status_code)  # Код состояния ответа
print(response.json())       # Данные в формате JSON
```

## Отправка POST-запроса с данными

```Python
data = {'key1': 'value1', 'key2': 'value2'}
response = requests.post('https://api.example.com/submit', data=data)
print(response.status_code)
```

## Передача параметров в GET-запросе

```Python
params = {'search': 'python', 'page': 2}
response = requests.get('https://api.example.com/search', params=params)
print(response.url)  # Полный URL с параметрами
```

## Загрузка файла

```Python
response = requests.get('https://api.example.com/file.jpg')
with open('file.jpg', 'wb') as f:
	f.write(response.content)
```

## Добавление заголовка в request

Зачастую браузеры отдают 404 на запросы без хедеров, поэтому стоит имитировать реальный браузер, добавляя head в тело запроса.

```Python
url = f"https://finance.yahoo.com/quote/{ticker}/financials?p={ticker}"

head = {"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"}

html = requests.get(url, headers=head)
```

## Читаем response

**Чтобы прочитать ответ от сервера:**

```Python
html = requests.get(url, headers=head)
print(html.text)
```

**Чтобы прочитать json():**

```Python
html = requests.get(url, headers=head)
print(html.text)
```
