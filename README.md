<!--Actually 9:02 WDI2-->
<!--9:06 WDI3 -->
<!--9:05 5 minutes -->
<!-- WDI6 9:00 -->

# Sequelize

<!--Hook: Think back to Mongoose for a second.  What did we use it for?  Well, as you may have noticed, this whole week we've been using SQL, not MongoDB.  Because of that, we'll need a new tool to set up our models.  Enter Sequelize. -->

## Objectives

*By the end of this lesson, developers will be able to:*

- **Include** Sequelize in a Node application
- **Use** Sequelize to create a SQL relation

## Introduction

### What is Sequelize?

>**From the docs:** Sequelize is a promise-based ORM (object-relational mapping) for Node.js and io.js. It supports the dialects PostgreSQL, MySQL, MariaDB, SQLite and MSSQL and features solid transaction support, relations, read replication and more.

In other words, in the same way that Mongoose was the glue holding Mongo and JS together, Sequelize is the glue holding SQL and JS together.

## Our first Sequelize project

>**Note:** We will only be working in `server.js` throughout this lesson.  We can worry about file organization later.

<!-- Catch-up -->

<!--Actually 9:07 WDI2 when turning over to devs -->

<!--9:09 WDI3 -->
<!--9:10 10 minutes -->

### Initial setup

Set up an npm project with a functioning `server.js`, using `express`, listening on port 3000, with a `'/'` `get` route that `send`s text like "Hello Sequelize" in its response.

Once this is all set up, you will need to create a PostgreSQL database.  To do this, enter the `psql` terminal, then run the following command:

`CREATE DATABASE test_sequelize;`

<!--9:20 WDI3 -->
<!--9:20 5 minutes -->
<!-- WDI6 9:16 -->
### Sequelize setup

Install `sequelize` with `npm` and `--save` it to your `package.json`.

Do the same with `pg` and `pg-hstore`.

Require `sequelize` into a variable called `Sequelize` (notice the capitalization--what kind of function do you think `Sequelize` is?).

<!--Actually 9:33 when finished setup -->

<!--9:26 WDI3 -->
<!--9:25 5 minutes -->

### Connecting with Sequelize

Create a new `Sequelize` connection like the one below, but **replace the \<localusername\> with your local Mac username**.  (**Hint:** what username is in your Terminal?)

```js
var sequelize = new Sequelize('postgres://<localusername>@localhost:5432/test_sequelize');
```

`console.log` this connection variable to see what we're working with.  A little daunting, right?  Well, for now the `options` object at the top tells us some helpful information.  Our `dialect` is `postgres`, the dialect we've been using in all our SQL labs.  Our `host` is `localhost` (our PC).  And our `port` is 5432 (the `postgres` port).

<!--9:34 WDI3 -->
<!-- 9:30 20 minutes -->
<!-- WDI6 9:26 -->
### Our first model

We're going to need to make our mark on the world, so let's save our name and our favorite saying so everyone knows we were here.  That would look like this:

```js
var User = sequelize.define('user', {
  name: {
    type: Sequelize.STRING
  },
  saying: {
    type: Sequelize.STRING
  }
});
```

Look familiar?

<!--Basically like a schema in Mongoose -->
<!--9:43 WDI3 -->

### Our first user

```js
User.sync({force: true}).then(function () {
  // Table created
  return User.create({
    name: 'Zeb',
    saying: 'Everything is basically 0s and 1s'
  });
});
```

Look familar?

<!--Almost exactly the same way we would seed our DB with Mongoose -->

>Note: Rerunning the server now may throw an error like `Unhandled rejection SequelizeDatabaseError: relation "users" does not exist`.  This is expected, and should not affect your ability to complete the rest of the lab.
<!-- WDI6 9:40 -->

### Getting that user back, I *promise*

#### Promises

Sequelize uses promises to control async control-flow, the same way we saw with Angular.  This means that you will need to use `then` or something similar to do something when your SQL DB returns the information to your JS.  Otherwise, your code may run before the result gets back.

#### Our code

So if we want to find our user, we will run the following inside of our route:

```js
User.findOne().then(function (user) {
    console.log(user.name);
});
```

Look familar?

<!--Basically the same way we accessed DB with Mongoose except we're using a promise instead of a callback-->

<!--Actually 9:59 when introing challenge WDI2 -->

<!--9:50 5 minutes -->

### Challenge

<!--9:53 turning over to devs WDI3 -->

Replace your "Hello Sequelize" response in your `'/'` route with a string including your name and your favorite saying.

**Bonus:** Can you send it as JSON or HTML?

<!--10:00 WDI3 -->
<!--9:50 5 minutes -->
<!-- 10:05 WDI6 -->

### Closing thoughts

Congratulations! You have set up your first database connection with Sequelize and Node.  Notice how similar this all is to Mongoose, and rely on the documentation below if you get stuck.

#### Questions

- What is Sequelize?
- Can you name two differences in the code between Mongoose and Sequelize?
<!--Examples include Mongoose we used callbacks, Sequelize uses promises, there aren't really any schemas, we use .define instead of new schema, we have to create the DB in psql and the table with .sync() (booo) -->

<!--10:04 WDI3 -->
<!--Actually 10:15 WDI2-->

## Resources

- [Sequelize Docs](http://docs.sequelizejs.com/en/v3/)
- [More about sync](http://sequelize.readthedocs.io/en/latest/api/sequelize/#sync)
