1. To have a visual look at our database, we will use [TablePlus](https://tableplus.com/).

2. Go through the installation process for TablePlus.

3. In TablePlus, we need to make a connection with our PostgreSQL database. At the bottom of the TablePlus window, click on `Create a new connection...`.

4. Choose `PostgreSQL`, and click `Create`.

5. Give your connection a name. We'll call ours `TodoList`.

6. The host is always `localhost`, and port is by default always `5432`.

7. Enter the User name and password that're the same as in your `config.json` file.

8. Enter the name of the database, and click `Connect`.

9. Tada! You can view your database in this beautiful crisp TablePlus UI!

10. Open the `Todo` table and viola! This is our model! But there are extra fields that we didn't define!

    Where did all those extra fields come from? So, sequelize automatically generates a **unique ID** field called `id`, a **`createdAt`** and an **`updatedAt`** fields. How cool is that? **Mind blown**

11. Let's create a row by clicking the **+ Row** button. Fill your fields and save (CMD/CTRL + S).

At this point, we wrote all our **CRUD methods** manually by accessing the data from our data file directly. But now we have **Sequelize** to take care of that. **Sequelize** _provides an endless number of methods to communicate with the database_. Let's use them to access our bright new database!

All the methods we're using are from the [documentation](https://sequelize.org/master/manual/model-querying-basics.html#simple-update-queries). So make sure to take a look at it.
