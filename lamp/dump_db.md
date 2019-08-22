## How to dump SQL databese

sign-in on your guest machine and run the following command: 

**Step 1: Dump sql**

```
$ mysqldump -u [uname] -p db_name > db_backup.sql
```

if you don't know the database name, you can find it using `mysql`:

```
$ mysql --user=your-user-name --password=your-password
```

then:

```
mysql> show databases;
```

output:

```
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
+--------------------+
2 rows in set (0.00 sec)
```

**Step 2: Download sql file from your computer**

```
scp user@IP_ADDRESS:/PATH_TO_SQL_FILE ~/PATH_TO_LOCAL
```

@reference:  

* [MySQL command to show list of databases on server](https://www.cyberciti.biz/faq/mysql-command-to-show-list-of-databases-on-server/)   
* [How to download a file from server using SSH?](https://stackoverflow.com/questions/9427553/how-to-download-a-file-from-server-using-ssh) (read comments)

