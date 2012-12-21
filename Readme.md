MssqlBundle
------------

This bundle implements a pdo_dblib based Microsft SQL Server. The original bundle was forked from https://github.com/intellectsoft-uk/MssqlBundle.

Symfony Install
---------------

Add the **trooney/mssql-bundle** into **composer.json**

    "require": {
        ....
        "trooney/mssql-bundle": "master-dev"
    },

Symfony Configuration
------------------

Update the doctrine section of your **config.yml** to include the option **driver_class**

    doctrine:
        dbal:
            driver:         %database_driver%
            driver_class:   \NRC\MssqlBundle\Driver\PDODblib\Driver


FreeTDS Configuration
=====================

DBLib requires FreeTDS. Your **freetds.conf** connection configured should look something like following:

```
[mssql_freetds]
    host = 172.30.252.25
    port = 1433
    tds version = 8.0
    client charset = UTF-8
    text size = 20971520

```


Putting everything together
===========================

Getting everything together wasn't easy. You need to complete the following steps, checking each installation is successful by connecting with the appropriate tools:

* Install FreeTDS and configure a server connection
    * *Verify* with ./tsql -S mssql_freetds -U yourusername -P yourpassword
* Install the PHP DBLib extension -- verify with PHP script containing
    * *Verify* $pdo = new PDO('dblib:host=mssql_freetds;dbname=yourdb', 'yourusername', 'yourpassword');
* Install and configure the PDODblibBundle
    * *Verify* Some kind of SQL against your database


Notes
=====

- This driver requires FreeTDS version 8.0 (from http://www.ubuntitis.com/?p=64)
- You cannot use nvarchar
