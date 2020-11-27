# PostgreSQL Cheatsheet

psql command line interface with superadmin **postgres**

```
sudo -u postgres psql;
```

Create User

```
sudo -u postgres createuser <username>;
```

Create Database

```
sudo -u postgres createdb <dbname>;
```

Change Password

```
alter user <username> with encrypted password '<password>';
```

Grant Database Access

```
grant all privileges on database postgres to <username>;
```

## Database Commands

Change Database:

```
\c dbname
```

`\d` show databases | `SHOW TABLES` mySQL

```
SELECT table_name FROM information_schema.tables WHERE table_schema = 'public';
```

`\l` show tables in db | `SHOW DATABASES` mySQL

```
SELECT datname FROM pg_database;
```

`\d table` show columns in table | `SHOW COLUMNS` mySQL

```
SELECT column_name FROM information_schema.columns WHERE table_name ='table';
```

`\d+ table` show data in specific column | `DESCRIBE TABLE` mySQL

```
SELECT column_name FROM information_schema.columns WHERE table_name ='table';
```

Viewing Column Data:

```
\x # toggle expanded view for readability
SELECT * FROM tablename LIMIT 10;
SELECT DISTINCT column_name from table_name;
```
