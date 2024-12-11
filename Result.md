# Итоговый отчет по анализу логов с использованием команды `grep`

## Результаты анализа

### 1. Запросы на скачивание файлов
Используя команду `grep "GET /downloads/" access.log`, были найдены следующие запросы:
```
192.168.0.10 - - [11/Dec/2024:10:01:02 +0000] "GET /downloads/report1.pdf HTTP/1.1" 200 1048576
192.168.0.15 - - [11/Dec/2024:10:02:15 +0000] "GET /downloads/report2.pdf HTTP/1.1" 404 0
192.168.0.20 - - [11/Dec/2024:10:03:22 +0000] "GET /downloads/secret_data.txt HTTP/1.1" 200 51200
192.168.0.10 - - [11/Dec/2024:10:05:10 +0000] "GET /downloads/budget.xlsx HTTP/1.1" 200 204800
```
![image](https://github.com/user-attachments/assets/8ad6c4f0-e566-4422-ba4e-600a78062dad)


### 2. Подозрительные IP-адреса
С помощью команды `grep -oP '\\d+\\.\\d+\\.\\d+\\.\\d+' access.log | sort | uniq`, были идентифицированы IP-адреса:
```
192.168.0.10
192.168.0.15
192.168.0.20
192.168.0.30
```
![image](https://github.com/user-attachments/assets/f7d97827-899b-410b-bd0b-997519cc58de)

### 3. Ошибки доступа
Команда `grep -E "404|500" access.log` выявила следующие ошибки:
```
192.168.0.15 - - [11/Dec/2024:10:02:15 +0000] "GET /downloads/report2.pdf HTTP/1.1" 404 0
```
![image](https://github.com/user-attachments/assets/52a4e766-eb21-4dde-bc49-5d23e19b7269)


### 4. Скачанные файлы
Сравнив список запрошенных файлов с файлами в папке `confidential_docs/`, мы определили следующие совпадения:
```
report1.pdf
budget.xlsx
secret_data.txt
```
Для сравнения использовались команды:
```bash
grep -oP '(?<=GET /downloads/)[^ ]+' access.log | sort | uniq > downloaded_files.txt
ls confidential_docs/ | sort > available_files.txt
comm -12 downloaded_files.txt available_files.txt
```
![image](https://github.com/user-attachments/assets/2161d407-1679-4dc5-928e-417c4b29a415)


### 5. Проверка учетных записей
Запросы на логины пользователей (`POST /login`) не содержали упоминаний пользователей из файла `users.txt`. Таким образом, учетные записи сотрудников не использовались явно в логах.
![image](https://github.com/user-attachments/assets/4dabfcf6-8e4c-4b68-84b1-8b18494c8092)

### 6. Дополнительное задание
Команда для поиска строк со скачиванием данных в логах за исключением скачиваний с успешным доступом (код 200).
``` bash
grep "GET /downloads/" access.log | grep -v " 200 "
```

## Итоговый вывод
1. **Подозрительные IP-адреса:**
   - 192.168.0.10
   - 192.168.0.15
   - 192.168.0.20

2. **Скачанные файлы:**
   - report1.pdf
   - budget.xlsx
   - secret_data.txt

3. **Ошибочные запросы:**
   - Файл `report2.pdf` отсутствует, так как запрос вернул ошибку 404.
