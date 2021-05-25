# SQL Training with Pagila Database and PostgreSQL DBMS
Tutorials, Data and Questions sets allowing you to download PostgreSQL and The Pagila Database for the purpose of real-world SQL simulation. In this repository you can find info to help you create an Entity Relationship Diagram (ERD) and question sets to help you train on the Pagila Dataset. 

______
# Simulating A Real-world SQL Environment
_______
**You can find this tutorial at [Simulating A Real-world SQL Environment](https://medium.com/p/63784f7f37ae/edit) This read-me is lacking the photos that the article contains**

A tutorial using PostgreSQL, pgAdmin 4 and the Pagila Dataset. 
Postgres is an open-source project under a liberal Open Source license. You can find the PostgreSQL licence here

---

### The following tutorial will walk you through the following tasks:

**1.** Download PostgreSQL and pgAdmin 4 to your own PC or environment.

**2.** Connect to PostgreSQL server

**3.** Download and load the Pagila database set (based on the famous Sakila training database).

**4.** Provide resources and a link to a Github repository detailing these steps. The data and the question sets will be included. 

---
### Reasoning Behind This Tutorial and Repository

As I quickly worked through many different methods for teaching myself SQL I began to notice that very few of them truly embody the real-world feel of using the database querying language in the wild. I also felt a longing to understand the deeper relationships between SQL and whichever database management system (DBMS) it was being used in. This lead me to the thought that certainly there is a dataset out there somewhere that will allow me to create a real-world environment to practice in. To my joy, there was. Sakila was created to train people in MySQL and shortly afterward Pagila was created to train new users in PostgreSQL. I will go over later where I found and how I used the Pagila data. You can also find a link to it under the movie film image below. 

The Pagila Database is a copy of the Sakila database and is designed more specifically for Postgre SQL learning. You can find the version of the database that I used here: Pagila Database by Devrim Gündüz. There is another Github repository that may also be helpful found here: Pagila by Robert Treat. The Pagila Database is a simulated set of tables that would mimic the operations and data of a chain of video stores. Think of Blockbuster Video circa 1990's. At first glance the use case of a video store may not seem very relevant in a post-Blockbuster world yet I assure you that this dataset still does relatively well mimicking many retail environments or environments where there is revenue, customers, and products. 

---

# 1. Let's Get Started: Downloading PostgreSQL
Download PostgreSQLI downloaded the Mac installer from EDB for PostgreSQL Version 13.3 here: PostgreSQL 13.3 from EDBDownload PostgreSQL . You can do this a number of ways (all of which are featured in the link). I chose to use the interactive installer by EDB but there may be some options that are easier and in fact better. If I took the time to do this all over again I would likely choose the postgres.app instead. The postgres.app install not only allows for a simple download and install but may even have a more intuitive GUI than pgAdmin 4. nonetheless, pgAdmin works just fine and if you're into command line usage I believe all of these implementations also allow SQL on CLI. 
I'm using Mac so I downloaded the installer from EDB. Installer will save an image to your computer that will open up a folder. 
Click on the folder and an installer will pop up. Follow the prompts. 

You can see the You can see the PostgreSQL 13.2–2 image file in the top left of this pic. Click on that box with the arrow going right and then the PostgreSQL 13.2–2 app image (bottom-left of pic) will pop up. Click on that disk-drive looking file and the installer will open up. Follow the prompts on the setup wizard. Click "Next". During the installation a prompt will come up asking you to select your locale. This is where you set up cultural preferences including language. It is important to select the right locale. If you're in the U.S. for instance you will select en_US.UTF-8.
It is important that you select the right locale here. If in United States then select the one pictured above. The installer will then show you a summary of your install configurations.

Pre-install summary. Your configurations should look fairly similar. Click Next to install.

---

# 2. Setting up Postgre SQL Server
There is a really nice tutorial walking you through Postgre SQL Server setup located here: Connect to a PostgreSQL Server Database. OR you can follow my quick and less thorough instructions below. 
Two Ways to Connect on Mac (App-based or Terminal-based)

Terminal Based Server Connection (Using psql)
One way to connect, especially if you love using command line, is to use the psql SQL shell. 
For terminal based you will need to open up the psql app that should have been downloaded as part of the PostgreSQL package in the previous steps. This will open up a SQL Shell. On mac I just type "psql" in the search bar or you can go to the application folder and find it there. 
Then you will enter Server name, Database name, Port, your username and your password. You can also press the Enter key and default values will be filled in. The default values are displayed in brackets next to each prompt. 
Lastly, you can interact directly with the PostgreSQL Database Server by writing a SQL statement. The below statement shows all of your databases in PostgreSQL. There is usually just a template database in there to start. 

\l 
Application Based Server Connection (Using pgAdmin 4)
You can also use pgAdmin 4 web-app. This allows you to connect and interact with PostgreSQL database server via a user-friendly GUI. 
Launch the pgAdmin application. Again, I just used the search bar in my mac but you can also find it via command line and in the applications folder. 
One tutorial I had seen said that pgAdmin will open in a web-browser but when I opened it pgAdmin actually opened in its own app on the Mac dock. 

When you launch pgAdmin it will open in its own application window on Mac. It will look something like this.  3. Right click on "Servers." and select Create > Server
This will create a server in pgAdmin 44. Enter server name (whatever you want it to be)
I used "test_postgreSQL" as my server name. After this step click the "Connection" tab up top. 5. Click the connection tab and enter host and password. This is the username and password you created in the PostgreSQL installation process. 
This will be the username and password you created in the PostgreSQL installation process. 6. Expand the servers cluster and then the databases node and you will see a default database called postgres already installed. Ignore the Pagila database in the image below. I had already downloaded it so it shows an unconnected database there. 
Ignore the pagila database here. I already had it installed at time of pic. Once you've navigated to the desired database you can click on it and then click on the query tool. You can do this two ways. Clicking on the "Tools" drop down and then the "Query Tool" option or by clicking on the icon that looks like databases with a "play" logo. 
diagram describing how to access and use the query tool7. Enter a query into the editor and click the execute button 
Click execute button to run query. Result will output below in the Data Output field. 

---

# 3. Download and Load The Pagila Database
There are two good githubs that I found which house the Pagila Database. I used the Pagila Database by Devrim Gündüz. It was the first one I found that had the database and clear instructions on what it was and how it works. If you are into using containerized environments he also has a tutorial for implementing the database in Docker. In this process I am assuming you already have a github account and know how to use git. If you do not then you can create a github account here and familiarize yourself with github tutorials. 
Fork Repository
copy the https or ssh link from the repository to clone it 
This will create a forked copy of this repository into your own github repository. It will also navigate the page to your new forked repository. Clone Repository
You can see in the image that the repository address in the top left of the screen is now my repository. From your forked repository you will clone the repository down to your PC. Click on code and copy the https or SSH url. 
Copy the url from the code button. You will insert this into the command line to create a local repository on your own computer. Start a new command line terminal. You can do this by typing terminal in the search bar on Mac or In the Finder you can open the /Applications/Utilities folder, then double-click Terminal.
FinderOnce terminal is open you can navigate over to the folder/directory where you would like to store the Pagila directory. Learn how to navigate through command line here: Navigate Through Command Line. You will then copy the link into the command line within the desired directory and a new directory will be created that houses all of the pagila database files that were housed in github. 
I chose to save my directory into a folder/directory that I call projects. The ```ls``` command lists out all the files in my new Pagila directory. At this point you will now have a Pagila directory that houses the Pagila databases on your own computer. We will not pull the Pagila files into PostgreSQL server using pgAdmin 4. Before doing this I strongly recommend reading the README.md file in Devrim Gündüz's Pagila github repository. 
Create a New Database in pgAdmin 4
Right click on "Databases", click "Create" and then "Database". Name your database, I named mine "test_pagila." Click on the save button. At this point a new database should show up under the Databases heading in the left broswer. Click on the new database (in my case it is test_pagila), then click on the query tool, go into the new query editor and find the file icon in the top left of the editor and then click on that to search for your Pagila SQL files. 
These are the steps you will take to find your Pagila SQL files. Choose the pagila-insert-data.sql file and click selectThe schema and data for the database will autofill into the query editor. Click the run icon and you should see a message that says "ALTER TABLE" below in the Data Ouput box. Now your database has been created. You can run queries and use this for whatever purposes you now desire. Happy querying. 

# 4. Resources for Using Pagila
There are many ways to train with The Pagila Database. You can spin up your own queries and use it any way you would use a real-world database or you can use question sets that quiz you on your abilities while using realistic data and data-structures. 
I have also scoured the internet to find all kinds of questions (with solutions in most cases) pertaining to Pagila and Sakila and compiled them into a group of Jupyter Notebooks. You can use these questions to test your abilities as well. Find them here:
I also created an Entity Relationship Diagram (ERD) using Pagila. You can find my tutorial for this here: Creating a SQL Entity Relationship Diagram (ERD) and the actual ERD image for your reference below: 

### I garnered much of my information to perform this task from these sites:

* [Devrim Gündüz Github](https://github.com/xzilla/pagila) Devrim is a major contributor to PostgreSQL. This is the database file I used in this tutorial. 

* [The Pagila Project Page on Github](https://github.com/xzilla/pagila) I found this one after I already started creating this tutorial but this is possibly the creator of Pagila. I'm not sure. But the creator of this project seems to be a major open-source contributor to a variety of projects. 

* [Connect to a PostgreSQL Database](https://www.postgresqltutorial.com/connect-to-postgresql-database/) This is the resource I used to connect to the PostgreSQL database. This site [Postgresqltutorial.com](www.postgresqltutorial.com) is also a helpful resource for other PostgreSQL information.
 
* [PostgresSQL Official Site](https://www.postgresql.org/download/) This is where I downloaded PostgresSQL.

* [Getting Started with PostgreSQL using Amazon RDS, CloudFormation, pgAdmin, and Python](https://programmaticponderings.com/2019/08/09/getting-started-with-postgresql-using-amazon-rds-cloudformation-pgadmin-and-python/) This is a resource I didn't use but something I want to use at some point. This tutorial combines PostgreSQL with Amazon AWS services to create a dual purpose learning experience.
