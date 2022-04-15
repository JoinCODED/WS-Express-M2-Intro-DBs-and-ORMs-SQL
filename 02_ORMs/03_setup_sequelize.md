There are many ways for the database to connect to the app, we will be using an **ORM** stands for Object-Relational Mapping, and it handles the movement of data between your application and the database.

The ORM we will be using is called Sequelize.

To read more about ORMs and Sequelize, [click here](https://warehouse.joincoded.com/workshops/express-encyclopedia/orms-and-sequelize/what-is-an-orm).

1. Back to our Express application, install the following:

   ```shell
   npm install sequelize sequelize-cli pg pg-hstore
   ```

   We will be using Sequelize CLI to initialize Sequelize. It's a special piece of software that's used to aid in the development process.

2. In your Express application, create a folder for all files related to the database called `db`. `cd` inside this folder.

   ```shell
   mkdir db
   cd db
   ```

3. To create all the files we need from Sequelize, we will run the following command.

   ```shell
   npx sequelize init
   ```

   This will initializes the configuration code, folders and helpers needed for the application. It sets up four directories: **config**, **migrations**, **models**, and **seeders**.

   Sequelize CLI does the configuration for us, we don't need to do it.

4. Open the `config.json` in `config`. You'll see three objects, one for your development mode database, one for testing and one for production mode. For now, we will only connect our app to the development mode database, which is the database we created.

5. Change the fields in the `development` object to the following parameters:

```javascript
"development": {
    "username": "postgres",
    "password": "a_super_cool_password",
    "database": "database_name",
    "host": "127.0.0.1",
    "dialect": "postgres"
  },
```

The `username` and `password` are the ones we created when installing Postgres, `database` is the name of the database we just created and `dialect` is the type of database we're using which is Postgres. Our database instance is ready!

6. Now we will connect the database to the app and test the connection. In `app.js` require the `db` object, which is created in the `models`'s `index.js`:

   ```javascript
   const db = require('./db/models');
   ```

7. To test the connection, we will use the `authenticate` method from `sequelize`. But since this method is asynchronous, we will save it in a function to use `async await`, then call it. Replace your `app.listen` with the following code:

   ```javascript
   const run = async () => {
     try {
       await db.sequelize.authenticate();
       console.log('Connection to the database successful!');
       await app.listen(8000, () => {
         console.log('The application is running on localhost:8000');
       });
     } catch (error) {
       console.error('Error connecting to the database: ', error);
     }
   };

   run();
   ```

8. If you get the `Connection to the database successful!` message, then you're ready to move to the next step.
