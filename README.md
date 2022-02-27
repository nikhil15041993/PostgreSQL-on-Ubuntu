# PostgreSQL-on-Ubuntu

PostgreSQL, or Postgres, is a relational database management system that provides an implementation of the SQL querying language.

## Step 1 — Installing PostgreSQL

first refresh your server’s local package index:
```
sudo apt update
```
Then, install the Postgres package along with a -contrib package that adds some additional utilities and functionality:
```
sudo apt install postgresql postgresql-contrib
```

## Step 2 — Using PostgreSQL Roles and Databases

By default, Postgres uses a concept called “roles” to handle authentication and authorization. These are, in some ways, similar to regular Unix-style users and groups.

The installation procedure created a user account called postgres that is associated with the default Postgres role. There are a few ways to utilize this account to access Postgres. One way is to switch over to the postgres account on your server by running the following command:

```
sudo -i -u postgres
```
Then you can access the Postgres prompt by running:
```
psql
```
This will log you into the PostgreSQL prompt, and from here you are free to interact with the database management system right away.

```
eg:

\q = for exit
\du = list user
\l = show databases

```
## Step 3 — Creating a New Role

You can create user in interactive mode, or normal mode.
You will be logged into PostgreSQL as superuser. Run the following command
```
createuser --interactive --pwprompt
```
```
Postgres will next ask you to enter new user details one by one, as shown below

Enter name of role to add – enter new user name
Enter password for new role – enter password for new user
Enter it again – enter password again
Shall the new role be a superuser- Enter Y if you want to create user with superuser privileges. Else enter N
Shall the new role be allowed to create databases- Enter Y if you want new user to be able to create databases, else enter N.
Shall the new role be allowed to create new roles- Enter Y if you want new user to be able to create new users, else enter N.
```
PostgreSQL will create your user.

#### Normal mode or non-interactive mode
In this mode PostgreSQL will directly create new user without prompting you for any information.

```
postgres=# create user user_name with encrypted password 'mypassword';
postgres=# ALTER USER techibeans WITH PASSWORD 'admin@123';
```
If you want to grant access to new user to your database sample_db, run the following command
```
postgres=# grant all privileges on database sample_db to user_name;
```
If i want to add new user to super user privilage
```
postgres=# ALTER USER admin WITH SUPERUSER;
```
For drop a user

```
postgres=# DROP USER username;
```
CREATE DATABASE
```
postgres=# CREATE DATABASE <databasenae>;
```
SWITCH TO DATABASE
```
postgres=# \c guru99
```
