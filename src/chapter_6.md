# Backup and Recovery

In this section, we will explore the various methods available for backing up and restoring databases in MySQL 8.4. Proper backup and recovery strategies are crucial for data integrity and disaster recovery. We will cover both logical and physical backups and provide examples to illustrate these processes.

## Backup Methods

### Logical Backups

Logical backups involve exporting the database structure and data into a format that can be easily read and restored. The most common tool for logical backups in MySQL is `mysqldump`.

#### Using `mysqldump`

`mysqldump` is a utility that generates SQL statements to recreate the database schema and its data. Here’s how to perform a logical backup using `mysqldump`:

```bash
mysqldump -u [username] -p [password] [database_name] > [backup_file].sql
```

- `-u [username]`: The username to connect to the MySQL server.
- `-p [password]`: The password for the MySQL user.
- `[database_name]`: The name of the database you want to back up.
- `[backup_file].sql`: The file where the backup will be stored.

**Example:**

```bash
mysqldump -u root -p mydatabase > mydatabase_backup.sql
```

### Physical Backups

Physical backups involve copying the actual database files. These backups are generally faster and more suitable for large databases. MySQL provides a tool called `mysqlbackup` as part of the MySQL Enterprise Backup suite for this purpose.

#### Using `mysqlbackup`

`mysqlbackup` can perform hot backups, which means it can back up data while the database is running, with minimal impact on performance.

**Example of a Full Backup:**

```bash
mysqlbackup --user=[username] --password=[password] --backup-dir=[backup_directory] backup-and-apply-log
```

- `--user=[username]`: The username to connect to the MySQL server.
- `--password=[password]`: The password for the MySQL user.
- `--backup-dir=[backup_directory]`: The directory where the backup will be stored.

**Example:**

```bash
mysqlbackup --user=root --password=my_password --backup-dir=/backups/full_backup backup-and-apply-log
```

## Recovery Methods

### Logical Recovery

To restore a database from a logical backup created with `mysqldump`, you can use the `mysql` command to execute the SQL statements stored in the backup file.

#### Using `mysql`

```bash
mysql -u [username] -p [password] [database_name] < [backup_file].sql
```

- `-u [username]`: The username to connect to the MySQL server.
- `-p [password]`: The password for the MySQL user.
- `[database_name]`: The name of the database to restore.
- `[backup_file].sql`: The backup file to restore from.

**Example:**

```bash
mysql -u root -p mydatabase < mydatabase_backup.sql
```

### Physical Recovery

To restore a database from a physical backup, you need to use the `mysqlbackup` tool to copy the backed-up files back to the MySQL data directory.

#### Using `mysqlbackup`

**Example of a Full Restore:**

```bash
mysqlbackup --user=[username] --password=[password] --backup-dir=[backup_directory] --datadir=[mysql_data_directory] copy-back
```

- `--user=[username]`: The username to connect to the MySQL server.
- `--password=[password]`: The password for the MySQL user.
- `--backup-dir=[backup_directory]`: The directory where the backup is stored.
- `--datadir=[mysql_data_directory]`: The MySQL data directory where the database files will be restored.

**Example:**

```bash
mysqlbackup --user=root --password=my_password --backup-dir=/backups/full_backup --datadir=/var/lib/mysql copy-back
```

After copying the files back, you may need to update the permissions and restart the MySQL server:

```bash
chown -R mysql:mysql /var/lib/mysql
systemctl restart mysqld
```

## Conclusion

Backing up and restoring MySQL databases are essential tasks for database administrators to ensure data availability and integrity. MySQL 8.4 offers both logical and physical backup methods to suit different needs. By using `mysqldump` for logical backups and `mysqlbackup` for physical backups, you can create a robust backup and recovery strategy for your databases.
