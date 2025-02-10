
Метод `__init__` в Python — это специальный метод, который выполняет роль конструктора класса. Он автоматически вызывается ==первым== при создании нового экземпляра класса и используется для инициализации атрибутов объекта. Давайте подробнее рассмотрим его назначение и полезность.

1. **Создание метода _ _ init_ _**

```Python
class Employee:
	def __init__(self, full_name, emp_id, department):
		self.full_name = full_name
		self.emp_id = emp_id
		self.department = department
```

2. **Создание экземпляра класса**

```Python
	employee_1 = Employee("Алексей Иванов", 12345, "Отдел продаж")
```

3. **Доступ к атрибутам класса**

```Python
print(employee_1.full_name)  # Выведет: Алексей Иванов
print(employee_1.emp_id)      # Выведет: 12345
print(employee_1.department)   # Выведет: Отдел продаж
```
