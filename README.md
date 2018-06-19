# Free Proxy List site

Цель: Собирать список публичных прокси серверов и проверять их: доступность, пинг, степень анонимности*.  
Интерфейс для вывода списка серверов, со статусами и фильтрами: (фильтры про стране, доступности, классу анонимности)

Стек технологий: Laravel, команды Laravel, 
Cron для запуска заданий, UI kit (Bootstrap 3)  
Json интерфейс для получения прокси.

## Установка

1) Отредактировать  /.env
2) Выполнить команду 
```bash  
 php artisan migrate
```
3) Создать cron команды:
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
