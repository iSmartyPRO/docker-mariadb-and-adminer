# Краткое описание
Сервер база данных MariaDB 10.6.7-focal.
Была выбрана именно эта база потому как она совместима с Zabbix, который я использую в своих ИТ инфраструктурах.

# Как установить
переименуйте .env.sample в .env и заполните своими данными

далее используйте следующую команду:
```
docker-compose up -d
```

# Примечание
Можно вручную удалить установку ADMINER отредактировав файл .env и docker-compose.yml

## Подключение другого Docker контейнера к сети MariaDB
```
docker network connect mariadb_default another-docker
```
после чего можно указывать имя mariadb в качестве хоста для подключения

# Полезные команды

### Подключение к базе данных
```
mysql -uroot -pPassword -h 192.168.0.100
```

### Создание базы данных

```
CREATE DATABASE mydatabase CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```
или
```
CREATE DATABASE mydatabase CHARACTER SET utf8 COLLATE utf8_bin;
```

### MySQL: Создание пользователя в базе данных
```
CREATE USER 'username'@'%' IDENTIFIED BY 'some_password';
```

### MySQL: настройка доступа к базе данных для пользователя
```
GRANT ALL PRIVILEGES ON mydatabase.* TO 'username'@'%';
```

### MySQL: перезагрузка настроенных разрешений
```
FLUSH PRIVILEGES;
```

в дополнении рекомендую использовать единую сеть для всех контейнеров, для этого отредактировав docker-compose.yml добавив следующие строки:
```
networks:
  default:
    external:
      name: "docker-lan"
```
