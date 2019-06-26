# POSTGRES
Command | Semantic
------- | --------
`sudo service postgresql restart` | restart PostgreSQL
`sudo -u postgres createdb ebz9` | create database
`sudo -u postgres dropdb ebz9` | remove database
`sudo -u postgres psql ebz9 < db_backup.sql` | run script on database
`sudo -i -u postgres psql` | enter to psql mode
`\password postgres` | change password for postgres user
`\list` | show all databases
`\c ebz9` | switch to table **ebz9**
`\d+ table_name` | show DDL of table

Extend `VARCHAR` column to **2096** symbols:
```postgresql
ALTER TABLE tablename ALTER COLUMN columnname TYPE varchar(2096);
```
#### Installation
```bash
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ bionic-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'
wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - | sudo apt-key add -
sudo apt-get update
sudo apt-get install postgresql-9.6 postgresql-client-9.6 libpq-dev pgadmin3
```

#### Open external connections
```bash
sudo mcedit /etc/postgresql/9.6/main/postgresql.conf
```
Set `listen_addresses` to `'*'`
```bash
sudo mcedit /etc/postgresql/9.6/main/pg_hba.conf
```
Add string `host all all 0.0.0.0/0 md5`

#### HQL
Query for potentially empty collection
```java
@Query("from User where (id in ?1 or ?1 is null)")
List<User> sandbox(List<Integer> ids);
```