Метод `items()` возвращает представление всех пар "ключ-значение" в словаре, кортежи.

`COMPANIES = {
 ``   'Apple': 'AAPL',
``    'Microsoft': 'MSFT',
``    'Netflix': 'NFLX',
``    'Tesla': 'TSLA',
``    'Nokia': 'NOK'
`}

`for key, value in COMPANIES.items():
``    print(key, value)

Здесь мы перебираем все `key` в `COMPANIES` и находим к ним все `value`, а затем выводим на экран.