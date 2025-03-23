#### 23 февраля, 2025
# Домашняя работа №1

Виртуальная машина создана. Подключилась через PuTTY:
![image](https://github.com/user-attachments/assets/d8f0e0d7-36ec-45ba-ab5d-a8b8c3d49563)

Установка PostgreSQL 17

![image](https://github.com/user-attachments/assets/e1621088-d046-4862-b4af-f0e1e328d49e)

Инициализация базы, включение автоматического старта, старт. 
![image](https://github.com/user-attachments/assets/a790ec37-6e2b-4073-b066-fb9c5f2dd84d)

Запуск второй сессии. Запуск psql под пользователем postgres.
![image](https://github.com/user-attachments/assets/d5530600-e931-4ab4-aba8-b3679dfe9ea0)

Отключение autocommit

![image](https://github.com/user-attachments/assets/19f4d4e6-25d5-49e7-a3d2-7e76e4932bb3)


 
Создание таблицы persons и наполнение данными (первая сессия)
![image](https://github.com/user-attachments/assets/3aa3d880-d0bc-4f44-bc8e-783da3ba425a)


Проверка уровня изоляции - read committed (первая сессия)

 ![image](https://github.com/user-attachments/assets/c294d40a-f8f5-44cd-a040-9557b4432c54)

Первая сессия. Добавление строки "sergey sergeev" (без коммита) 
![image](https://github.com/user-attachments/assets/492bd20f-1a89-42eb-a0d2-3bd509ffc4e0)

Вторая сессия. Выборка всех строк из таблицы persons: результирующая выборка не содержит строки "sergey sergeev", поскольку транзакция, вставившая данную строку в таблицу, ещё не завершена, а текущий уровень изоляции ("read committed") не даёт читать изменения, сделанные незавершёнными транзакциями. 

![image](https://github.com/user-attachments/assets/3b99c3b3-4338-4e38-98ca-7c91e62de111)

Первая сессия. Выполнение commit;

![image](https://github.com/user-attachments/assets/f0adfcde-66fa-47c8-91c4-aa27f2f98efc)

Вторая сессия. Выборка всех строк из таблицы persons: видим новую строку "sergey sergeev", поскольку транзакция, вставившая её, завершена. 

![image](https://github.com/user-attachments/assets/41639ac1-86aa-4567-8b93-b5699d1cfa8c)


Установка уровня изоляции на repeatable read в обеих сессиях:

![image](https://github.com/user-attachments/assets/e4a7bc79-06c0-42b7-91be-f053509a9e7e)

Первая сессия. Вставляем строку "sveta svetova" (без коммита)  

![image](https://github.com/user-attachments/assets/507f97c0-610b-40d2-aaf1-6f86dfcdabe2)

Вторая сессия. Читаем таблицу persons: всего 3 строки, без "sveta svetova", поскольку при уровне repeatable read аномалия  грязного чтения также не допустима. 

![image](https://github.com/user-attachments/assets/ee796047-90b7-48bb-9928-fc4916f4a87c)

Первая сессия. Завершение транзакции

![image](https://github.com/user-attachments/assets/6fa5c4d2-cd7e-4b89-b15e-bcd2640245e7)

Вторая сессия. Читаем таблицу persons: всего 3 строки, без с "sveta svetova". Зафиксированная строка в результрующей выборке отсутствует, так как аномалия неповторяющегося чтения недопустима  для уровня repeatable read (т.е. в контексте одной транзакции результат повторного чтения должен быть одинаковым). 

![image](https://github.com/user-attachments/assets/a4d4e83b-26cd-4871-8392-08b212f74759)

Вторая сессия. Завершение транзакции. Далее повторно читаем таблицу persons: всего 4 строки, включая  "sveta svetova". Строка появилась, так как данная транзакция была начата, когда строка  "sveta svetova" уже была зафиксирована первой сессией.

![image](https://github.com/user-attachments/assets/35e5d443-041e-47d4-bd89-ef3959cacc1a)

