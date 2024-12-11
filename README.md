# Лабораторная работа «команда grep»
## Разминка
Давайте узнаем, что такое команда «grep», и для чего она нужна.
- Grep – команда Linux/UNIX, с помощью которой выполняется поиск строк и сопоставление текстовых файлов с регулярными выражениями. Данная команда предустановлена в ОС Linux. Так что скачивать Вам ничего не придется.
Как выглядит команда:
```bash
$ grep [опции] шаблон [путь к файлу или папке]
```

1. Скачайте текстовый файл Welcome.txt. После чего выполните команду:
```bash
$ grep "Linux" Welcome.txt
```
В результате Вы должны получить следующий вывод:
![image](https://github.com/user-attachments/assets/e7e10676-a35f-44cf-98e0-a31555cbc3ed)
2. Скопируйте данный файл, создайте папку "test" и вставьте туда файл.
После этого вернитесь в директорию к исходному файлу и выполните команду:
```bash
$ grep -r "Linux" *
```
В результате Вы должны получить:
![image](https://github.com/user-attachments/assets/b3349b1a-6f5d-4d95-ba85-d81a0b0eeee5)

Такой вывод связан с тем, что параметр "-r" позволяет искать строку в текущем каталоге и его подкаталогах.

Таким образом, Вы увидели, что разные флаги позволяют производить более расширенный поиск. А теперь перейдем к основному заданию.

## Основное задание
Вы – сотрудник отдела информационной безопасности крупной компании. Вам поручили расследовать подозрительную активность на сервере. Кто-то скачал конфиденциальные файлы, и ваша задача — найти, какие именно данные были скачаны, и откуда произошел доступ. Для этого вам предстоит использовать команду grep для анализа логов и данных.
### Цель работы:
- Изучить команду grep и её параметры.
- Научиться эффективно фильтровать и анализировать текстовые данные.
- Применить полученные навыки в реальной ситуации.
### Задачи:
- Выяснить, какой IP-адрес совершал подозрительные действия.
- Найти, какие файлы были скачаны с сервера.
- Определить, какие учётные записи могли быть скомпрометированы.
### Исходные данные:
- Логи доступа хранятся в файле access.log.
- Список сотрудников и их учётных записей – в файле users.txt.
- Файлы документов – в папке confidential_docs/.

## Часть 1: Анализ логов
Задания:
1. Найдите все строки в файле access.log, содержащие запросы на скачивание файлов (строки с GET /downloads/).
2. Определите, какие IP-адреса совершали запросы на скачивание. Используйте регулярные выражения.
3. Найдите строки, содержащие ошибки (с кодом 404 или 500).

## Часть 2: Сравнение данных
Задания:
1. Проверьте, совпадают ли имена скачанных файлов с файлами в папке confidential_docs/. Используйте команды grep, ls, и diff.
2. Выясните, какие учётные записи могли быть использованы.
Для этого:
- Найдите упоминания логинов пользователей в логах.
- Сравните их с данными в users.txt.

## Часть 3: Дополнительное задание
Напишите команду, которая одновременно находит строки с запросами и исключает строки с кодом 200 (успешный доступ):

## По итогам работы оформите отчет в файле Result.md

## Дополнительные источники
1. [Документация по grep на Linux.org](https://www.linux.org/docs/man1/grep.html)
2. [Справочник GNU grep](https://www.gnu.org/software/grep/manual/grep.html)
3. [Поиск строк и шаблонов с помощью grep](https://selectel.ru/blog/tutorials/grep-command-in-linux/)
