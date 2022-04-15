1. Moving to the update method, let's start by adding the `async await` and `try-catch` block.

   ```javascript
   exports.taskUpdate = async (req, res) => {
     const { taskId } = req.params;
     try {
       // ...
     } catch (error) {
       res.status(500).json({ message: error.message });
     }
   };
   ```

2. Updating a `task` **requires two steps**: **finding** the task with `taskId`, then **updating** this task. To get an item by its ID we will use a method called `.findByPk()`. `pk` stands for _primary key_, which is a unique value that distinguishes between the objects, which is the `id`.

   ```javascript
   exports.taskUpdate = async (req, res) => {
     const { taskId } = req.params;
     try {
       const foundTask = await Task.findByPk(taskId);
     } catch (error) {
       res.status(500).json({ message: error.message });
     }
   };
   ```

3. Then we will pass `foundTask` to a **Sequelize method** called `.update()` that **will take care of updating the task for us**. Don't forget to **change the status** to `204` and **end the response**.

   ```javascript
   try {
     const foundTask = await Task.findByPk(taskId);
     await foundTask.update(req.body);
     res.status(204).end();
   }
   ```

4. But what if the task ID sent doesn't exist? The response is `null` with a status code `200`. We need to fix this! We must check if the task is found or not:

   ```javascript
   try {
     const foundTask = await Task.findByPk(taskId);
     if (foundTask) {
       await foundTask.update(req.body);
       res.status(204).end();
     } else {
       res.status(404).json({ message: "Task not found" });
     }
   }
   ```
