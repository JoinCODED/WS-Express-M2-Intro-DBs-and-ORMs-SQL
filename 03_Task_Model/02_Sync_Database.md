1.  Next, we need to sync our database so that any models we create, or any changes we make on our models, are applied to the database.

2.  In your `app.js`, change `db.sequelize.authenticate()` to the following:

        ```javascript
        try {
            await db.sequelize.sync();
            // ...
        }
        ```

3.  Now our model is registered in our database!
