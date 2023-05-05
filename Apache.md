# Apache
Для управления сервером **Apache** в **Ubuntu** можно использовать встроенные утилиты и команды **bash**. 
Например, можно использовать команду **service** для запуска, остановки и перезапуска службы **Apache**.

#### Примеры команд:

Запустить **Apache**: 
```` bash
sudo service apache2 start
````
Остановить **Apache**: 
```` bash
sudo service apache2 stop
````
Перезапустить **Apache**: 
```` bash
sudo service apache2 restart
````
Проверить статус **Apache**: 
```` bash
sudo service apache2 status
````

Кроме того, можно создать ***bash-скрипт*** для управления Apache. 
Например, можно создать файл с расширением **.sh** (например, ***apache.sh***) 
и добавить в него команды для управления **Apache**.

```` bash
#!/bin/bash

case $1 in
  start)
    sudo service apache2 start
    ;;
  stop)
    sudo service apache2 stop
    ;;
  restart)
    sudo service apache2 restart
    ;;
  status)
    sudo service apache2 status
    ;;
  *)
    echo "Usage: $0 {start|stop|restart|status}"
    exit 1
    ;;
esac

exit 0
````
Затем, после того как файл был сохранен и установлен как исполняемый, (***chmod +x apache.sh***) можно вызвать его с
нужным аргументом для выполнения соответствующей команды. Например:

***Запустить Apache***
```` bash
./apache.sh start  
````
***Остановить Apache***
```` bash
./apache.sh stop
````
***Перезапустить Apache***
```` bash
./apache.sh restart  
````
***Проверить статус Apache***
```` bash
./apache.sh status
````

### Расмотрим еще несколько полезных наборов команд

Показать ошибки конфигурации:
```` bash
sudo apache2ctl configtest
````
Показать версию Apache:
```` bash
apache2 -v
````
Показать модули Apache:
```` bash
apache2ctl -M
````
Показать виртуальные хосты Apache:
```` bash
apache2ctl -S
````
Добавление нового виртуального хоста:
```` bash
#!/bin/bash
# Задаем имя домена
DOMAIN_NAME="example.com"
# Создаем директорию для хранения файлов сайта
sudo mkdir -p /var/www/$DOMAIN_NAME
# Создаем файл конфигурации для нового виртуального хоста
sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/$DOMAIN_NAME.conf
# Открываем файл конфигурации для редактирования
sudo nano /etc/apache2/sites-available/$DOMAIN_NAME.conf
# Вносим нужные изменения в файл конфигурации
sudo a2ensite $DOMAIN_NAME.conf
# Перезагружаем Apache для применения изменений
sudo systemctl reload apache2
````
Удаление виртуального хоста:
```` bash
#!/bin/bash
# Задаем имя домена
DOMAIN_NAME="example.com"
# Отключаем виртуальный хост
sudo a2dissite $DOMAIN_NAME.conf
# Удаляем файл конфигурации
sudo rm /etc/apache2/sites-available/$DOMAIN_NAME.conf
# Удаляем директорию с файлами сайта
sudo rm -rf /var/www/$DOMAIN_NAME
# Перезагружаем Apache для применения изменений
sudo systemctl reload apache2
````
