![Oracle Logo](https://upload.wikimedia.org/wikipedia/commons/thumb/5/50/Oracle_logo.svg/1200px-Oracle_logo.svg.png)


# Cheat Sheet
A concise set of notes about Oracle Database used for quick reference

## About Oracle Database
Oracle Database is a Relational Database Management System with the largest market share. Oracle Database allows you to quickly and safely store and retrieve data.
Some features to highlight are:
* **Cross-platform** – It can run on various hardware across operating systems including Windows Server, Unix, and various distributions of GNU/Linux.
* **ACID-compliant** – Oracle is ACID-compliant Database that helps maintain data integrity and reliability.
* **Logical data structure** – Oracle uses the logical data structure to store data so that you can interact with the database without knowing where the data is stored physically.
* **Partitioning** – is a high-performance feature that allows you to divide a large table into different pieces and store each piece across storage devices.
* **Memory caching** – the memory caching architecture allows you to scale up a very large database that still can perform at a high speed.
* **Backup and recovery** – ensure the integrity of the data in case of system failure. Oracle includes a powerful tool called Recovery Manager (RMAN) – allows DBA to perform cold, hot, and incremental database backups and point-in-time recoveries.
* **Clustering** – Oracle Real Application Clusters (RAC) – Oracle enables high availability that enables the system is up and running without interruption of services in case one or more server in a cluster fails.

## Main data types
An overview of the built-in Oracle data types:
<h3>CHAR(length)</h3>
<p>- stores fixed-length string</p>
<p>- the <b>length</b> parameter specifies the length of the string, if the length is shorter, the rest will be filled with spaces</p>

<h3>VARCHAR2(length)</h3>
<p>- stores variable length string</p>
<p>- the <b>length</b> parameter specifies the maximum length of the string</p>

<h3>DATE</h3>
<p>- stores date and time</p>

<h3>INTEGER</h3>
<p>- stores integer values</p>

<h3>NUMBER(x,y)</h3>
<p>- stores float or integer numbers</p>
<p>- <b>x</b>: maximum number of digits in all number</p>
<p>- <b>y</b>: maximum number of digits to the right of the decimal point</p>

<h3>BINARY_FLOAT</h3>
<p>- stores a 32 bits float number</p>

<h3>BINARY_DOUBLE</h3>
<p>- stores a 64 bits double number</p>

<p></p>

> The complete list of data types can be checked [in here](https://docs.oracle.com/cd/E11882_01/appdev.112/e10646/oci03typ.htm#LNOCI030)

<p></p>


# SQL Commands

![SQL commands](https://i.stack.imgur.com/7uUaJ.png)


## DDL - Data Definition Language
<p>For instance here is going to be used a small market database.</p>
<h3>CREATE TABLE</h3>
<p>- To create database and its objects like (table, index, views, store procedure, function and triggers)</p>

#### Primary Key

The PRIMARY KEY constraint uniquely identifies each record in a table.

#### Costumers table

```sql
CREATE TABLE tb_customers(
  id_customer INTEGER,
  first_name  VARCHAR2(30) NOT NULL,
  last_name   VARCHAR2(30) NOT NULL,
  email       VARCHAR2(40) NOT NULL,
  phone       VARCHAR2(12) NOT NULL,
  is_active   INTEGER,
  CONSTRAINT pk_customer PRIMARY KEY(id_customer)
);
```
#### Products categories table

```sql
CREATE TABLE tb_prod_categories(
  id_category    INTEGER,
  category_name  VARCHAR2(20) NOT NULL,
  is_active      INTEGER,
  CONSTRAINT pk_category PRIMARY KEY(id_category)
);
```

#### FOREIGN KEY

The FOREIGN KEY constraint is a key used to link two tables together.

#### Products table

```sql
CREATE TABLE tb_products(
  id_product        INTEGER,
  id_prod_category  INTEGER,
  product_name      VARCHAR2(30) NOT NULL,
  product_descr     VARCHAR2(140),
  price             NUMBER(5,2) NOT NULL,
  is_active         INTEGER,
  CONSTRAINT pk_product PRIMARY KEY(id_product),
  CONSTRAINT fk_prod_category FOREIGN KEY(id_prod_category) REFERENCES tb_prod_categories(id_category)
);
```

#### Sales table

```sql
CREATE TABLE tb_sales(
  id_product    INTEGER,
  id_customer   INTEGER,
  quantity      INTEGER,
  is_active     INTEGER,
  CONSTRAINT fk_product FOREIGN KEY(id_product) REFERENCES tb_products(id_product),
  CONSTRAINT fk_customer FOREIGN KEY(id_customer) REFERENCES tb_customer(id_customer),
  CONSTRAINT pk_sales PRIMARY KEY (id_product, id_customer)
);
```

## DML - Data Manipulation Language

<h3>SELECT</h3>
<p>- Retrieve data from the a database</p>

```sql
/*Returns all registers on the table*/
SELECT *
FROM table_name
```

<h3>DESCRIBE</h3>
<p>- Command to describe the structure of a table</p>

```sql
DESCRIBE table_name
```

<h3>INSERT</h3>
<p>- Add data into a table</p>
<p>- The order in <b>VALUES</b> corresponds to the order in which the table columns are</p>

```sql
INSERT INTO table_name (column1, column2, column3, ... columnN)
VALUES (value1, value2, value3, ... valueN);
```


## TCL - Transaction Control Language 

<h3>COMMIT</h3>
<p>- Makes the operations permanent</p>

<h3>ROLLBACK</h3>
<p>- Undo operations</p>
