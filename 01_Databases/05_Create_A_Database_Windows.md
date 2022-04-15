Every project you're working on must have its own database.

When installing Postgrs, an **SQLShell** is installed.

1. Open SQLShell (Search for it).

2. It will ask you for a few things, choose the default (Press Enter four times), then enter your Postgres password.

3. Write the following command:

   ```shell
     CREATE DATABASE mydatabase_db;
   ```

4. Replace `mydatabase_db` with the database's name. Choose a suitable name for your project.

   When running this command, nothing will happen. So how can we know that the database is created?

5. Run the following command anywhere in your terminal to see the list of your databases:

   ```shell
     \l
   ```

   Congrats! You created your first database!
