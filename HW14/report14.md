#### 22 июня, 2025
# Домашняя работа №14

Для выполнения дз была использована БД demo.
Диаграмма таблиц
![image](https://github.com/user-attachments/assets/55bcb238-deb6-4ebc-9542-fa9b4a3be064)

[Описание схемы на сайте](https://postgrespro.ru/docs/postgrespro/9.6/apjs03)

##### 1. Реализовать прямое соединение двух или более таблиц
В данном случае соединяем таблицы бронирования и билетов.
![image](https://github.com/user-attachments/assets/98a2dcd6-b317-4012-bebe-015fe2893e8b)

План выполнения запроса

![image](https://github.com/user-attachments/assets/e6c84a86-928d-4f0e-8bf0-09b20dd325a9)

Предполагаю, что выбран алгоритм Merge Join, поскольку присутствует сортировка по book_ref, плюс в dbeaver по умолчанию выдаются только первые 200 строк.

##### 2. Реализовать левостороннее (или правостороннее) соединение двух или более таблиц

Выполним left join. Таким образом, можно увидеть, для каких билетов выбраны места, а для каких нет (стоит NULL в boarding_no, seat_no)

![image](https://github.com/user-attachments/assets/b8f9594e-a348-4146-9ebf-5f8cab7b115e)

План выполнения без сортировки

![image](https://github.com/user-attachments/assets/f04f1d66-f587-4968-8219-b976f3657714)

Выбран алгоритм Hash Left Join, поскольку сортировка отсутствует, и обе таблицы имеют достаточно много записей - несколько сотен тысяч строк. 

##### 3. Реализовать кросс соединение двух или более таблиц

Для cross-join проверим все возможные сочетания аэропортов и самолётов
![image](https://github.com/user-attachments/assets/84ef188c-2fce-4a73-bd9b-470733551f44)

Поскольку кросс джоин - это декартово произведение, берётся алгоритм Nested Loop.
![image](https://github.com/user-attachments/assets/14b1aa65-b70c-4670-82de-de5484dc4793)

##### 4. Реализовать полное соединение двух или более таблиц
Найдём через full join рейсы, на которые отсутствуют записи о билетах
![image](https://github.com/user-attachments/assets/79f88aa8-2e54-4701-83a1-327aae160bc9)

План запроса покажет нам Hash Full Join, который дополнительно использует фильтр для исключения записей рейсов, у которых забронированы билеты.
![image](https://github.com/user-attachments/assets/8308a882-5523-4d2c-b8af-1a4f5df32fa1)

##### 5. Реализовать запрос, в котором будут использованы разные типы соединений
Используем обычный inner join для соединения таблиц рейсов, самолётов и мест. Далее присоединяем через left join таблицу по посадочным талонам с условием, что посадочного талона на место нет (NULL). Таким образом, можно узнать, какие места свободны (последняя колонка seat_no)
![image](https://github.com/user-attachments/assets/9896627c-6090-4d83-9fd2-608181dd42b1)

Если фильтровать по рейсу, выбирается алгоритм Nested Loop
![image](https://github.com/user-attachments/assets/ce1b7ffc-9369-4d19-81db-305f1d01dd7a)

Если убрать фильтр (т.е. найдём все незанятые места по всем рейсам), для джойна boarding_passes и flights используется Hash Join
![image](https://github.com/user-attachments/assets/b29b05a6-fed1-438c-85c8-7267a9599408)



