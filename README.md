# Free Proxy List site

![preview](https://raw.githubusercontent.com/cyberpaste/free-proxy-list-site/master/preview.jpg)

Цель: Собирать список публичных прокси серверов и проверять их: доступность, пинг, степень анонимности*.  
Интерфейс для вывода списка серверов, со статусами и фильтрами: (фильтры про стране, доступности, классу анонимности)

Стек технологий: Laravel, команды Laravel, 
Cron для запуска заданий, UI kit (Bootstrap 3)  
Json интерфейс для получения прокси.

## Установка
1) Установить Laravel
```bash 
composer create-project laravel/laravel
```
2) Загрузить файлы из этого репозитория в папку с проектом
3) Отредактировать  /.env
4) Выполнить команду в консоли
```bash  
 php artisan migrate
```
5) Создать cron команды:
  ```bash 
   curl --insecure 'https://free-proxy-list-site.com/check' > /dev/null >/dev/null 2>&1     */1	*	*	*	*
   ```
  ```bash 
   curl --insecure 'https://free-proxy-list-site.com/add' > /dev/null >/dev/null 2>&1     1	    23	*	*   * 
  ```
  
  
* проверка на анонимность и тип не сделана. 

Скрипт работает так: подгружает список с сторонего сервиса.
Добавляет его в базу. 
Крон его проверяет. 
Если весь список проверен, то идет проверка прокси, дата проверки которых самая старая (и так по кругу).

Скрипт в день проверяет 14400 прокси (по 10 за крон задачу).
