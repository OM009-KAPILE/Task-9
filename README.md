#BACKEND CODE........

// backend/server.js
const express = require("express");
const cors = require("cors");

const app = express();
app.use(cors());

// Dummy student data
const students = [
  { id: 1, name: "Om", course: "React" },
  { id: 2, name: "Aarav", course: "Node.js" },
  { id: 3, name: "Riya", course: "Python" },
  { id: 4, name: "Neha", course: "Java" },
];

// API endpoint
app.get("/students", (req, res) => {
  res.json(students);
});

const PORT = 5000;
app.listen(PORT, () => {
  console.log(`✅ Server running at http://localhost:${PORT}`);
});




#FRONTEND CODE........

import React, { useEffect, useState } from "react";

function App() {
  const [students, setStudents] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch("http://localhost:5000/students")
      .then((res) => res.json())
      .then((data) => {
        setStudents(data);
        setLoading(false);
      })
      .catch((err) => {
        console.error("Error fetching students:", err);
        setLoading(false);
      });
  }, []);

  return (
    <div style={styles.container}>
      <h1>🎓 Student Directory</h1>
      {loading ? (
        <p>Loading students...</p>
      ) : (
        <ul style={styles.list}>
          {students.map((student) => (
            <li key={student.id} style={styles.card}>
              <h3>{student.name}</h3>
              <p>Course: {student.course}</p>
            </li>
          ))}
        </ul>
      )}
    </div>
  );
}

const styles = {
  container: {
    fontFamily: "Arial, sans-serif",
    padding: "20px",
    textAlign: "center",
  },
  list: {
    listStyle: "none",
    padding: 0,
  },
  card: {
    border: "1px solid #ddd",
    borderRadius: "10px",
    margin: "10px auto",
    padding: "15px",
    width: "250px",
    boxShadow: "0 4px 8px rgba(0,0,0,0.1)",
  },
};

export default App;
