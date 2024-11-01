# Как установить/обновить PHP 8.3 в Ubuntu или Debian

[PHP 8.3](https://sergeymukhin.com/blog/chto-novogo-v-php-83) - это главное обновление PHP 2023 года. Он содержит новые интересные функции, такие как типизированные константы в классах, новый тип исключений в DateTime, новая функция json_validate, а также несколько других изменений. Как обычно, в новом релизе PHP содержит несколько исправлений ошибок и улучшений, а также повышение производительности.

В этой статье объясняется, как установить PHP 8.3 в современных системах Linux - Debian и Ubuntu. Аналогичным способом также можно установить некоторые из наиболее популярных расширений PECL.
## Быстрый старт для администраторов

Если вы опытный разработчик/девопс и вам достаточно вспомнить последовательность команд для установки.
## Debian (10, 11, 12)
```bash
# Можете сохранить существующий список пакетов PHP в файл packages.txt.
sudo dpkg -l | grep php | tee packages.txt

# Добавьте источник репозитория Ondrej и ключ подписи вместе с зависимостями.
sudo apt install apt-transport-https

sudo curl -sSLo /usr/share/keyrings/deb.sury.org-php.gpg https://packages.sury.org/php/apt.gpg
sudo sh -c 'echo "deb [signed-by=/usr/share/keyrings/deb.sury.org-php.gpg] https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'

sudo apt update

# Установите новые пакеты PHP 8.3
sudo apt install php8.3 php8.3-cli php8.3-{bz2,curl,mbstring,intl}

# Установите FPM для Nginx
sudo apt install php8.3-fpm

# или Apache модуль
# sudo apt install libapache2-mod-php8.3
# Тут же для Apache включите PHP 8.3 FPM
sudo a2enconf php8.3-fpm

# Выключить предыдущие версии:
sudo a2disconf php8.2-fpm

# Удалите старые пакеты если надо
sudo apt purge php8.2*
```
## Ubuntu (20.04, 22.04, 24.04)
```bash
# Сохранить существующий список пакетов PHP в файл packages.txt.
sudo dpkg -l | grep php | tee packages.txt

# Репозиторий Ondrej PPA
sudo add-apt-repository ppa:ondrej/php # Нажмите Enter

sudo apt update

# Установка PHP 8.3 и расширений
sudo apt install php8.3 php8.3-cli php8.3-{bz2,curl,mbstring,intl}

# Установка FPM
sudo apt install php8.3-fpm

# или Apache модуль
sudo apt install libapache2-mod-php8.3
# Для Apache включить PHP 8.3 FPM
sudo a2enconf php8.3-fpm
# выключаем предыдущие версии Apache:
sudo a2disconf php8.2-fpm

# удаляем старую версию если надо
sudo apt purge php8.2*
```
## Подробное руководство по установке/обновлению PHP 8.3

Ни одна из текущих версий Debian и Ubuntu не включает PHP 8.3 в репозитории программного обеспечения по умолчанию. Готовые пакеты PHP доступны из репозитория, поддерживаемого [Ondřej Surý](https://launchpad.net/~ondrej), который и используется в этой статье. Пакеты в этом репозитории имеют ту же конфигурацию, имена пакетов и конфигурацию systemd, что и пакеты PHP, предоставляемые репозиториями программного обеспечения ОС.

В этой статье основное внимание уделяется Ubuntu 22.04 (Jammy), Ubuntu 20.04 (Focal), Ubuntu 24.04 (Noble), Debian 10 (Buster), Debian 11 (Bulseye) и Debian 12 (Bookworm), как последним актуальным версиям.
## Перечислить и записать существующие пакеты PHP

При обновлении существующей версии PHP следующая команда перечисляет все установленные пакеты со словом php в имени пакета и сохраняет их в файл packages.txt, а также выводит их в терминале.

Это будет полезно для установки соответствующих пакетов PHP 8.3 на следующих шагах.

Этот шаг не обязателен при установке PHP в новой системе.
```bash
dpkg -l | grep php | tee packages.txt
```
## Добавить репозиторий ondrej/php

Следующие команды добавляют репозиторий в список репозиториев программного обеспечения и запускается apt update для получения списка пакетов, доступных из нового репозитория, а также из существующих репозиториев.

**Debian**
```bash
sudo apt install apt-transport-https
sudo curl -sSLo /usr/share/keyrings/deb.sury.org-php.gpg https://packages.sury.org/php/apt.gpg
sudo sh -c 'echo "deb [signed-by=/usr/share/keyrings/deb.sury.org-php.gpg] https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
sudo apt update
```
**Ubuntu**
```bash
sudo add-apt-repository ppa:ondrej/php # Нажмите Enter
sudo apt update
```
## Установить расширения PHP 8.3

После добавления репозитория PHP Ондрея, расширения PHP теперь можно устанавливать с помощью apt. Все пакеты PHP 8.3 следуют ставить по шаблону php8.3-name_ext. Эти имена совпадают и переопределяют версии PHP, предоставленные собственными репозиториями ОС.
```bash
sudo apt install php8.3-common php8.3-cli php8.3-fpm php8.3-{curl,bz2,mbstring,intl}
```
Расширение php8.3-common представляет собой метапакет, который устанавливает несколько расширений PHP. Позже можно выборочно отключить отдельные расширения. Нет необходимости и возможности устанавливать их как отдельные пакеты.
## Дополнительные расширения PHP

В репозитории также доступно несколько расширений PECL, которые можно легко установить без необходимости компилировать. Сюда входят некоторые наиболее популярные расширения PECL, такие как Image Magick, APCu, Xdebug и Redis.
## Интеграция с веб-сервером

В большинстве случаев PHP интегрирован с веб-сервером. Интеграция с PHP-FPM по протоколу Fast CGI является наиболее распространенным подходом, хотя также возможна интеграция PHP с другими SAPI.
### Nginx, Caddy , Litespeed и другие серверы через Fast CGI

После установки PHP-FPM - php8.3-fpm systemd регистрирует службу для PHP 8.3 FPM по адресу сокета /run/php/php8.3-fpm.sock.
### Apache
```bash
sudo a2enconf php8.3-fpm
sudo a2disconf php8.2-fpm # When upgrading from an older PHP version
sudo systemctl restart apache2
```
Если Apache настроен для запуска PHP в качестве модуля Apache (обычно называемого mod_php или mod_php8), установите libapache2-mod-php8.3 пакет вместо php8.3-fpm:
```bash
sudo apt install libapache2-mod-php8.3
sudo a2enmod php8.3

# Выключить предыдущую версию и перезагрузить Apache
sudo a2dismod php8.2 
sudo systemctl restart apache2
```
## Тест/проверка установки PHP 8.3

После установки всех пакетов наступает момент истины, чтобы проверить, прошла ли новая установка успешно:
```bash
php -v
```
```powershell
PHP 8.3.0 (cli) (built: Nov 23 2023 08:49:45) (NTS)
Copyright (c) The PHP Group
Zend Engine v4.3.0, Copyright (c) Zend Technologies
    with Zend OPcache v8.3.0, Copyright (c), by Zend Technologies
```
## Удалить старые версии PHP

Чтобы удалить старые версии PHP, запустите apt purge с префиксом версии PHP. Например, следующие команды удаляют пакеты и конфигурацию PHP 8.2:
```bash
sudo apt purge php8.2*
```
## Запуск PHP 8.3 вместе с другими версиями PHP

PHP 8.3 можно установить и использовать вместе с другими версиями PHP. Именно это и происходит при установке PHP 8.3 без предварительного удаления старых пакетов PHP.
```bash
sudo update-alternatives --config php
```
По умолчанию `php` будет связано с последней версией PHP, но его можно изменить. Используйте команду `update-alternatives`. При этом появится приглашение интерактивно выбрать альтернативный путь PHP.
```
  Выбор   Путь         Приор Состояние
------------------------------------------------------------
* 0            /usr/bin/php8.3   83        автоматический режим
  1            /usr/bin/php8.2   82        ручной режим
  2            /usr/bin/php8.1   81        ручной режим
Нажмите «enter», чтобы не менять текущий выбор[*], или введите нужное число: 
```

Источник: https://sergeymukhin.com/blog/kak-ustanovitobnovit-php-83-v-ubuntu-ili-debian
