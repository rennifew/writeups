
---
## Scenario

> John Doe was accused of doing illegal activities. A disk image of his laptop was taken. Your task as a soc analyst is to analyze the image and understand what happened under the hood.
---
## Q1. What is the MD5 hash value of the suspect disk?
Среди скачанных файлов находится `.txt` файл, который в конце содержит MD5 хэш-сумму подозрительного диска.
> Answer: 9471e69c95d8909ae60ddff30d50ffa1

## Q2. What phrase did the suspect search for on 2021-04-29 18:17:38 UTC? (three words, two spaces in between)
Необходимо экспортировать файл `History`, который хранит историю браузера пользователя.
Данный файл находится по пути: `C:\Users\John Doe\AppData\Local\Google\Chrome\User Data\Default\History`. 
Далее, открыв его в DB Browser и перейдя в таблицу


Число 13264218406522742, которое вы видите в файле History Chrome, представляет собой количество микросекунд, прошедших с 1 января 1601 года. Это формат времени, используемый Chrome для хранения истории посещений.

Чтобы преобразовать это число в читаемый формат, можно использовать SQL запрос:
```sql
SELECT datetime(last_visit_time / 1000000 + (strftime('%s', '1601-01-01')), 'unixepoch', 'localtime')
```
где `last_visit_time` это ваше число

Альтернативно, можно использовать онлайн-конвертеры, указав, что это WebKit time (микросекунды с 1601-01-01)

В C# можно преобразовать это значение, вычтя 11644473600000 (количество миллисекунд между 1601-01-01 и 1970-01-01) и рассматривая результат как обычную временную метку Unix в миллисекундах