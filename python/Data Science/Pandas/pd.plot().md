
Для построения графиков на основе данных, содержащихся в объектах `DataFrame` и `Series` используется `df.plot()`. Этот метод является оберткой над функциями библиотеки Matplotlib, что делает его удобным для визуализации данных без необходимости глубокого погружения в настройки [[matplotlib]].

## Быстрый старт

Создаем объект осей при помощи `df.plot()`, который возвращает объект осей (axes, можно сократить, как `ax`) с автоматически настроенным графиком. Либо передаем параметры графика прямо в аргументы метода, чтобы получить кастомный график.

```Python
ax = checker.plot(figsize=(15, 8), fontsize=8)
```

==Если надо наложить еще один график поверх первого==, создаем еще один график чтобы наложить его поверх предыдущего, при помощи `df.plot()`, но в параметрах указываем `ax=ax`, где первый `ax` - аргумент "объекта осей", а второй `ax` - созданный объект осей в предыдущем шаге.

## Первичные настройки при создании объекта осей ax

Для настройки дизайна наших графиков при создании нового объекта осей мы можем использовать аргументы метода `df.plot()`:

* `title=<название графика>` - добавляет заголовок над графиком.
* `figsize=(<ширина>, <высота>)` – устанавливает размер графика в дюймах.
* `fontsize=<размер>` – устанавливает размер шрифта.
* `color=['<цвет>']` – принимает список цветов для столбцов
* `colormap=<название цветовой схемы>` - раскрашивает график в соответствии с выбранной [цветовой схемой](https://matplotlib.org/stable/users/explain/colors/colormaps.html)

* `x=<название столбца для оси X>` - устанавливает связь столбца и оси, актуально для линейных диаграмм.
* `y=<название столбца для оси X>` - устанавливает связь столбца и оси, актуально для линейных диаграмм.

* `xlabel=<название>` – устанавливает название для оси X.
* `ylabel=<название>` – устанавливает название для оси Y.

**Пример:**

```Python
ax = checker.plot(kind='bar', stacked=True, figsize=(15, 8), fontsize=8, title='Commits per day', color=['darkcyan', 'darkred', 'pink', 'lightblue'])
```

## Настройки диаграммы после создания

Эти настройки применяются к объекту осей `ax`, который мы сохранили при создании первичного графика:

`ax.get_yticks()` – получает `list` со значениями меток по оси y.
`ax.get_xticks()` – получает `list` со значениями меток по оси x.

`ax.set_ylim()` – устанавливает границы оси Y на графике. Принимает два аргумента: первый – нижняя граница (0), второй – верхняя (602).
`ax.set_xlim()` – устанавливает границы оси Y на графике. Первый аргумент – нижняя граница, второй аргумент – верхняя.

`ax.axhline()` – рисует горизонтальную линию, принимает параметры `y` для указания точки, откуда пойдет линия, `color`, `linewidth`, `linestyle` (например, `'solid'`, `'dashed'`, `'dashdot'`, `'dotted'`, `-`, `-.`, `--`).
`ax.axvline()` – рисует вертикальную линию, параметры аналогичны.

## Типы диаграмм

Тип диаграммы указывается параметром `kind`, передаваемым в `df.plot()`. По умолчанию, строится линейная диаграмма, чтобы изменить настройку нужно передать аргумент со соответствующим значением:

`kind='line'` – линейная диаграмма
`kind='bar'` – вертикальная столбчатая диаграмма
`kind='barh'` – горизонтальная столбчатая диаграмма
`kind='hist'` – гистограмма
`kind='line'` – линейная диаграмма

Пример использования:

```Python
ax = checker.plot(kind='barh')
# Выведет столбчатую диаграмму горизонтально
```











## Управление осями и пределами

### ax.set_xlim(xmin, xmax) / set_ylim(ymin, ymax)
Устанавливает пределы отображения по осям X и Y. Также можно использовать `xlim()` и `ylim()`

### ax.set_xlabel(label) / set_ylabel(label)

Устанавливает подписи к осям X и Y

### ax.set_title(label)

Устанавливает заголовок графика

### ax.set_xscale(value) / set_yscale(value)

Устанавливает тип шкалы (например, 'linear', 'log').

### ax.set_xticks(ticks) / set_yticks(ticks)

Устанавливает метки на осях X и Y

###  ax.taick_params()

Изменяет внешний вид тиков и меток

## Настройка внешнего вида

### ax.set_facecolor(color)

Устанавливает цвет фона области графика.

### ax.grid(True)

Включает отображение сетки.

## Легенда
## ax.legend()

Отображает легенду графика.

## Добавление текста и аннотаций

### ax.text(x, y, s)

Добавляет текст в указанные координаты.

### ax.annotate(s, xy, xytext, arrowprops)

Добавляет аннотацию с возможностью указания стрелки.

## Работа с тиками (метками)

### xaxis.set_major_locator(locator) / yaxis.set_major_locator(locator)

Устанавливает основной локатор для меток оси (например, для задания интервала между метками).

### xaxis.set_major_formatter(formatter) / yaxis.set_major_formatter(formatter)

Устанавливает основной форматтер для меток оси (например, для задания формата чисел).

## Вспомогательные линии

### ax.axvline(x, color, linestyle, zorder)

Добавляет вертикальную линию.

### ax.axhline(y, color, linestyle, zorder)

Добавляет горизонтальную линию.





## Пример

```Python
ax = df.plot(fontsize="8", figsize=(15,8), title="Views per day", xlabel="date", rot=90)

ax.legend(['views'], loc='upper right')
```

![[Pasted image 20250220153830.png]]




### Параметры метода `plot()`

- **kind**: Тип графика (например, `'line'`, `'bar'`, `'hist'`).
- **title**: Заголовок графика.
- **xlabel**, **ylabel**: Подписи осей.
- **subplots**: Если True, создаст отдельные подграфики для каждого столбца.
- **layout**: Определяет расположение подграфиков.
- **fontsize**: Определяет размер шрифта, `fontsize=9`
- **figsize**: определяет размеры фигуры (общей области для графика) в дюймах. К примеру, `figsize=(15, 8)` означает, что ширина фигуры будет 15 дюймов, а высота - 8 дюймов.
- **rot**: определяет угол подписей значений, к примеру `rot=90` расположит их вертикально
- **x**: определяет, какие данные должны быть на оси x: `x='date'` 
- **y**: определяет, что находится на оси y: `y='views'`
- **marker**: 

