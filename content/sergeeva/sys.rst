Библиотка sys.
===============

:date: 2020-10-07 09:00
:summary: Библиотека sys
:status: published 
:author: Сергеева Ю.Д.

Модуль sys обеспечивает доступ к некоторым переменным и функциям, взаимодействующим с интерпретатором Python. Модуль sys часто используют с модулем os. С помощью sys получают нужную информацию об операционной системе, чтобы избежать непредвиденных ошибок, а с помощью os взаимодействуют с ней (работа с файлами, запуск программ на выполнение, обработка путей и так далее).

Рассмотрим следующие функции:


* sys.exec_prefix
* sys.executable
* sys.platform
* sys.argv
* sys.builtin_module_names
* sys._current_frames()
* sys.getrecursionlimit()
* sys.hexversion
* sys.modules
* sys.path
* sys.version
* sys.exit[arg]
* sys.stdin
* sys.stdout
* sys.stderr

Информация о системных параметрах
---------------------------------
sys.exec_prefix
~~~~~~~~~~~~~~~
Выводит строку, которая показывает, в какой каталог установлен Python. 

sys.executable
~~~~~~~~~~~~~~
Строка, показывающая путь к интерпретатору Python. Это очень полезно, когда вы используете чей-то компьютер, и вам нужно узнать, где установлен Python.

Если по какой-то причине определить путь к интерпретатору нельзя, sys.executable будет пустой строкой или None.

sys.platform
~~~~~~~~~~~~
Строка, дающая информацию об используемой операционной системе (идентификатор платформы). Можно использовать sys.platform чтобы добавлять модули к sys.path, импортировать разные модули, в зависимости от платформы, или запускать разные части кода. Например, можно проверить в какой мы находимся опреационной системе и установить какие действия мы в зависимости от этого хотим выполнить:

*os=sys.platform*

*if os=='win32':*

    *#работаем с Windows*

*elif os.startswith('linux'):*

    *#работаем с Linux*  

Информация о параметрах интерпретатора
--------------------------------------
sys.argv
~~~~~~~~
Список, состоящий из аргументов командной строки, которые используются в текущем скрипте.

argv[0] — это имя скрипта. Если имя скрипта не было передано интерпретатору, то argv[0] будет пустой строкой. В зависимости от платформы, на которой вы работаете, первый аргумент может содержать полный путь к скрипту или к названию файла.
Примеры:

*import sys*

*print(sys.argv)*

Такой код выведет пустой список ['']. Если же создать файл sysargv.py с таким же содержимым, то результатом вывода будет список, содержащий один элемент - путь к скрипту.

sys.builtin_module_names
~~~~~~~~~~~~~~~~~~~~~~~~
Кортеж, который показывает все доступные интерпретатору Python модули. sys.builtin_module_names — единственный способ получить эту информацию, любые другие инструменты могут показать лишь список импортированных в скрипт модулей.

sys._current_frames()
~~~~~~~~~~~~~~~~~~~~~
Возвращает словарь, дающий информацию об активных потоках.

sys.getrecursionlimit()
~~~~~~~~~~~~~~~~~~~~~~~
Возвращает максимально возможное значение рекурсии и максимальную глубину стека интерпретатора. Этот предел предотвращает переполнение стека C, который в свою очередь приводит к сбою Python. Установить предел рекурсии можно с помощью функции setrecursionlimit().

sys.hexversion
~~~~~~~~~~~~~~
Номер версии интерпретатора Python, закодированный одним числом. Это число увеличивается с каждой версией, включая все виды релизов.

sys.hexversion используют, чтобы удостовериться, поддерживает ли интерпретатор какую-либо функцию. Если нет, то функция заменяется каким-либо поддерживаемым аналогом.

sys.modules
~~~~~~~~~~~

Словарь, дающий информацию о загруженных в скрипт модулях.

Его можно изменять, чтобы принудительно перезагружать или удалять модули, однако эти манипуляции могут привести к сбою Python.

sys.path
~~~~~~~~~
Одна из наиболее важных функций.
Выводит список строк, который показывает, в каких директориях ищутся модули. Инициализируется из переменной окружения PYTHONPATH и директории по умолчанию, которая зависит от дистрибутива Python. 
Первый элемент списка (path[0]) — это директория, в которой находится скрипт, запускающий интерпретатор Python.

Как правило, эта функция указывает Python, где искать, когда он пытается импортировать модуль.
Так как sys.path - это список, то его можно изменять. Например, когда мы хотим импортировать какую-то библиотеку, пути к которой нет в sys.path. Можно добавить путь к ней с помощью sys.path.append("путь"), тогда библиотеки будут искаться и по этому пути. В sys.path могут быть добавлены только строки и байтовые строки, другие типы данных игнорируются при импорте.

sys.version
~~~~~~~~~~~
Строка, состоящая из номера версии Python, а также дополнительной информации о номере сборки и используемом компиляторе.

Функции, выполняющие действия и преобразования
-----------------------------------------------
sys.exit([arg])
~~~~~~~~~~~~~~~
Выход из Python. Вызывает исключение SystemExit, которое можно перехватить. По желанию можно передать функции аргумент, который может быть целым числом (обычно от 0 до 127), которое дает статус выхода. Ноль считается как успешное завершение, любое другое значение приводит к «неуспешному завершению». Если аргумент не входит в нужный числовой диапазон, функция может вернуть неопределённые результаты. 

sys.exit — это быстрый способ выйти из программы при возникновении ошибки.

sys.stdin
~~~~~~~~~
Стандартный поток ввода, который используется для интерактивного ввода, включая вызовы input(). **Файло-подобный объект**, считывать данные можно с помощью его метода read.
Удобно, если неизвестно количество вводимых строк.
С помощью sys.stdin.readlines() можно считать строки в массив:

*import sys*

*st = sys.stdin.readlines()*

*print(st)*

*import sys*

Чтобы обозначить, что ввод закончен, нужно нажать Ctrl-D 

А с помощью такого кода просто считать строку 

*for ls in sys.stdin:*

    *st = ls.strip()*

sys.stdout
~~~~~~~~~~
Стандартный поток вывода, который используется для вывода функции print(), выражений и запросов input(). **Файло-подобный объект**, записывать данные в него можно с помощью его метода write.

Например, такой код выведет Hi, Hello, world(каждое слово в новой строке)

*import sys*

*file = sys.stdout*

*a= ['Hi', 'Hello', 'world']*

*for ip in a:*

    *file.write(ip + '\n')*

Поток вывода можно перенаправить, добавив строчку sys.stdout = open('newfile.txt', 'w'). Аналогично с потоками ввода. Лучше перенаправлять поток с помощью >, < для вывода ввода соответственно.

скрипт.py> newfile.txt

Функции для работы с ошибками и исключениями
---------------------------------------------
sys.stderr
~~~~~~~~~~~
Стандартный поток вывода ошибок, в который отправляются все ошибки интерпретатора. **Файло-подобный объект**, считывать данные можно с помощью его метода read.
