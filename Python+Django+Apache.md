# Различные скрипты Bash Python+Django+Apache

Установка Python 3 и пакетов для виртуального окружения:
```` bash
#!/bin/bash
# Установка Python 3 и пакетов для виртуального окружения

sudo apt-get update && sudo apt-get install -y \
python3 \
python3-dev \
python3-pip \
python3-venv

sudo -H pip3 install --upgrade pip
sudo -H pip3 install virtualenvwrapper
````

Узнать версию Django в консоли можно через следующую команду:
```` bash
python -m django --version
````
Добавление нового виртуального хоста Apache:
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
Удаление виртуального хоста Apache:
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