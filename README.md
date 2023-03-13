# 9.2 «Zabbix. Часть 1»

# Александр Широбоков

## Задание 1. Установите Zabbix Server с веб-интерфейсом.
### Скриншот админки и запущенного сервера с дашбордом:
![Снимок экрана (37)](https://user-images.githubusercontent.com/69298696/224605574-ada6cca8-b945-4c9d-911e-bc5355741c90.png)
![Снимок экрана (38)](https://user-images.githubusercontent.com/69298696/224605708-0e34a1d8-01e2-4d68-875f-d45bbc2ad6a6.png)
### Список использованных команд:
- Установка Zabbix:
1.  wget https://repo.zabbix.com/zabbix/6.4/debian/pool/main/z/zabbix-release/zabbix-release_6.4-1+debian11_all.deb
2.  dpkg -i zabbix-release_6.4-1+debian11_all.deb
3.  apt update
- Установка PSQL:
4.  sudo apt install postgresql
- Запуск Zabbix Server:
5.  sudo apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts nano -y
- Создание пользователя с помощью psql из под root
6.  su - postgres -c 'psql --command "CREATE USER zabbix WITH PASSWORD '\'123456789\'';"'
7.  su - postgres -c 'psql --command "CREATE DATABASE zabbix OWNER zabbix;"'
- Импорт схемы
8.  zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
- Настройка пароль DBPassword в файле /etc/zabbix/zabbix_server.conf
9.  sudo nano /etc/zabbix/zabbix_server.conf
- Запуск Zabbix Server, Zabbix Agent и web-сервер
10. sudo systemctl restart zabbix-server apache2 # zabbix-agent
11. sudo systemctl enable zabbix-server apache2 # zabbix-agent

## Задание 2. Установите Zabbix Agent на два хоста.
### Скриншот подключенных агентов:
![Снимок экрана (40)](https://user-images.githubusercontent.com/69298696/224608303-a7586b32-4b4d-43c7-9d26-d4dc8724ebd6.png)
### Скриншот лога zabbix agent:
![Снимок экрана (41)](https://user-images.githubusercontent.com/69298696/224608760-da5fde68-faa8-43d3-a97d-5222fda91b90.png)
### Cкриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные(test-machine и zabbix-server):
![Снимок экрана (42)](https://user-images.githubusercontent.com/69298696/224609180-f30429e9-d21f-4148-a4e3-1de61bceb0f5.png)
![Снимок экрана (43)](https://user-images.githubusercontent.com/69298696/224609203-734bce2c-5875-41a5-9fb3-ab520d24b14e.png)

### Список использованных команд:
- Установите Zabbix Server и компоненты
1.  sudo apt install zabbix-agent -y
- Запустите Zabbix Agent
2.  sudo systemctl restart zabbix-agent
3.  sudo systemctl enable zabbix-agent
- Меняю адрес сервера на адрес сервера Zabbix:
4.  sudo nano /etc/zabbix/zabbix_agentd.conf
- Перезапускаю агент:
5.  sudo systemctl restart zabbix-agent
## Задание 3* Установите Zabbix Agent на Windows (компьютер) и подключите его к серверу Zabbix.
### Приложите скриншот раздела Latest Data, где видно свободное место на диске C:
### Zabbix агент запущенный в windows: 
![Снимок экрана (44)](https://user-images.githubusercontent.com/69298696/224624715-f2d89b77-60be-4d85-8912-eeb5420de3a5.png)
### Агент подключенный на сервере:
![Снимок экрана (47)](https://user-images.githubusercontent.com/69298696/224624970-71b81faf-4ef5-40cd-b416-88e203651d85.png)
### Общее и свободное место на диске С:
![Снимок экрана (45)](https://user-images.githubusercontent.com/69298696/224625303-662279b3-c308-4ae2-b031-57a86e318604.png)
