# PRODIGY_AD_02

# index.html

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>To-Do List App</title>
  <link rel="stylesheet" href="style.css"/>
</head>
<body>
  <div class="container">
    <h1>To-Do List</h1>
    <div class="input-container">
      <input type="text" id="task-input" placeholder="Enter a task..." />
      <button onclick="addTask()">Add</button>
    </div>
    <div class="filter-container">
     <button onclick="filterTasks('all')">All</button>
     <button onclick="filterTasks('active')">Active</button>
     <button onclick="filterTasks('completed')">Completed</button>
    </div>
    <ul id="task-list"></ul>
  </div>
  
  <script src="script.js"></script>
</body>
</html>

# style.css

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Segoe UI', sans-serif;
  background: linear-gradient(135deg, #e0eafc, #cfdef3);
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  padding: 20px;
}

.container {
  background: #ffffff;
  padding: 50px 60px;
  border-radius: 20px;
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 650px;
  max-height: 90vh;
  overflow-y: auto;
  display: flex;
  flex-direction: column;
}

h1 {
  text-align: center;
  color: #333;
  margin-bottom: 30px;
  font-size: 28px;
}

.input-container {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

input[type="text"] {
  flex: 1;
  padding: 16px;
  font-size: 18px;
  border: 1px solid #ccc;
  border-radius: 6px;
  outline: none;
}

/* Filter Buttons */
.filter-container {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-bottom: 20px;
}

.filter-container button {
  padding: 10px 16px;
  font-size: 15px;
  background-color: #f1f1f1;
  color: #333;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  transition: background 0.3s ease;
}

.filter-container button:hover {
  background-color: #ddd;
}

button {
  padding: 14px 20px;
  font-size: 18px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  transition: background 0.3s ease;
}

button:hover {
  background-color: #0056b3;
}

/* Task List */
ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: #f8f9fa;
  padding: 16px 20px;
  margin-bottom: 12px;
  border-radius: 8px;
  box-shadow: inset 0 0 4px rgba(0, 0, 0, 0.05);
  gap: 10px;
  font-size: 17px;
}

li.completed input[type="text"] {
  text-decoration: line-through;
  color: #888;
}

li input[type="text"] {
  border: none;
  background: transparent;
  font-size: 17px;
  flex: 1;
  margin-left: 10px;
}

.actions {
  display: flex;
  gap: 5px;
}

.actions button {
  background-color: #6c757d;
  font-size: 14px;
  padding: 8px 12px;
}

.actions button:hover {
  background-color: #495057;
}

/* Responsive tweaks */
@media (max-width: 600px) {
  .container {
    padding: 30px 20px;
  }

  h1 {
    font-size: 24px;
  }

  button {
    font-size: 16px;
    padding: 12px;
  }

  input[type="text"] {
    font-size: 16px;
  }

  li {
    flex-direction: column;
    align-items: flex-start;
  }

  .actions {
    width: 100%;
    justify-content: flex-end;
  }
}

# script.js

function addTask() {
  const taskInput = document.getElementById("task-input");
  const taskText = taskInput.value.trim();

  if (taskText === "") return;

  const li = document.createElement("li");

  const checkbox = document.createElement("input");
  checkbox.type = "checkbox";
  checkbox.onchange = () => {
    li.classList.toggle("completed", checkbox.checked);
  };

  const input = document.createElement("input");
  input.type = "text";
  input.value = taskText;
  input.disabled = true;

  const actions = document.createElement("div");
  actions.className = "actions";

  const editBtn = document.createElement("button");
  editBtn.textContent = "Edit";
  editBtn.onclick = () => {
    input.disabled = !input.disabled;
    editBtn.textContent = input.disabled ? "Edit" : "Save";
  };

  const deleteBtn = document.createElement("button");
  deleteBtn.textContent = "Delete";
  deleteBtn.onclick = () => li.remove();

  actions.appendChild(editBtn);
  actions.appendChild(deleteBtn);

  li.appendChild(checkbox);
  li.appendChild(input);
  li.appendChild(actions);

  document.getElementById("task-list").appendChild(li);

  taskInput.value = "";
}
function filterTasks(filter) {
  const tasks = document.querySelectorAll("#task-list li");

  tasks.forEach(task => {
    const isCompleted = task.classList.contains("completed");

    if (filter === "all") {
      task.style.display = "flex";
    } else if (filter === "active" && isCompleted) {
      task.style.display = "none";
    } else if (filter === "completed" && !isCompleted) {
      task.style.display = "none";
    } else {
      task.style.display = "flex";
    }
  });
}
