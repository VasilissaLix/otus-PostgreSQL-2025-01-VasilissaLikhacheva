#### 25 апреля, 2025
# Домашняя работа №2

Виртуальная машина создана, Centos 7. Подключилась через PuTTY:
![image](https://github.com/user-attachments/assets/d8f0e0d7-36ec-45ba-ab5d-a8b8c3d49563)

Установка docker
![image](https://github.com/user-attachments/assets/ad7856a2-8f6e-452f-976d-d230227e94d6)

![image](https://github.com/user-attachments/assets/5756d9d9-c8d1-46c1-90e0-045037843236)

![image](https://github.com/user-attachments/assets/545ecc5c-5bad-4a17-92a0-fc7756705ade)
![image](https://github.com/user-attachments/assets/9bcac5e5-74e8-467d-99f1-ba2abea52eeb)
![image](https://github.com/user-attachments/assets/79c21594-502b-4251-9e38-cd6395ea4146)


Подготовка папки /var/lib/postgres

![image](https://github.com/user-attachments/assets/1e3ebd69-89ce-420e-979f-63ddee201077)

Создание образа из Dockerfile (файлики скачала c docker hub: https://hub.docker.com/_/postgres)
![image](https://github.com/user-attachments/assets/af6208ed-d83c-4e0c-be30-6d4b94cc58ed)

Проверяем в спике образов:

![image](https://github.com/user-attachments/assets/26687e75-b78f-4786-a542-8fede761943c)

Запуск контейнера и монтирование папки
![image](https://github.com/user-attachments/assets/4b8b739b-8ff1-42d8-bdc8-69ad68c3b785)

Подключаюсь через docker exec psql и создаю таблицу
![image](https://github.com/user-attachments/assets/16ca9acb-6df4-454a-8efe-687b734ed21b)

Создаю второй контейнер-клиент
![image](https://github.com/user-attachments/assets/3aee4d2c-47aa-4226-ab87-4bb93f555827)

Создание сети и подключение к ней контейнеров (без создания новой сети не получилось подключиться)
![image](https://github.com/user-attachments/assets/e961c5da-845a-4673-b843-2bb46bb14628)

Подключение контейнера-клиента к контейнеру-серверу 
![image](https://github.com/user-attachments/assets/4ba84547-d3f2-4899-acb6-4d7148ef9aec)

Подключение с рабочего ноутбука через DBeaver
![image](https://github.com/user-attachments/assets/7538db70-0ac2-4f5b-83ad-1ab057db9e25)
![image](https://github.com/user-attachments/assets/e5deec08-1628-4e49-82fd-575f2c4fb375)

Удаляю контейнер. Проверяю наличие данных в папке
![image](https://github.com/user-attachments/assets/e4d97722-3fd3-49ad-b725-4b1fcf8035e6)

Создаю контейнер-сервер заново. Добавляю в сеть.
![image](https://github.com/user-attachments/assets/1828c694-a0ce-47d4-81e9-c6ce8eb5944b)

Подключаюсь, проверяю наличие данных. 

![image](https://github.com/user-attachments/assets/66efcdde-9eab-4984-bd3c-d2640331c445)
Итог: данные остались.
