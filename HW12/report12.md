#### 22 июня, 2025
# Домашняя работа №12

ВМ создана. PostgreSQL установлен:
![image](https://github.com/user-attachments/assets/0598b6df-517d-4572-b69a-c14c6ca023d7)

БД называется demo, схема bookings.
Бекап будет снят с таблицы rand, в которой сгенерировано 100 строк
![image](https://github.com/user-attachments/assets/01a71524-250b-46ab-956a-1ddeca997e56)

Создаю папку demo_db_backups под postgres

![image](https://github.com/user-attachments/assets/0c242f5b-579a-4f2b-b528-01ce9d49f2bd)

Делаю копию через запрос, используя COPY

![image](https://github.com/user-attachments/assets/1ec06d1b-c675-40d4-acf3-9bb779d37592)
![image](https://github.com/user-attachments/assets/55f7c985-0c1f-4740-b826-c08e4a822e47)

Создаём вторую схему, где будем восстанавливать ранее снятый бекап

![image](https://github.com/user-attachments/assets/8cf0ab34-2ab6-4798-8cf2-62870a6dddfe)

Восстанавливаю также через copy

![image](https://github.com/user-attachments/assets/453f6621-7503-4582-b5af-c2b897ab87cd)
![image](https://github.com/user-attachments/assets/c8796d25-3c86-4e39-99f8-25739e06123a)

Меняю наименование этой таблицы, чтобы их различить при снятии бекапа через pg_dump

![image](https://github.com/user-attachments/assets/6e762478-0041-4180-98dd-3ce326374ae6)

Снимаем копию таблиц rand и rand_bcp через pg_dump
![image](https://github.com/user-attachments/assets/d9556a3b-01ab-4e66-97d5-6861d674b362)

Восстанавление rand_bcp
1) Создаю БД и схему
  ![image](https://github.com/user-attachments/assets/fa6edd33-06f5-4fb5-bd16-a49709b7f45f)
2) Восстанавливаю через pg_restore
![image](https://github.com/user-attachments/assets/f388f498-3f18-4cc2-8868-6571cf0dd5a3)
![image](https://github.com/user-attachments/assets/a4f6b350-4096-4441-a1aa-a55f949abd7b)
