# PostgreSQL 14 Installation on Fedora 7.9

#### Reference Links

* https://yallalabs.com/databases/how-to-install-and-use-postgresql13-centos-7/

* https://computingforgeeks.com/how-to-install-postgresql-14-centos-rhel-7/ 
            
#### Important Postgres Paths in Fedora
    > Config Path : cat /var/lib/pgsql/14/data/postgresql.conf
    > hba file path : cat /var/lib/pgsql/14/data/pg_hba.conf           
 
#### Password for users 
   > 'postgres' is Root@123   
    
   > 'test_user is Root@123   
                                                                                                                                                              
#### Installation of PostgreSQL Server

##### Step 1 — Add the PostgreSQL repository:


  > sudo yum -y install https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm

_Note : Update The Server After Adding the Repository_
  > sudo yum -y update 

##### Step 2 — Install PostgreSQL 14.2 

  > sudo yum install -y postgresql14-server postgresql14
  

##### Step 3 — Check if PostgreSQL is installed 
  > which psql

  > psql --version

_Note : In our case we have installed PostgreSQL 14.2_


##### Step 4 - Initialize the database
  > sudo /usr/pgsql-14/bin/postgresql-14-setup initdb

<code>initdb creates a new PostgreSQL database cluster. A database cluster is a collection of databases that are managed by a single server instance.</code>


##### Step 5 - Enable and start the PostgreSQL service
  > sudo systemctl enable --now postgresql-14

  _Note : This will create symlink as below :_

<code>Created symlink from /etc/systemd/system/multi-user.target.wants/postgresql-14.service to /usr/lib/systemd/system/postgresql-14.service.</code>
        
        

##### Step 5 - Check the status after Enabling PostgreSQL service
  > sudo systemctl status postgresql-14  

<code>Loaded: loaded (/usr/lib/systemd/system/postgresql-14.service; enabled; vendor preset: disabled)
Active: active (running) </code>

#### PostgreSQL Usage Examples
1 - PostgreSQL by default creates a user named postgres. Access the PostgreSQL Database Server:
    
   * Switch into the postgres user
   
       ``` 
       $ sudo su - postgres
       ```

   * Connect to the PostgreSQL terminal

        ``` 
        $ psql
        ```
   * Set Strong Password for 'postgres' user

        ``` 
        postgres=# alter user postgres with password 'PostgresStr0ngPassw0rd#';
        ```
2 - List all the databases

   ``` 
     # \list or \l
   ```

3 - Create New Database 

   ``` 
     # CREATE DATABASE demodb;
   ``` 

4 - Connect to an existant PosgreSQL database named demodb:

   ``` 
     # \c demodb
   ``` 

5 -  Create a table named employees

   ``` 
     # create table employees (name varchar(25), surname varchar(25));
   ``` 

6 - List all the tables

   ``` 
     # \d
   ```        

7 - Insert a couple of rows into the new table named employees

   ``` 
     # INSERT INTO employees VALUES ('Abhishek','Budruk');
     # INSERT INTO employees VALUES ('Chetan','Patil');
   ```        

8 - Query all rows from the table named employees

   ``` 
     # SELECT * FROM employees;
   ```        

9 - Exit from PosgreSQL prompt

   ``` 
     # \q
   ```     

#### Access PostgreSQL using command Line

1 - Connect to the username 'postgres'

   ``` 
     sudo -u postgres psqL
   ```      
           
           
#### Uninstall Postgres from Fedora

``` 
 yum remove postgresql
 yum remove postgres\*
 rm -rf /var/lib/pgsql


 rpm -qa | grep postgres
 rpm -qa | grep post
 yum list installed | grep postgres
 yum remove {POSTGRESS-PACKAGE NAME}


```        

#### Create New Dababase and User for Your Project

Step 1 - Connect to 'postgres' user

   ``` 
     sudo -u postgres psqL
   ```      

Step 2 - Create User in Postgres Utility
   ``` 
   Command :
       postgres=# CREATE USER $USER WITH PASSWORD '$PASSWORD';
   Example:                   
       postgres=# CREATE USER test_user WITH PASSWORD 'Root@123';
   ```     

Step 3 - Create Database in Postgres Utility
   ``` 
   Command :
       postgres=# CREATE DATABASE $DB;
   Example:                   
       postgres=# CREATE DATABASE test_db;
   ```        

Step 4 - Grant All the Privileges to the Created User
   ``` 
   Command :
       postgres=# GRANT ALL PRIVILEGES ON DATABASE $DB to $USER;
   Example:                   
       postgres=# GRANT ALL PRIVILEGES ON DATABASE test_db to test_user;
   ``` 

Step 5 - Quit the postgres utility
   ```
      postgres =# \q
   ```

Step 6 - Access the new created db using following command 
   ```
   Command :
      ~# psql -h <host-name> -d <database-name> -U <user-name> ​
   Example:  
      ~# psql -h localhost -d test_db -U test_user; 
   ```                               

#### Make postgres database available over the public internet

##### Error 
  > ~# psql -U postgres -h 10.171.58.216
    
      psql: could not connect to server: Connection refused
      Is the server running on host "10.171.58.216" and accepting
      TCP/IP connections on port 5432?

Step 1 - Modify pg_hba.conf to add Client Authentication Record. Add 
    0.0.0.0/0 to this file as shown below 
   ```  
   ~# vi /var/lib/pgsql/14/data/pg_hba.conf; 
   ```      
      
   > host    all             all             0.0.0.0/0               scram-sha-256

      

Step 2 - Change the Listen Address in postgresql.conf
   ```  
      ~# vi /var/lib/pgsql/14/data/postgresql.conf; 
   ```      
               
   > listen_addresses = '*'


Step 3 - Test Your Remote Connection
   ```  
      ~# sudo psql -U test_user -d test_db -h 10.171.58.216 
   ```      
               
   _Note : 10.171.58.216 is the IP Address of your machine_     