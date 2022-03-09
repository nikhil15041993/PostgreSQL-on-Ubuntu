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

## 2. Configure PostgreSQL to allow remote connection

By default PostgreSQL is configured to be bound to "localhost".

```
$ netstat -nlt
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp        0      0 0.0.0.0:443             0.0.0.0:*               LISTEN
tcp        0      0 127.0.0.1:11211         0.0.0.0:*               LISTEN
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN
tcp        0      0 127.0.0.1:5432          0.0.0.0:*               LISTEN
tcp        0      0 127.0.0.1:3737          0.0.0.0:*               LISTEN
tcp6       0      0 :::22                   :::*                    LISTEN
```
As we can see above port 5432 is bound to 127.0.0.1. It means any attempt to connect to the postgresql server from outside the machine will be refused. 

### Configuring postgresql.conf:

Now we need to open the file and make some changes in order to allow remote connection. To open the file you’ve to use the keyword “nano” or you can run the command in the terminal that is provided below:
```
sudo nano /etc/postgresql/13/main/postgresql.conf 
```

This command will open this file and in it, you need to search “listen_addresses” and add the following line.
```
#listen_addresses = 'localhost'
listen_addresses = '*'
```

### Configuring pg_hba.conf:

In order to allow the users that we want to be connected to the database then we need to make changes in the “pg_hba.conf” file. This file will be available under the same directory as above.

Now open the file using the command provided below:
```
sudo nano /etc/postgresql/13/main/pg_hba.conf 
```
In the file you’ve to add the following lines in file:

```
# TYPE  DATABASE	USER	ADDRESS   	METHOD
host    all     	all     0.0.0.0/0      md5
host    all             all     :/0      md5
```

Now, restart your database by executing the below given command:
```
sudo systemctl restart postgresql 
```
Now simply open the port “5432” in the firewall
```
sudo ufw allow 5432 
```


```
eg:  psql -h 107.170.158.89 -U postgres
```
