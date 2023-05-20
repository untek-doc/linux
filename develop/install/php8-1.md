# PHP 8.1

## Добавить PPA ondrej/php

После добавления этого репозитория первоначальную установку и обновления можно выполнить стандартными apt командами.

**Ubuntu**

    sudo add-apt-repository ppa:ondrej/php # Press enter when prompted.
    sudo apt update

**Debian**

    sudo apt install apt-transport-https lsb-release ca-certificates wget -y
    sudo wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
    sudo sh -c 'echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
    sudo apt update

## Установите PHP 8.1 и расширения

Все пакеты PHP 8.1 следуют шаблону php8.1-NAME. Дополнительные расширения (такие как GD, Curl и т. д.) могут быть установлены так же, в виде наименование программных пакетов  (php8.1-gd, php8.1-curl и т. д.).

 * php8.1 - это мета-пакет , который коллективно устанавливает несколько зависимостей, таких, как php8.1-cli и php8.1-readline, а также некоторые вспомогательные пакеты.
 * php8.1-common - это также мета-пакет, который устанавливает большинство широко используемых расширений PHP за один раз. Он автоматически устанавливает пакет, например php8.1-pdo, php8.1-tokenizer и другие полезные расширения.

    sudo apt install php8.1 php8.1-common php8.1-cli -y

Эта команда установит несколько расширений PHP - php8.1-common и CLI для PHP 8.1.  После установки, можно проверить наличие установленных модулей, запустив:

    php -v # Показать версию PHP .
    php -m # Показать установленные и загруженные модули PHP.

Вы можете установить дополнительные расширения по тому же шаблону php8.1-NAME. Обратитесь к файлу packages.txt, чтобы увидеть список существующих пакетов, если вы обновляете существующую систему. Обратите внимание, что начиная с PHP 8.0, расширение JSON входит в комплект и устанавливается неявно.

Пример установки еще нескольких полезных расширений:

    sudo apt install php8.1-{bz2,curl,intl,xml,mbstring,zip,bcmath}

Для сред разработки также могут быть установлены инструменты покрытия кода или отладчик Xdebug. 

    sudo apt install php8.1-pcov # PCOV code coverage tool
    sudo apt install php8.1-xdebug # Xdebug debugger

В зависимости от используемого веб-сервера вам потребуется установить дополнительные пакеты для интеграции с веб-сервером. 

Для использования Nginx, Litespeed и т.п. устанавливаем php8.1-fpm. Пакет обеспечивает интеграцию с PHP 8.1 через FPM:

    sudo apt install php8.1-fpm

Для использования Apache mod_php установите libapache2-mod-php8.1:

    sudo apt install libapache2-mod-php8.1

Обратите внимание, что обработчик Apache2 переименован из php7_module в php_module для PHP 8.0.  Пакет автоматически настраивает расположение модуля Apache, но если вы обновляете с существующей установки PHP, возможно , потребуется обновление конфигурационных файлов; в частности блоки <IfModule>. 

## Протестируйте установку PHP 8.1

Чтобы убедиться, что все установлено, можно так же проверить установку PHP и расширений, выполните следующие команды:


    php -v
    php -m

## Запуск PHP 8.1 с другими версиями

    sudo update-alternatives --config php

## Ссылки

* [Как установить PHP 8.2 на Debian/Ubuntu](https://www.dev-notes.ru/articles/php/install-php82-ubuntu-debian/?ysclid=lhak8kikiy749890379)
* [Как установить/обновить PHP 8.1 в Ubuntu/Debian](https://sergeymukhin.com/blog/kak-ustanovitobnovit-php-81-v-ubuntudebian?ysclid=lh76zzcv7q800894993)
