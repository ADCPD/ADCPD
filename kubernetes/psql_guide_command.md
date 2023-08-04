# PSQL GUIDE

---

Top psql commands and flags you need to know | PostgreSQL
Source : https://hasura.io/blog/top-psql-commands-and-flags-you-need-to-know-postgresql

## Connect to POD 

- From infra folder : 

```bash
kubectl -n default get po | grep post

k -n default exec -it postgres-client  bash
```

## Access to your database 

- **If the database is on the same host as your machine, you can use the following command:**

```bash
psql -U waste_man@3slabdevpostgres -W -h 3slabdevpostgres.postgres.database.azure.com waste_man
> password : b3N0Z3zc2J!enVyZS5R
```

The above command includes three flags:

-d  // specifies the name of the database to connect to
-U  // specifies the name of the user to connect as
-W  // forces psql to ask for the user password before connecting to the database

- **Different host database**

```bash
psql -h <db-address> -d <db-name> -U <username> -W

//example
psql -h my-psql-db.cloud.neon.tech -d tutorials_db -U admin -W
```
The -h flag specifies the host address of the database.

- **SSL mode**

There might be cases where you want to use SSL for the connection.
```sh
psql "sslmode=require host=<db-address> dbname=<db-name> user=<username>"

//example
psql "sslmode=require host=my-psql-db.cloud.neon.tech dbname=tutorials_db user=admin"
```

### Command 

1. List all databases

```sh
postgres=# \l
```

2. Switch to another database "schemas"

```sh
postgres=# \c waste_man
```

3. List database tables

```sh
waste_man=# \dt
```

4. Describe a table

psql also has a command that lets you see the table's structure.


```sh
waste_man=# \d ref_contract
```

If you want more information about a table, you can use the command:

```sh
waste_man=# \d+ ref_contract
```

5. List all schemas

```sh
waste_man=# \dn 
```
It returns the name of the schemas and their owners.

6. List users and their roles

```sh
waste_man=# \du
```

7. Retrieve a specific user

```sh
waste_man=# \du <username>
```

8. List all functions

```sh
waste_man=# \df
```
The command returns all functions and the:
- schema they belong to
- names
- result data type
- argument data types
- type

9. List all views

```sh
waste_man=# \dv
```

10. Save query results to a file 

```sh
\o <file-name>

// example
\o query_results
...run the psql commands...
\o - stop the process and output the results to the terminal again
```
**Note:** To stop saving results to the file, you need to run the \o command again without the file name.

11. Run commands from a file
It's also possible to run commands from a file. For simple commands, it might not be the best solution. But when you want to run multiple commands and complex SQL statements, it helps a lot.
Create a txt file with the following content:
 
```sh
\l
\dt
\du
```

When you run the file, it should return a list of all:
- databases
- database tables
- users

You can run commands from a file with the following psql command:
```sh
\i <file-name>

// example
\i psql_commands.txt
```


12. Quit psql

```sh
waste_man=# \q
```
