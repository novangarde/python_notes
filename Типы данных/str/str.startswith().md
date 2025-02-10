
Метод `.startswith()`, который используется для проверки, начинается ли строка с указанной подстроки. Этот метод возвращает `True`, если строка начинается с заданного префикса, и `False` в противном случае.

`string.startswith(prefix[, start[, end]])

- **prefix**: строка или кортеж строк, с которыми необходимо проверить начало строки.
- **start** (необязательный): индекс, с которого начинается проверка.
- **end** (необязательный): индекс, на котором заканчивается проверка.

#### Пример 1: без дополнительных параметров

```Python
text = "Python programming"
print(text.startswith("Python"))  # True
print(text.startswith("programming"))  # False
```
#### Пример 2: с параметрами start и end

```Python
text = "Python programming is fun"
print(text.startswith("programming", 7))  # True
print(text.startswith("Python", 0, 6))  # True
print(text.startswith("Python", 1, 6))  # False
```

#### Пример 3: с использованием кортежа

```Python
text = "Python programming"
print(text.startswith(("Java", "Python")))  # True
print(text.startswith(("Java", "C++")))  # False
```
