
Этот метод "закрывает" файл, вызванный командой open().

По всей видимости, [[open()]] создает объект на базе файла, куда сохраняет его содержимое и мета-данные. А close() в свою очередь удаляет этот объект и очищает память.

Метод close() можно не использовать, если файл открывается с оператором [[with]] - тогда после завершения работы файл закрывается автоматически.

### Пример использования

`f = open(input_file, 'r', encoding='utf-8')`
`f.close()