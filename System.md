# Набор различных скриптов Bash 

Скрипт для автоматического обновления системы:
```` bash
#!/bin/bash
sudo apt-get update
sudo apt-get upgrade -y
sudo apt-get dist-upgrade -y
sudo apt-get autoremove -y
sudo apt-get autoclean -y
````
Скрипт для проверки доступности сайта:
```` bash
#!/bin/bash
wget --spider --quiet http://example.com
if [ $? -eq 0 ]; then
    echo "Site is up."
else
    echo "Site is down."
fi
````
Удаление пакета и его зависимостей:
```` bash
#!/bin/bash
sudo apt-get remove --auto-remove $1
````
Удаление пакетов, неиспользуемых в системе:
```` bash
#!/bin/bash
sudo apt-get autoremove
````
Скрипт для установки Docker:
```` bash
#!/bin/bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker $USER
````
Для резервного копирования баз данных **PostgreSQL** на **Ubuntu**, 
который будет создавать файлы резервных копий в указанном каталоге.
В этом скрипте мы задаем параметры подключения к **PostgreSQL** 
(хост, порт, имя пользователя и пароль), список баз данных, 
которые нужно скопировать, и каталог для сохранения резервных копий.
Затем мы создаем отдельную директорию для каждой базы данных, 
создаем резервную копию базы данных с помощью команды **pg_dump** и 
сжимаем ее с помощью **gzip**.
```` bash
#!/bin/bash

# Указываем параметры подключения к PostgreSQL
HOST=localhost
PORT=5432
USERNAME=postgres
PASSWORD=password

# Указываем список баз данных, которые нужно скопировать
DATABASES=(db1 db2 db3)

# Указываем каталог для сохранения резервных копий
BACKUP_DIR=/backup/postgres

# Создаем каталог, если он не существует
mkdir -p $BACKUP_DIR

# Определяем текущую дату и время
NOW=$(date +"%Y-%m-%d-%H-%M-%S")

# Создаем отдельную директорию для каждой базы данных
for DB in ${DATABASES[@]}; do
  DB_BACKUP_DIR=$BACKUP_DIR/$DB
  mkdir -p $DB_BACKUP_DIR

  # Создаем резервную копию базы данных
  pg_dump -h $HOST -p $PORT -U $USERNAME -W $PASSWORD $DB > $DB_BACKUP_DIR/$NOW.sql

  # Сжимаем резервную копию с помощью gzip
  gzip -f $DB_BACKUP_DIR/$NOW.sql
done
````