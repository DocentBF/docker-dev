# Сборка Docker для локальной разработки

## Состав
- Nginx
- Php-fpm:7.4
- Php-fpm:8.2
- MariaDB:11
- Memcached
- Redis
- MailCatcher
- Node 16

## Конфигурация
- На основе `.env.sample` делаем свой `.env`.
    - Для Linux: указываем id и id группы своего пользователя. Узнаем с помощью `id -u` `id -g` в терминале соответственно
- В директорию `www/site.local` кладем файлы сайта
- В файлах `php.ini` (8.2, 7.4) указываем `xdebug.client_host` согласно ОС
- Можно добавить неограниченное кол-во хостов в папке `config/nginx`.
- MySQL доступен по localhost:3307
- Почтовая заглушка доступна по http://localhost:1080/

### Настройка XDebug
Указываем в PHPStorm порт для XDebug равный 9008.

Для справки: https://blog.denisbondar.com/post/phpstorm_docker_xdebug/#%d0%bd%d0%b0%d1%81%d1%82%d1%80%d0%be%d0%b9%d0%ba%d0%b0-phpstorm