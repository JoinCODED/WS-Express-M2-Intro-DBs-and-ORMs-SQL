Every project you're working on must have its own database.

1. In **any place in your terminal**, write the following command:

   ```shell
     $ createdb mydatabase_db -U username
   ```

2. Replace `mydatabase_db` with the database's name. Choose a suitable name for your project.

3. Replace `username` with the name of your macbook's username.

   When running this command, nothing will happen. So how can we know that the database is created?

4. Run the following command anywhere in your terminal to see the list of your databases:

   ```shell
     $ psql -l
   ```

Congrats! You created your first database!
