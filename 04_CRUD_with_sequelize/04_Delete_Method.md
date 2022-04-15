1. The **delete method** is _very similar_ to the **update method**. We need to **find** the task with `taskId` then **delete** this task. To find a task, we will use `.findByPk()` method.

   ```javascript
   exports.taskDelete = async (req, res) => {
     const { taskId } = req.params;
     try {
       const foundTask = await Task.findByPk(taskId);
     } catch (err) {
       res.status(500).json({ message: error.message });
     }
   };
   ```

2. If `foundTask` exists, we will pass it to a **Sequelize method** called `.destroy()` that will take care of deleting the task for us, **set the status to** `204` and **end the response**.

   ```javascript
   try {
     const foundTask = await Task.findByPk(taskId);
     if (foundTask) {
       await foundTask.destroy();
       res.status(204).end();
     }
   }
   ```

3. Else, we will **set that status** code to `404` and a message as a JSON response.

   ```javascript
   try {
     const foundTask = await Task.findByPk(taskId);
     if (foundTask) {
       await foundTask.destroy();
       res.status(204).end();
     } else {
       res.status(404).json({ message: "task not found" });
     }
   }
   ```
