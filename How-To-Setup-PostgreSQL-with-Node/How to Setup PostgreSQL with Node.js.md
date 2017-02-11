# How to Setup PostgreSQL with Node.js

## Introduction

Ever wanted to add a PostgreSQL database to the backend of your web application? If so, by the end of this tutorial you should have a PostgreSQL database up and running with your Node.js web application. PostgreSQL is a popular open source relational database.  This tutorial assumes you have Node and NPM installed on your machine, if you need help installing that check [this][nodeInstall] out. First let's download PostgreSQL.

## PostgreSQL

### Install

I am writing and testing this tutorial on a mac, so it will primarily be catered towards that, but I will include links down in the Reference section for downloading PostgreSQL on select Linux distributions and Windows as well.

If you are on a Mac however you can follow these steps.  
First, you must have Homebrew.  If you do not have it you may install following the directions [here][homebrewInstall]. Once Homebrew is installed and working, you can do the following:

```
$ brew update
$ brew install postgres
```
This downloads and installs PostgreSQL for you.

### Command Line Setup

Now, open a new instance of terminal, by pressing `command+t`.  Once you have the new tab you can start a PostgreSQL server with the command: 
`postgres -D /usr/local/var/postgres`.  This allows you to use Postgres locally and gives you a logger for all the commands you run on your databases. 


Next open a new instance of terminal with `command+t` and enter: 
`$ createdb`
This creates a database.  This is only needed to be done on the first time you are using PostgreSQL. Then enter:
`$ psql`

This is similar to a command center for Postgres.  It
allows you to create things in your database, and plenty more.  You can manually enter commands here to set up your environment.  

For this example, we are going to be creating a database called *example*. To do that, while in the terminal tab with *psql* running enter 
`CREATE DATABASE example;`
To confirm that the database was made you should see:
`CREATE DATABASE` as the output.  Also to list all databases you would use: `\l`.  Then we will want to connect to our new database with the command `\connect example`.  This should give you a a message telling you connected: `You are connected to database "example" as user`.  

In order to store things in this database we need to create a table.  Enter:

 ```
 CREATE TABLE numbers(
  age integer
  );
 ```
  So this format is probably confusing if you have never seen it before.  This is telling Postgres to create a table in this database called *numbers*, with one column called *age* and all items in column age are going to be of the data type *integer*. Now this should give us the output of `CREATE TABLE` but if you wanted to list all tables in a database you would use `\dt` command.
  
Now for sake of this example we are going to add a row to the table so we have some data to play with and prove this works.  When you want to add something to a database in PostgreSQL you use the INSERT command.  Enter this command to have the first row in the table equal to *732*: `INSERT INTO numbers VALUES (732);`.  This should give you an output of `INSERT 0 1`. To check the contents of the table, simply type: `TABLE numbers;`.

Now that we have a database up and running with a table with a value we can setup our code to access this table and pull the value from it.

## Code

### Setup

In order to follow this example, you will need to make sure you have the following packages: pg, pg-format, and express. Enter the project directory you plan on working in (and where you have node and npm installed).

For pg: `npm install -pg`
This is a Postgres client for node.

For pg-format: `npm install pg-format`
This allows us to safely make dynamic SQL queries.

For express: `npm install express --save`
This allows us to create a quick and basic server.

Now that those packages are installed we can code!

### Actual Code
 Let's create a file called `app.js` for this as the main point in our program. At the top establish your variables:
 
```
const express = require('express')
const app = express()
var pg = require('pg')
var format = require('pg-format')
var PGUSER = 'yourUserName'
var PGDATABASE = 'example'
var age = 732
```

The first two lines allow us to use the package `express` and help us make our server.  The next two lines allow us to use the packages `pg` and `pg-format`.  *PGUSER* is a variable that holds the user to your database. Please enter your user name here in place of *'yourUserName'*.  *PGDATABASE* is a variable to hold the database name we will like to connect to.  Then the last variable is to hold the number that we stored in the database.  Next add this:

```
var config = {
  user: PGUSER, // name of the user account
  database: PGDATABASE, // name of the database
  max: 10, // max number of clients in the pool
  idleTimeoutMillis: 30000 // how long a client is allowed to remain idle before being closed
}

var pool = new pg.Pool(config)
var myClient
```
Here, we are establishing a *config* object that allows *pg* to know that we want to connect to the database specified as the user specified, with a maximum of 10 clients in a pool of clients with a time out of 30000 milliseconds of how long a client can be idle before disconnected from the database.  Then we are creating a new pool of clients according to that config file.  Afterwards we are creating a variable called *myClient* to store the client we get from the database in the next step.  Now enter the last bit of code here:

```
pool.connect(function (err, client, done) {
  if (err) console.log(err)
  app.listen(3000, function () {
    console.log('listening on 3000')
  })
  myClient = client
  var ageQuery = format('SELECT * from numbers WHERE age = %L', age)
  myClient.query(ageQuery, function (err, result) {
    if (err) {
      console.log(err)
    }
    console.log(result.rows[0])
  })
})
```

This tries to connect to the database with one of the clients from the pool.  If a client successfully connects to the database, we start our server by listening on a port (here I use 3000). Then we get access to our client. Then we create a variable called *ageQuery* to make a dynamic SQL query.  A query is command to a database. Here we are making a **SELECT** query to the database checking all rows in the table called *numbers* where the *age* column is equal to *732*.  If that is a successful query (meaning it finds a row with 732 as the value) then we will log the answer.

Time to test all your hard work!  Save the file, and run the command in terminal:

`node app.js`

Your output should look like:

```
listening on 3000
{ age: 732 }
```

## Conclusion 

There you go! You now have a PostgreSQL database connected to your web app ! To summarize our work, here is a quick breakdown of what happened:

1. We installed PostgreSQL through Homebrew
2. We started our Local PostgreSQL server
3. Opened `psql` in terminal to use commands manually
4. Created a database called `example`
5. Created a table in that database called `numbers` 
6. Added a value to that table
7. Installed `pg`, `pg-format`, and `express`
8. Used Express to Create a Server
9. Created a Pool of Clients using a config object to access the database
10. Queried the table in the database for 732
11. Logged the Value

If you enjoyed this post share it on [twitter][twit]. Check out the code for this tutorial on [GitHub][gitRepo]. 

## Possible Resources

Check out my [GitHub][mainGit]

View my personal [blog][pblog]

Windows Install [Postgres][winInstall]

Linux Install [Postgres][linInstall]

Check out [Express.js][expressjs]

More on PostgreSQL node packages [node-postgres][pg] and [postgres format][pgform]

[nodeInstall]:  https://nodejs.org/en/download/
[homebrewInstall]: http://www.howtogeek.com/211541/homebrew-for-os-x-easily-installs-desktop-apps-and-terminal-utilities/
[twit]: https://twitter.com/
[gitRepo]: https://github.com/acucciniello/setup-postgres
[mainGit]: https://github.com/acucciniello/
[winInstall]: https://www.postgresql.org/download/windows/
[linInstall]: https://www.postgresql.org/download/linux/
[expressjs]: http://expressjs.com/
[pg]: https://github.com/brianc/node-postgres
[pgform]: https://github.com/datalanche/node-pg-format
[pblog]: http://www.acucciniello.com/