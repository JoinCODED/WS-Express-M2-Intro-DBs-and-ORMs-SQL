1. Create a file in your `models` folder called `Task.js`. Make sure it's **singular** and starts with **a capital letter!**

2. In this file we will start with creating a function called `TaskModel` that takes two arguments, `sequelize` which is our database from `models/index` and `DataTypes`.

   ```javascript
   const TaskModel = (sequelize, DataTypes) => {};
   ```

3. Inside this function, we will **define** our **model**, using `sequelize`'s `define` function. This function takes two arguments, the name of the model and an object where we will define the model's fields. Then we will save the return value in a variable called `Task`.

   ```javascript
   const TaskModel = (sequelize, DataTypes) => {
     const Task = sequelize.define('Task', {});
   };
   ```

4. Next we will define the fields of this model. The fields represent the columns in the database. We will add four fields to our model, `task`, and `done`. Don't forget to return `Task`.

   ```javascript
   const TaskModel = (sequelize, DataTypes) => {
     const Task = sequelize.define('Task', {
       task: {
         type: DataTypes.STRING,
       },
       done: {
         type: DataTypes.BOOLEAN,
       },
     });
     return Task;
   };
   ```

5. One more thing! **Don't forget to export TaskModel!**

   ```javascript
   module.exports = Task;
   ```

6. We can clean this up by directly exporting the return value of the function:

   ```javascript
   module.exports = (sequelize, DataTypes) => {
     const Task = sequelize.define('Task', {
       task: {
         type: DataTypes.STRING,
       },
       done: {
         type: DataTypes.BOOLEAN,
       },
     });
     return Task;
   };
   ```

7. We can clean it up even more by directly `return`ing the model:

   ```javascript
   module.exports = (sequelize, DataTypes) => {
     return sequelize.define("Task", {...});
   };
   ```
