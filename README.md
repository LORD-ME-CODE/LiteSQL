# LiteSQL 
База данных? Без проблем!

# КРАТКАЯ ДОКУМЕНТАЦИЯ
Привет! Эта библиотека создана для простого и быстрого создания и редактирования базы данных формата SQL.
 Библиотека основана на sqlite3

Pypi - https://pypi.org/project/LiteSQL

## Импорты
Рекомендуем использовать from LiteSQL import lsql (он будет рассмотрен тут), но есть и другие варианты импорта.

## lsql.connect(file_name)
Открывает файл БД если он существует, либо создает его и открывет (Имя файла писать без .bd)

file_name - имя файла без .bd
## lsql.create(names, table="albums")
Создает столбцы таблицы

names - строка в виде названий столбцов через ", ", например "Имя, Улица"
table - название подтаблицы, по умолчанию albums (не спрашивайте почему) - больше не буду про него писать

## lsql.insert_data(data_mass, len_title, table="albums")
Вставляет данные в таблицу по строкам с помощью массива

data_mass - массив с кортежами через запятую (если их несколько), например [("Вася", "Покровская")] для одного заполнения одной строки из 2 столбцов или [("Петя", "Ленина"), ("Лена", "Уфимская")] для заполнения сразу 2-х строчек из 2-х столбцов.
len_title - число столбцов в БД (да, я не мог сделать функцию, которая это определяет)

## lsql.edit_data(title_last, last, title_new, new, table="albums")
Изменяет данные в конкретной ячейке таблицы
title_last - название столбца поиска 
last - данные, которые мы ищем в конкретном столбце для выявления строки (строк)
(предыдущие 2 всего лишь находят строку, в которой надо что-то изменить, но никак не влияют на изменение)
title_new - название столбца, данные в котором надо изменить 
new - данные, которые нужно вписать в ячейку конкретного столбца этой строки

## lsql.delete_data(name, title_name, table="albums")
Удаление строки (строк), где присутсвует конкретное имя в конкретном столбце

name - данные, которые мы ищем в конкретном столбце для последующего удаления найденой строки
title_name - столбец для поиска данных

## lsql.select_data(name, title, row_factor=False, table="albums")
Поиск и возврат данных в переменную по данным и столбцу

name - данные, которые мы ищем в конкретном столбце для вывода строки
title - название столбца поиска
row_factor - тип вывода данных, по умолчанию выключен и выводится в формате fetchone, если передать True - вернется в fetchall

## lsql.select_data_with_sort(type_sort, name, title_name, table="albums")
Тоже самое, что и с lsql.select_data, но с сортировкой. name можно придать None, и тогда вернется только столбик

type_sort - тип сортировки (подробнее в документации sqlite3)
name - данные, которые мы ищем в конкретном столбце для вывода строки
title - название столбца поиска

## lsql.search(type_search, name_search, table="albums")
Поиск данных в БД и возврат их в переменную

type_search - тип поиска (например - title - столбцы)
name_search - имя, которое мы ищем (в том числе с помощью неопределенности - например % может искать любое количество любых символов в имени, даже 0), например "у%ица"

# Примеры
```python
from LiteSQL import lsql
lsql.connect('test_LiteSQL') #Соединяемся с БД по имени test_LiteSQL.bd
lsql.create('id, hash') #Создаем 2 столбца - id и hash
lsql.insert_data([('234', '234'), ('3234235', '134234234')], 2) #Добавляем данные
a = lsql.select_data('234', 'id') #Ищем строку, в которой id = '234'
print(a) #Результат - [('234', '234')]
lsql.edit_data('id', '234', 'id', '1234') #Изменяем данные - там, где id = 234, теперь id = 1234
a = lsql.select_data('1234', 'id') #Ищем строку, в которой id = '1234'
print(a) #Результат - [('1234', '234')]
b = lsql.search('id', '3%34%5') #Поиск строк с помощью специальных фильтров
print(b) #Результат - [('3234235', '134234234')]
v = lsql.select_data_with_sort('rowid', None, 'id') #Сортировка строк по возрастанию данных в id
print(v) #Результат - [(1, '1234', '234'), (2, '3234235', '134234234')]
```

# Контакты

Что-то не работает, есть вопросы, пожелания? Пиши - vk.com/maks.mushtriev2, t.me/Error_mak25

Мой блог - vk.com/mamush_blog

Донат - vk.cc/az7BQK (Киви)


# Удачи!
