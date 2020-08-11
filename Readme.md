# Postgresql Cheatsheet 
### by Nissan Devnath
#### prepared for **Brilliant Cloud Research Team**

## Installing PostgreSQL in Windows 10
To download Postgresql visit their official [website](https://www.postgresql.org/download/)

> If theres some error during installation saying vc++ not installed then follow these steps

* Create a shourtcut of the downloaded file.  
* Go to the properties of the shourcut and in the target field add this line ```--install_runtimes 0``` 

![image_2](images/two.png)

* Now install

## Adding PostgreSQL to Path variable

To add PostgreSQL to the path we have to copy the path to PostGreSQL installation directory to the path variable.

* First we have to copy the path to the bin folder in the installation directory.
![image_3](images/three.png)

* Then we open the System Environment Variables Setting
![image_4](images/four.png)

* Then we go to the **Environment Variables** option
![image_5](images/five.png)

* Then we add a new line to the Path and paste our copies directory path
![image_6](images/six.png)


Now we can access PostgreSQL from Commandline interface. 

## Acessing PostgreSQL local database

When we install PostgreSQL the default username is postgres. So to login as the default user we use the command

` psql -U postgres`

After that we will have to provide the password that we set during installation . Then we will be logged in as default user.

![image_7](images/seven.png)

To get help we have to type:

`\?`

![image_8](images/eight.png)

## Creating and Inserting data into database

To get the list of all the data bases we have to type:

`\l`

![image_nine](images/nine.png)

If we want to create a new database we have to type:

`CREATE DATABASE database_name;`

Let's say we want to create a database named **test** . So we have to type:

`CREATE DATABASE test;`

![image_ten](images/ten.png)

To drop or delet a database we have to type:

`DROP DATABASE database_name;`

So, if we want to drop the **test** database that we created we have to type:

`DROP DATABASE test;`

![image_11](images/eleven.png)

To connect to a database we have to type:

`\c database_name`

Let's say we want to connect to a database named **nissan** ,then we have to type:

`\c nissan`

![image_12](images/twelve.png)

### Creating a table in a database

To create a table we have to type :

```
CREATE TABLE table_name(
    column_name data_type constraints(if any)
);
```
Let's say we want to create a table named **person** with the columns of **id** which is a *integer* datatype, **first_name, last_name** and **gender** which are of type *charachter(varchar)* and date_of_birth which is of type *DATE* . So we have to type:

```
CREATE TABLE person (
   id INT,
   first_name VARCHAR(50),
   last_name VARCHAR(50),
   gender VARCHAR(8),
   date_of_birth DATE 
);
```
This command will create a table without any constrains which means that if we want we can insert a empty entry into the table. So to avoid these situations we want to creata a table with constraints in that way we can't insert a blank entry into the table .

If we want to create the same table with constraints then we would have to type:
```
CREATE TABLE person(
    id BIGSERIAL NOT NULL PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    gender VARCHAR(8) NOT NULL,
    date_of_birth DATE NOT NULL,
    email VARCHAR(100), 
);
```

In the above command we created a table similar to the one before but we have added constraints to the table like we have added `NOT NULL` to id,first_name, last_name, gender, date_of_birth but we have to added any constraints to the email column. So if we want we can make a new entry in the **person** column without giving an email id . Moreover we have added data type of *BIGSERIAL* to the id column and made it a `PRIMARY KEY`, which means id column will have an auto increasing value with every entry in the table and as it's a primary key it'll have unique value by which we can uniquely identify an entry.

### Inserting records into the table

To insert records into the table we have to type in the format:
```
INSERT INTO person(
    column_names
) 
VALUES (column_values);
```
In our case if we want to insert a record into our previously created table then we have to type:
```
INSERT INTO person(
    first_name,
    last_name,
    gender,
    date_of_birth,
    email
) VALUES('Nissan', 'Devnath', 'MALE', DATE '1998-03-23', 'xyz@mail.com');
```

This will create an entry into the table with the first_name of Nissan, last_name of Devnath, gender of MALE, date_of_birth 1998-03-23 and email of xyz@mail.com . But in the insert command we didn't give any **id** value because the id value is a BIGSERIAL as a result it will increment automatically in every entry.
