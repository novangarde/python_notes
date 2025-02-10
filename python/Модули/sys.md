Позволяет получать доступ к аргументам командной строки. К примеру, если мы вызовем скрипт командой `python3 stock_prices.py Tesla`, благодаря sys, программа получит `Tesla` в качестве входного аргумента.

К примеру, следующая программа напишет в терминале `Tesla`:
`company_name = sys.argv[1]
`def get_stock_price(company_name):
`    print(company_name) # Tesla

[[sys.executable]]
[[exit()]]