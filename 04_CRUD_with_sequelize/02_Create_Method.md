1. Moving to the `taskCreate` method. Sequelize has a model method called `create`, you pass it your fields and it will return the newly created task from the database.

   ```javascript
   exports.taskCreate = (req, res) => {
     const newTask = Task.create(req.body);
     res.status(201).json(newTask);
   };
   ```

2. As we agreed, **Sequelize methods** are _asynchronous_, so we need an `async await` and a `try-catch` block.

   ```javascript
   exports.taskCreate = async (req, res) => {
     try {
       const newTask = await Task.create(req.body);
       res.status(201).json(newTask);
     } catch (error) {
       res.status(500).json({ message: error.message });
     }
   };
   ```

Let's test it using Postman by sending a `POST` request to `http://localhost:8000/tasks`.

```json
{
  "id": 8,
  "task": "New Task",
  "done": false,
  "updatedAt": "2020-04-30T06:57:23.945Z",
  "createdAt": "2020-04-30T06:57:23.945Z"
}
```

It works! Look at this! The database **automagically** generated an `id`, a `createdAt` and `updatedAt` fields!!

But what about our slug?! Don't worry! I didn't forget it.

1. Let's start with adding a slug field to our model.

   ```javascript
   {
       task: {
         type: DataTypes.STRING,
       },
       slug: {
         type: DataTypes.STRING,
       }
   ```

2. Now, we can still use the `slugify` library, but if we check the [Sequelize documentation](https://sequelize.org/master/manual/resources.html) we'll see that Sequelize recommends a dependency called [`sequelize-slugify`](https://www.npmjs.com/package/sequelize-slugify). Let's take a look at it.

   ```shell
     $ npm install sequelize-slugify
   ```

3. First, we will add a `unique` property to our `slug` field.

   ```javascript
   slug: {
     type: DataTypes.STRING,
     unique: true
   }
   ```

4. Next, we will require our brand new library

   ```javascript
   const SequelizeSlugify = require('sequelize-slugify');
   ```

5. Then **right before** our return in `models/Task.js`, call `SequelizeSlugify.slugifyModel` method, and we will pass it our model `Task` and the `source` of our slugs which is the `task`.

   ```javascript
   module.exports = (sequelize, DataTypes) => {
     const Task = sequelize.define("Task", {
       ...
     });

     SequelizeSlugify.slugifyModel(Task, {
       source: ["task"]
     });

     return Task;
   }
   ```
