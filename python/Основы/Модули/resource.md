
Модуль **`resource`** в Python предоставляет механизмы для измерения и контроля системных ресурсов, используемых программой. Он позволяет получать информацию о времени выполнения, использовании памяти и других ресурсах, что полезно для оптимизации производительности приложений.

## Основные функции и возможности модуля resource

1. **Получение информации о ресурсах:**
    
    - Функция `resource.getrusage(who)` возвращает информацию о ресурсах, потребляемых текущим процессом или его дочерними процессами. Аргумент `who` может быть одной из следующих констант:

        - `resource.RUSAGE_SELF`: ресурсы текущего процесса.
        - `resource.RUSAGE_CHILDREN`: ресурсы дочерних процессов.
        - `resource.RUSAGE_BOTH`: ресурсы текущего процесса и его дочерних процессов.

2. **Поля возвращаемого значения:**
    
    - Функция возвращает объект, содержащий информацию о различных ресурсах, включая:

        - `ru_utime`: время в пользовательском режиме (в секундах).
        - `ru_stime`: время в системном режиме (в секундах).
        - `ru_maxrss`: максимальный размер резидентной памяти (в килобайтах).

## Как пользоваться?

1. Добавляем модуль

	`import resource

2. В конце программы вызываем функцию

	`usage = resource.getrusage(resource.RUSAGE_SELF)

	Она возвращает объект структуры, содержащий информацию о ресурсах, используемых текущим процессом (или его дочерними процессами, если вы используете `RUSAGE_CHILDREN`)

3. Достаем из usage нужные данные:

	`peak_memory = usage.ru_maxrss / (1024 * 1024) # перевод в GB
	`user_time = usage.ru_utime
	`system_time = usage.ru_stime

* `usage.ru_maxrss`: максимальный размер резидентной памяти (в килобайтах).
* `usage.ru_utime`: время в пользовательском режиме (в секундах).
* `usage.ru_stime`: время в системном режиме (в секундах).

==**Размер резидентной памяти** (Resident Set Size, RSS) — это количество страниц памяти, выделенных процессу операционной системой и в данный момент находящихся в оперативной памяти (ОЗУ). Это значение показывает, сколько физической памяти использует процесс в данный момент времени.==

