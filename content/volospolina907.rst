Основные команды для работы с файлами в Linux
====================================================

:date: 2020-10-07 09:00

:summary: Основные команды работы с файлами Linux.

:status: published

:author: Волос П.В.

**Группа** Б06-907

.. contents:: Оглавление

Команда pwd
""""""""""""""""""""""

Выводит имя текущего каталога. 
::

    $ pwd
    /home/guest

Команда cd
""""""""""""""""""""""

Это команда изменения каталога, она позволяет перемещаться между каталогами:


+--------------------+---------------------------------------+
| Команда            |Результат                              |
+====================+=======================================+
| cd <путь католога> |перейти в указанный каталог            |
+--------------------+---------------------------------------+
| cd /               |перейти корневой каталог               |
+--------------------+---------------------------------------+
| cd ..              |перейти на уровень выше                |
+--------------------+---------------------------------------+
| cd ../..           |перейти на два уровня выше             |
+--------------------+---------------------------------------+
| cd ~ или cd        |перейти в домашний каталог             |
+--------------------+---------------------------------------+
| cd –               |перейти в каталог до перехода в текущий|
+--------------------+---------------------------------------+

Команда ls
""""""""""""""""""""""

Команда ls позволяет вывести список файлов заданной папки. Без указания конкретного пути показывает текущий каталог.

+--------------------+------------------------------------------+
| Команда            |Результат                                 |
+====================+==========================================+
| ls                 |покажет файлы и каталоги в текущей папке  |
+--------------------+------------------------------------------+
| ls <путь католога> |покажет файлы и каталоги в указанной папке|
+--------------------+------------------------------------------+
| ls -l              |покажет содержимое с подробной информацией|
+--------------------+------------------------------------------+
| ls -a              |покажет содержимое включая скрытые файлы  |
+--------------------+------------------------------------------+

*Пример:*

Получение полного листинга текущего каталога, включая скрытые файлы.
::

    $ ls -la
    total 224
    drwx------ 16 guest guest 4096 Mar 21 18:16 .
    drwxr-xr-x  3 root root 4096 Mar 21 17:53 ..
    -rw-------  1 guest guest   21 Mar 21 17:54 .bash_history
    -rw-r--r--  1 guest guest   33 Dec 16 22:42 .bash_logout
    -rw-r--r--  1 guest guest  176 Dec 16 22:42 .bash_profile
    -rw-r--r--  1 guest guest  124 May 16 22:42 .bashrc
    drwxr-xr-x  2 guest test  4096 Feb 21 17:53 Desktop

Информация о файлах в длинном формате: тип файла (обычный файл -, каталог d), права доступа (чтение — r, запись — w, исполнение — x; первые 3 символа относятся к владельцу, следующие 3 — к членам группы, владеющей файлом, и последние 3 — ко всем остальным), кол-во ссылок на файл, владелец, группа, размер в байтах, дата модификации, имя файла.

Команда rm
""""""""""""""""""""""

Удалить файлы или каталоги. Если права доступа не позволяют этого сделать немедленно, то последние выводятся в восьмеричной форме и требуется подтверждение операции.

+--------------------+------------------------------------------------------+
| Команда            |Результат                                             |
+====================+======================================================+
| rm <file>          |удалить файл                                          |
+--------------------+------------------------------------------------------+
| rm -r <directory>  |выполнить удаление рекурсивно, включая каталоги       |
+--------------------+------------------------------------------------------+
| rm -f <file>       |не спрашивать подтверждений, удалить все, что возможно|
+--------------------+------------------------------------------------------+
| rm -i <file>       |запрашивать подтверждение на каждый удаляемый файл    |
+--------------------+------------------------------------------------------+
| rmdir <directory>  |удаление пустой папки                                 |
+--------------------+------------------------------------------------------+

Команда mv
""""""""""""""""""""""
::

    $ mv file_or_directory file_or_directory
    $ mv [-i] file_or_directory file_or_directory #запрашивать разрешение на перезапись уже существующих объектов

Переименовать файл или каталог, указанный в первом аргументе, в файл или каталог, указанный во втором.
::

    $ mv file <directory>


Перемещает файл в новое место.

Команда cp
""""""""""""""""""""""
::

    $ cp file_or_directory file_or_directory
    $ cp [-i] file_or_directory file_or_directory #запрашивать разрешение на перезапись уже существующих объектов
    $ cp -r directory directory #рекурсивное копирование каталога

Копирует файлы или каталог, указанный в первых параметрах, в файл или каталог, указанный в последнем.

Команда mkdir
""""""""""""""""""""""

Создает новый каталог:

+-----------------------+------------------------------------------+
| Команда               |Результат                                 |
+=======================+==========================================+
|mkdir newfolder        |создаст каталог с именем newfolder        |
+-----------------------+------------------------------------------+
|mkdir new new1	        |создаст два каталога с именами new и new1 |
+-----------------------+------------------------------------------+
|mkdir -p new/new1/new2 |создаст указанное дерево директорий       |
+-----------------------+------------------------------------------+

Команда ln
""""""""""""""""""""""
Позволяет создавать жесткие и символические ссылки на файлы или папки. Если второй операнд является уже существующим каталогом, то ссылки создаются внутри него. В случае, если второй аргумент отсутствует, ссылка создается в текущем каталоге с именем источника.
::

    $ ln файл_или_каталог ... [ссылка_или_каталог]
    $ ln -f файл_или_каталог ... [ссылка_или_каталог] #устанавливать ссылку вместо существующего файла
    $ ln -s файл_или_каталог ... [ссылка_или_каталог] #символьная ссылка

*Примеры:*

Сделать символьную ссылку b на a:
::

    $ln -s a b
    $ls -l
    итого 8
    -rw-rw-r-- 1 guest guest 0 Мар 21 18:57 a
    lrwxrwxrwx 1 guest guest 1 Мар 21 18:57 b -> a

Команда touch
""""""""""""""""""""""
Создает пустой файл. 
::

    $ touch file #создает пустой файл с именем file
    $ touch f1 f2 #создает несколько файлов
    $ touch  -t 201601081830.14 файл #позволяет установить дату создания в формате YYMMDDHHMM.SS

Команда cat
""""""""""""""""""""""
Читает данные из файла/файлов или стандартного ввода и выводит их на экран.
::

    $ cat file1 file2

Команда chmod
""""""""""""""""""""""
Позволяет изменить права доступа к файлам.
::

    $ chmod права /путь/к/файлу

Есть три основных вида прав:

#. **r** - чтение
#. **w** - запись
#. **x** - выполнение
#. **s** - выполнение  от имени суперпользователя (дополнительный)

Также есть три категории пользователей:

#. **u** - владелец файла
#. **g** - группа файла
#. **o** - все остальные пользователи

В качестве действий могут использоваться знаки "+" - включить или "-" - отключить.

*Пример:*

#. **u+x** - разрешить выполнение для владельца
#. **ugo+x** - разрешить выполнение для всех
#. **ug+w** - разрешить запись для владельца и группы
#. **o-x** - запретить выполнение для остальных пользователей
#. **ugo+rwx** - разрешить все для всех

Но права можно записывать не только таким способом. Есть еще восьмеричный формат записи, он более сложен для понимания, но пишется короче и проще:

* 0 - никаких прав;
* 1 - только выполнение;
* 2 - только запись;
* 3 - выполнение и запись;
* 4 -  только чтение;
* 5 - чтение и выполнение;
* 6 - чтение и запись;
* 7 - чтение запись и выполнение.

Во время установки прав сначала указываются цифры прав для владельца, затем для группы, а потом для остальных. Например:

* 744 - разрешить все для владельца, а остальным только чтение;
* 755 - все для владельца, остальным только чтение и выполнение;
* 764 - все для владельца, чтение и запись для группы, и только чтение для остальных;
* 777 - всем разрешено все.

Например:
::

    $ chmod u+x file
    $ chmod 766 file

