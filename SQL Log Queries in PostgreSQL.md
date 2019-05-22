See [How to show queries log in PostgreSQL?](https://tableplus.io/blog/2018/10/how-to-show-queries-log-in-postgresql.html)

Quick Summary:

Edit postgresql.conf

```
vi /etc/postgresql/9.5/main/postgresql.conf
```

Uncomment lines at 630

```
#log_statement = 'all'
#log_directory = 'pg_log'
#log_filename = 'postgresql-%Y-%m-%d_%H%M%S.log'
#logging_collector = on
#log_min_error_statement = error
```

Restart PostgreSQL

```
sudo /etc/init.d/postgresql restart
```

Tail the log file

```
cd /var/lib/postgresql/9.5/main/pg_log
ls -lrt
tail -f postgresql-2019-0....
```

