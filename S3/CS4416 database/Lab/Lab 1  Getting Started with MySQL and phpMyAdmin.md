# Lab Exercise: Getting Started with MySQL and phpMyAdmin

In the Database Systems labs, you will work with the MySQL database management system. MySQL runs as server software that allows client applications to create and manipulate multiple databases. Client applications use the standard SQL language to request MySQL database management system services. A single instance of MySQL can act as a server for multiple (typically a large number) users/apps and databases.

In the CSIS labs, you will use the web app phpMyAdmin to access the CSIS MySQL database management system as a database administrator. phpMyAdmin is only one of the many client applications you can use to access a MySQL database management system.

#### In this lab exercise, you will:

learn how to login to the CSIS MySQL database management system via the phpMyAdmin web app,
familiarise yourself with the user interface of phpMyAdmin,
learn how to import a database from a text file and how to export a database to a text file.
Tasks
1. Download the file pcshop.sql.

2. Open the MySQL login page at http://testweb3.csis.ul.ie/phpmyadmin.

Note: testweb3.csis.ul.ie is the machine that runs the CSIS MySQL database management system.

The server testweb3.csis.ul.ie is accessible only from the cable network in the CSIS building. To work on your own computer you need to install MySQL. We recommend that you download XAMPP from https://www.apachefriends.org/ and install it on your own computer in order to work in the same environment as in the CSIS labs. Watch the video below for help with installing XAMPP. When working with XAMPP you must first create a database before importing the file pcshop.sql into it.

3. Log in to MySQL with the following credentials:

username: cXXXXXXXX where XXXXXXXX is your ID number
password: cXXXXXXXX where XXXXXXXX is your ID number

4. Change your password (under General settings). Please do not use a secure password that you use elsewhere. This server is only a sandbox to practice SQL.

5. Each account has a single database associated with it. On this server, you don’t have permission to create multiple databases. The name of your database is the same as your username. 

Find your database in the list of databases on the left-hand side of the screen and click on it. Any tables that you may want to create will be stored in your single database.
Pay attention to the navigation bar at the top of the page. It tells you what the context of any operation you are performing is.
6. With the name of your database appearing in the navigation bar, click on the Import button and import pcshop.sql. Note that pcshop.sql is a text file that contains a list of SQL statements. You can also open and look at its content with a text editor (e.g. Notepad).

7. Practice using the web interface to insert more data into the tables and modify the existing data.

8. Click on the name of your database in the navigation bar on top and then use the menu to export your database to an SQL file. Throughout the semester, remember to export your database to a file after you have made essential changes to it so that you have a backup copy. You can also use the export/import functionality to continue working at home, export your database from the CSIS lab and import it on your computer, and vice-versa.

9. Note that phpMyAdmin is a web application that is one of the many available clients for a MySQL database server. An alternative client, for example, is the Windows application HeidiSQL. As an exercise:

Download the portable version of HeidiSQL from http://www.heidisql.com/download.php.
Unzip HeidiSQL and run it on a lab PC.
Use HeidiSQL to connect to testweb3.csis.ul.ie. You should be able to see your database with the tables you have imported.
