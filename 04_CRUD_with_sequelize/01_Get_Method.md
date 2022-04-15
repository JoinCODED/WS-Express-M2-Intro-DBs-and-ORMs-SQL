So let's adjust our methods in `/api/tasks/tasks.controllers.js` to use the data from our brand new database.

1. First, to access our `Task` model, in `/api/tasks/tasks.controllers.js`, we will require it from our `models` folder:

```javascript
const { Task } = require('../db/models');
```

2. Let's start with our `tasksGet` method. to fetch all the tasks from our `Task` **model**, we will use a **sequelize method** called `.findAll()`.

   ```javascript
   exports.tasksGet = (req, res) => {
     const tasks = Task.findAll();
     console.log('tasks', tasks);
     res.json(tasks);
   };
   ```

   Such a weird response! We got a `200` and an empty object. If you `console.log` the `tasks` array you'll see that it's returning a `Promise`, which means that this method is asynchronous!

3. To **fix** this issue we will add `async` and its soulmate `await`. And for extra precautions let's **add** a `try-catch` block in case anything went wrong.

   ```javascript
   exports.tasksGet = async (req, res) => {
     try {
       const tasks = await Task.findAll();
       console.log('tasks', tasks);
     } catch (error) {}
   };
   ```

4. In case we had an error, what do we do? We'll **change the response status code** to [`500`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/500#:~:text=The%20HyperText%20Transfer%20Protocol%20(HTTP,%22catch%2Dall%22%20response.) which is the generic error response and pass the message from `error` as a JSON response.

   ```javascript
   exports.tasksGet = async (req, res) => {
     try {
       const tasks = await Task.findAll();
       console.log('tasks', tasks);
     } catch (error) {
       res.status(500).json({ message: error.message });
     }
   };
   ```

5. Test it in Postman. Finally our data is coming from a real database! **This calls for a celebration!! 🎉**

6. But what if I don't want to send all the fields? Let's assume we only want to send `task` and `id`. Basically, we can **pass an object** to `.findAll()` to **customize** our **response**, to choose the fields we use the `attributes` key and pass it an array of fields we need. Let's test it again.

   ```javascript
   const tasks = await Task.findAll({
     attributes: ['id', 'task'],
   });
   ```

   Tada!

7. What if I want all fields except for the `createdAt` and `updatedAt`? We can pass all fields to attributes. But what if my model had ten fields? Do I need to write all of them? Nope, we can basically pass `attributes` an object that has an `exclude` property that takes an array of unwanted fields:

   ```javascript
   const tasks = await Task.findAll({
     attributes: { exclude: ['createdAt', 'updatedAt'] },
   });
   ```

8. Let's test it again... Tada!
