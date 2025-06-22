#### 22 июня, 2025
# Домашняя работа №4. "Логический уровень PostgreSQL"

Кластер PostgreSQL 14:
![image](https://github.com/user-attachments/assets/a75c26f7-dfde-417d-a49c-3aec76e1a4f1)

Создание БД, схемы, таблицы. Вставка строки

![image](https://github.com/user-attachments/assets/6c4850a1-084d-4a66-8e40-0aff90ba164b)

![image](https://github.com/user-attachments/assets/c922af9c-2f2b-48f1-9a2b-b1a7dac747b7)

Создание роли readonly и выдача ей прав

![image](https://github.com/user-attachments/assets/f6776d5a-4c73-483d-8a05-86f74da433cd)

Проверка выданных прав для readonly

![image](https://github.com/user-attachments/assets/89ec5ce1-41b0-4946-9865-16d2a15a7641)

Работа с пользователем testread (создание, присвоение роли, подключение к БД, чтение данных):

![image](https://github.com/user-attachments/assets/2820eaaf-2a31-402a-ba62-2b4a740e3607)

Данные считываются, всё корректно. Если при создании таблицы не указать схему, пользователь testread не сможет на данном этапе считать данные, так как у роли readonly есть права на чтение таблиц только из схемы testnm.

Таблицы в схеме:

![image](https://github.com/user-attachments/assets/130d8c05-ced0-48db-8f6f-f723745736f0)


Пересоздание таблицы 

![image](https://github.com/user-attachments/assets/86339f62-0348-4542-af48-e4f43a01db35)

Попытка чтения новой таблицы пользователем testread - неудачно
![image](https://github.com/user-attachments/assets/91da43a8-1820-470c-9470-6a72d9e01a54)

Данные невозможно прочитать, поскольку это новый объект (хоть он и называется  как удалённый объект t1). А во время выдачи прав чтения на все таблицы схемы testnm этот объект ещё не существовал.

Выдаём права default priveledges роли readonly, снова пытаемся прочитать данные
![image](https://github.com/user-attachments/assets/84877781-0f80-4ae1-9211-b406a9002717)

Не получилось, так как alter default priviledges действует только на таблицы, созданные после выполнения данной команды.
Сделаем повторно grant select и прочитаем данные:

![image](https://github.com/user-attachments/assets/f13851d9-09cc-4bf7-8e54-b980c9ee11b6)

Получилось!

Создаём вторую таблицу

![image](https://github.com/user-attachments/assets/5780152b-42f3-4a1b-88de-59c350bedb11)

Таблица создалась в схеме public, так как по умолчанию пользователь имеет на это право, если имеется разрешение на подключение к БД

![image](https://github.com/user-attachments/assets/2cb93c8e-5a71-41b9-95c2-38bf410395b1)

Отбираем права для схемы public, и далее снова попытка создания таблицы под пользователем testread
![image](https://github.com/user-attachments/assets/65d2c57e-5867-48d7-9de5-a0aa4014696c)

![image](https://github.com/user-attachments/assets/14789f54-f2b3-4e2b-b709-f3742584a567)

В создании таблицы в схеме public отказано - так и должно быть.
