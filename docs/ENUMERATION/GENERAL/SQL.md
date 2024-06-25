# SQL
#mysql
``` sql
mysql -u root -p'root' -h 192.168.50.16 -P 3306
select version();
select system_user();
show databases;
SELECT user, authentication_string FROM mysql.user WHERE user = '[user]';
```

#mssql 
``` sql
impacket-mssqlclient [username]:[password]@[ip] -windows-auth
SELECT @@version;
SELECT name FROM sys.databases;
SELECT name FROM sys.objects WHERE type = 'U';
SELECT * FROM [database].information_schema.tables;
select * from [database].dbo.users;
```



master.dbo.sysusers table is a default table in older versions of MSSQL