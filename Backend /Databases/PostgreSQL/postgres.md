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
