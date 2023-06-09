# Bash Ubuntu
#### Набор полезных скриптов для Ubuntu:

* [Apache](https://github.com/den0011/bash_ubuntu/blob/main/Apache.md)
* [Python+Django+Apache](https://github.com/den0011/bash_ubuntu/blob/main/Python%2BDjango%2BApache.md)
* [System](https://github.com/den0011/bash_ubuntu/blob/main/System.md)

## Для запуска Bash-скриптов на Ubuntu нужно выполнить следующие действия:

1. Создать файл скрипта с расширением .sh. Для примера, создадим файл с именем **script.sh**:

```` bash
#!/bin/bash
echo "Hello, World!"
````
2. Сделать файл скрипта исполняемым с помощью команды **chmod**:

```` bash
chmod +x script.sh
````

3. Запустить скрипт, указав его полный путь и имя:

```` bash
./script.sh
````
Если скрипт не находится в текущей директории, нужно указать полный путь до файла.

Также можно запустить скрипт, указав команду **bash** и полный путь до файла:

```` bash
bash /path/script.sh
````
или
```` bash
sh /path/script.sh
````