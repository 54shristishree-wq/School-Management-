# School-Management-
Automates and centralizes a school's administrative, academic, and financial tasks
<!DOCTYPE html>
<html>
<head>
  <title>School Management System</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

<div class="container">
  <h1>School Management System</h1>

  <!-- Student Form -->
  <h2>Add Student</h2>

  <input id="name" placeholder="Student Name">
  <input id="roll" placeholder="Roll Number">
  <input id="className" placeholder="Class">

  <button onclick="addStudent()">Add Student</button>

  <h2>Student List</h2>
  <table>
    <thead>
      <tr>
        <th>Name</th>
        <th>Roll No</th>
        <th>Class</th>
        <th>Action</th>
      </tr>
    </thead>
    <tbody id="studentTable"></tbody>
  </table>
</div>

<script src="app.js"></script>
</body>
</html> 
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial;
}

body{
  background: #eef2ff;
  display: flex;
  justify-content: center;
  padding: 30px;
}

.container{
  background: white;
  padding: 25px;
  border-radius: 10px;
  width: 800px;
  box-shadow: 0 0 10px rgba(0,0,0,0.2);
}

h1{
  text-align: center;
  margin-bottom: 15px;
}

input{
  width: 32%;
  padding: 8px;
  margin-top: 10px;
  margin-bottom: 10px;
}

button{
  padding: 8px 12px;
  background: #1e3a8a;
  color: white;
  border: none;
  border-radius: 6px;
  margin-top: 5px;
  cursor: pointer;
}

table{
  width: 100%;
  margin-top: 10px;
  border-collapse: collapse;
}

th, td{
  border: 1px solid #c7d2fe;
  padding: 8px;
  text-align: center;
}

th{
  background: #e0e7ff;
}
// Load existing students from localStorage
let students = JSON.parse(localStorage.getItem("students")) || [];

// Display students initially
displayStudents();

function addStudent() {
  const name = document.getElementById("name").value;
  const roll = document.getElementById("roll").value;
  const className = document.getElementById("className").value;

  if (!name || !roll || !className) {
    alert("Please fill all fields");
    return;
  }

  // Create object
  const student = { name, roll, className };

  // Save into array
  students.push(student);

  // Save to localStorage
  localStorage.setItem("students", JSON.stringify(students));

  // Refresh table
  displayStudents();

  // Clear inputs
  document.getElementById("name").value = "";
  document.getElementById("roll").value = "";
  document.getElementById("className").value = "";
}

function deleteStudent(index) {
  students.splice(index, 1);
  localStorage.setItem("students", JSON.stringify(students));
  displayStudents();
}

function displayStudents() {
  const table = document.getElementById("studentTable");
  table.innerHTML = "";

  students.forEach((student, index) => {
    table.innerHTML += `
      <tr>
        <td>${student.name}</td>
        <td>${student.roll}</td>
        <td>${student.className}</td>
        <td><button onclick="deleteStudent(${index})">Delete</button></td>
      </tr>
    `;
  });
}
