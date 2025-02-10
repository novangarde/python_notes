
Beautiful Soup 4 — это популярная библиотека Python, предназначенная для парсинга HTML и XML документов. Она предоставляет удобный интерфейс для извлечения данных из веб-страниц, что делает её идеальным инструментом для веб-скрапинга.

## Использование

`url = f"https://finance.yahoo.com/quote/{ticker}/financials?p={ticker}"

`head = {"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"}

`html = requests.get(url, headers=head)

`if html.status_code != 200: raise Exception(f"Ответ сервера: {html.status_code}")

`soup = BeautifulSoup(html.text, 'html.parser')

В переменной soup сохраняется объект, который мы распарсили из html.txt. Во втором аргументе указывается встроенный парсер, который будет "разбирать" объект. Это может быть `html.parser`, `lxml` и `html5lib`.

## Методы

Beautiful Soup предоставляет несколько методов для поиска элементов на веб-странице. Вот основные из них:

## 1. `find()`

- **Описание**: Находит первый элемент, соответствующий заданным критериям.
- **Пример**:
    
    `first_div = soup.find('div', class_='example')`
    
## 2. `find_all()` (или `findAll()`)

- **Описание**: Находит все элементы, соответствующие заданным критериям.
- **Пример**:
    
    `all_divs = soup.find_all('div', class_='example')`
    

## 3. `select()`

- **Описание**: Позволяет использовать CSS-селекторы для поиска элементов. Это более мощный и гибкий способ поиска.
- **Пример**:
    
    `elements = soup.select('.example')  # Находит все элементы с классом "example"`
    

## 4. `select_one()`

- **Описание**: Находит первый элемент, соответствующий заданному CSS-селектору.
- **Пример**:
    
    `first_element = soup.select_one('.example')`
    

## 5. Поиск по атрибутам

Вы можете использовать параметры для фильтрации по атрибутам:

`link_with_id = soup.find('a', id='link2')  # Находит <a> с id='link2' links_with_class = soup.find_all('a', class_='sister')  # Находит все <a> с class='sister'`

## 6. Поиск по тексту

Можно искать элементы, содержащие определённый текст:

`elements_with_text = soup.find_all(string="Some text")`

## 7. Навигация по дереву

Beautiful Soup также предоставляет методы для навигации по дереву HTML:

- `find_parent()` и `find_parents()`: ищут родительские теги.
- `find_next_sibling()` и `find_previous_sibling()`: ищут соседние теги на одном уровне.

## Примеры использования

## Пример с использованием `find_all()`

`from bs4 import BeautifulSoup html = "<div class='example'>Example</div><div class='example'>Example 2</div>" soup = BeautifulSoup(html, 'html.parser') # Найти все div с классом 'example' divs = soup.find_all('div', class_='example') for div in divs:     print(div.text)`

## Пример с использованием CSS-селекторов

`# Используя select для поиска элементов elements = soup.select('div.example') for element in elements:     print(element.text)`