
**Matplotlib** — это популярная библиотека на языке Python, предназначенная для визуализации данных двумерной и трёхмерной графикой. Она позволяет создавать различные типы графиков, такие как линейные графики, гистограммы, круговые диаграммы, столбчатые диаграммы и многое другое.

Часть функций разобраны в [[pd.plot()]]

## matplotlib.pyplot

Модуль из библиотеки matplotlib, который обеспечивает процедурный интерфейс для построения графиков. Он часто используется для создания различных типов графиков, таких как линейные графики, гистограммы, круговые диаграммы и многое другое.

```Python
import matplotlib.pyplot as plt
```

### Быстрый старт

**Создаем фигуру и список подграфиков:**

```Python
fig, ax = plt.subplots(figsize=(15, 8))
```

**Добавляем столбцы:**

```Python
ax.bar(weekend.index, weekend.values, alpha=0.7, label='weekend', color='black', width=1, align='edge')

ax.bar(working_days.index, working_days.values, alpha=0.7, label='working_day', color='gold', width=1, align='edge')
```

**Публикуем график:**

```Python
plt.show()
```

### plt.subplots()

Функция из библиотеки matplotlib, которая позволяет создать несколько подграфиков на одной фигуре. Она возвращает два объекта: `fig` (фигура) и `axs` (список подграфиков).

```Python
fig, axs = plt.subplots(2, 1, figsize=(15, 10))
# 2 – количество строк для подграфиков
# 1 – количество столбцов для подграфиков
# figsize – размер фигуры в дюймах
```

Такой код создаст график, на котором будет объединено два графика: один сверху, другой снизу. Чтобы добавить подграфики на общий график, нужно при создании ссылаться на объект осей, заданный для `plt` – `axs`:

```Python
weekend.plot(kind='bar', x='hour', y='weekend', fontsize=8, xlabel="", title='weekend', color='darkcyan', ax=axs[0])

working_days.plot(kind='bar', x='hour', y='working_day', rot=0, fontsize=8, title='working_day', color='purple', ax=axs[1])
```

#### Добавить заголовок

```Python
fig.suptitle('Commits per hour')
```

#### Убрать подписи с тиков на оси X

```Python
axs[0].set_xticklabels([])
```

#### Добавить легенду

```Python
ax.legend(fontsize=10)
```

#### Установить ограничения по X

```Python
ax.set_xlim(0, max(weekend.index)+1)
```

## Функциональный стиль

Вы используете функции из модуля `matplotlib.pyplot`, которые автоматически создают и управляют фигурами и осями. В этом случае не нужно явно создавать объекты фигур или осей.

```Python
plt.figure(figsize=(15, 8))

plt.hist(working_days_hours, bins=24, range=(0, 24), alpha=0.7, color='gold', label='working_days')

plt.hist(weekend_hours, bins=24, range=(0, 24), alpha=0.7, color='black', label='weekend')

plt.xlim(0, 24)

plt.legend(fontsize=10)

plt.show()
```

## Объектно-ориентированный стиль

Вы создаете объекты фигур и осей явно с помощью `plt.subplots()` или `plt.figure()` и `plt.axes()`. Это дает больше контроля над графиком, но требует больше кода.

```Python
fig, ax = plt.subplots(figsize=(15, 8))

ax.hist(working_days_hours, bins=24, range=(0, 24), alpha=0.7, color='gold', label='working_days')

ax.hist(weekend_hours, bins=24, range=(0, 24), alpha=0.7, color='black', label='weekend')

ax.set_xlim(0, 24)

ax.legend(fontsize=10)

plt.show()
```
