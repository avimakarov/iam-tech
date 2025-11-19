Представление pg_stat_activity 
позволяет взглянуть на работу процессов с точки зрения PostgreSQL

* Поднимем локальный инстанс PostgreSQL и зайдем в консоль БД
```sh
$ git clone https://github.com/lesovsky/postgresql-monitoring-book.git
$ cd postgresql-monitoring-book/playground
$ make up
$ make primary/psql
```

* Посмотрим описание представления pg_stat_activity;
```sh
$ \d pg_stat_activity

                      View "pg_catalog.pg_stat_activity"
      Column      |           Type           | Collation | Nullable | Default 
------------------+--------------------------+-----------+----------+---------
 datid            | oid                      |           |          | 
 datname          | name                     |           |          | 
 pid              | integer                  |           |          | 
 leader_pid       | integer                  |           |          | 
 usesysid         | oid                      |           |          | 
 usename          | name                     |           |          | 
 application_name | text                     |           |          | 
 client_addr      | inet                     |           |          | 
 client_hostname  | text                     |           |          | 
 client_port      | integer                  |           |          | 
 backend_start    | timestamp with time zone |           |          | 
 xact_start       | timestamp with time zone |           |          | 
 query_start      | timestamp with time zone |           |          | 
 state_change     | timestamp with time zone |           |          | 
 wait_event_type  | text                     |           |          | 
 wait_event       | text                     |           |          | 
 state            | text                     |           |          | 
 backend_xid      | xid                      |           |          | 
 backend_xmin     | xid                      |           |          | 
 query_id         | bigint                   |           |          | 
 query            | text                     |           |          | 
 backend_type     | text                     |           |          | 
```

* Информация о клиенте
    **datname** 
        * Имя БД, к которой выполнено подключение
    **username**
        * Имя пользователя при подключении
    * **client_addr**
        * Сетевой адрес, с которого установлено соединение с БД
    * **client_port**
        * Номер порта удаленной машины, с которого установлено соединение с БД

* Продолжительность сеанса, транзакции, запроса
    **xact_start** 
        * Время начала транзакции
    **query_start**
        * Время начала текущего запроса, если он не единственный в транакции
    **backend_start**
        * Время начала сеанса, те время подключения клиента к СУБД

