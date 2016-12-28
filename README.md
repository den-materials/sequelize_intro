<!--9:45 5 minutes -->

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

<!--9:50 10 minutes -->

### Initial setup

Set up an npm project with a functioning `server.js`, using `express`, listening on port 3000, with a `'/'` `get` route that `send`s text like "Hello Sequelize" in its response.

Once this is all set up, you will need to create a PostgreSQL database.  To do this, enter the `psql` terminal, then run the following command:

`CREATE DATABASE test_sequelize;`

<!--10:00 5 minutes -->

### Sequelize setup

Install `sequelize` with `npm` and `--save` it to your `package.json`.

Do the same with `pg` and `pg-hstore`.

Require `sequelize` into a variable called `Sequelize` (notice the capitalization--what kind of function do you think `Sequelize` is?).

<!--10:05 5 minutes -->

### Connecting with Sequelize

Create a new `Sequelize` connection like the one below, but **replace the \<localusername\> with your local Mac username**.  (**Hint:** what username is in your Terminal?)

```js
var sequelize = new Sequelize('postgres://<localusername>@localhost:5432/test_sequelize');
```

`console.log` this connection variable to see what we're working with.  A little daunting, right?  Well, for now the `options` object at the top tells us some helpful information.  Our `dialect` is `postgres`, the dialect we've been using in all our SQL labs.  Our `host` is `localhost` (our PC).  And our `port` is 5432 (the `postgres` port).

<!-- 10:10 15 minutes -->

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

### Getting that user back, I *promise*

#### Promises

Sequelize uses promises to control async control-flow, the same way we saw with Angular.  This means that you will need to use `then` or something similar to do something when your SQL DB returns the information to your JS.  Otherwise, your code may run before the result gets back.

#### Our code

So if we want to find our user, we will run the following:

```js
User.findOne().then(function (user) {
    console.log(user.get('name'));
});
```

Look familar?

<!--Basically the same way we accessed DB with Mongoose except we're using a promise instead of a callback-->

<!--10:25 5 minutes -->

### Challenge

Replace your "Hello Sequelize" response in your `'/'` route with a string including your name and your favorite saying.

**Bonus:** Can you send it as JSON or HTML?

<!--10:30 5 minutes -->

### Closing thoughts

Congratulations! You have set up your first database connection with Sequelize and Node.  Notice how similar this all is to Mongoose, and rely on the documentation below if you get stuck.

#### Questions

- What is Sequelize?
- Can you name two differences in the code between Mongoose and Sequelize?
<!--Examples include Mongoose we used callbacks, Sequelize uses promises, there aren't really any schemas, we use .define instead of new schema, we have to create the DB in psql and the table with .sync() (booo) -->

## Resources

- [Sequelize Docs](http://docs.sequelizejs.com/en/v3/)
