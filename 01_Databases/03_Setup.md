Let's start with installing Postgresql for **Mac Users**.

1. For Mac users, you can use `brew` to install it.

   ```shell
     $ brew install postgresql
   ```

2. After that we will start the postgres server:

   ```shell
     $ brew services start postgresql
   ```

Your Postgres username is your device's username, and there is no password for it.

---

Let's start with installing for **Windows Users**.

1. For Windows users, download the latest version of [Postgresql](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads).

2. Run the installer you downloaded and follow all the instructions.

3. Keep on clicking `Next` until it asks you for a password.

4. The installer will ask for a password. Basically it's creating a user for the database. The default username is `postgres`. Make sure to write an easy password and write it somewhere, you might need it later! Don't use a personal password, we will all see this password when we check your code, lol.
