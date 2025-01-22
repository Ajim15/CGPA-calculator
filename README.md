<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CGPA Calculator</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>CGPA Calculator</h1>
        <div id="subjects">
            <div class="subject-row">
                <input type="number" class="grade" placeholder="Grade (0-4)" min="0" max="4" step="0.01">
                <input type="number" class="credit" placeholder="Credits" min="1" step="1">
            </div>
        </div>
        <button onclick="addSubject()">Add Subject</button>
        <button onclick="calculateCGPA()">Calculate CGPA</button>
        <div id="result"></div>
    </div>
    <script src="script.js"></script>
    body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    margin: 0;
    padding: 20px;
}

.container {
    max-width: 500px;
    margin: auto;
    background: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

h1 {
    text-align: center;
    margin-bottom: 20px;
    color: #333;
}

.subject-row {
    display: flex;
    justify-content: space-between;
    margin-bottom: 10px;
}

.subject-row input {
    width: 48%;
    padding: 8px;
    border: 1px solid #ddd;
    border-radius: 4px;
}

button {
    width: 100%;
    padding: 10px;
    margin-top: 10px;
    border: none;
    border-radius: 4px;
    background-color: #007bff;
    color: white;
    font-size: 16px;
    cursor: pointer;
}

button:hover {
    background-color: #0056b3;
}

#result {
    margin-top: 20px;
    text-align: center;
    font-size: 18px;
    color: #007bff;
}

</html>
// Arrays to store grades and credits
let grades = [];
let credits = [];

// Function to add a new subject row
function addSubject() {
    const subjectsDiv = document.getElementById('subjects');
    const newRow = document.createElement('div');
    newRow.classList.add('subject-row');
    newRow.innerHTML = `
        <input type="number" class="grade" placeholder="Grade (0-4)" min="0" max="4" step="0.01">
        <input type="number" class="credit" placeholder="Credits" min="1" step="1">
    `;
    subjectsDiv.appendChild(newRow);
}

// Function to calculate CGPA
function calculateCGPA() {
    const gradeInputs = document.querySelectorAll('.grade');
    const creditInputs = document.querySelectorAll('.credit');

    // Reset arrays and totals
    grades = [];
    credits = [];
    let totalQualityPoints = 0;
    let totalCredits = 0;

    // Loop through inputs and calculate total quality points and credits
    for (let i = 0; i < gradeInputs.length; i++) {
        const grade = parseFloat(gradeInputs[i].value);
        const credit = parseFloat(creditInputs[i].value);

        if (!isNaN(grade) && !isNaN(credit) && grade >= 0 && grade <= 4 && credit > 0) {
            grades.push(grade);
            credits.push(credit);
            totalQualityPoints += grade * credit;
            totalCredits += credit;
        } else {
            alert('Please enter valid grades (0-4) and credits (>0).');
            return;
        }
    }

    // Calculate CGPA
    const cgpa = totalCredits > 0 ? (totalQualityPoints / totalCredits).toFixed(2) : 0;

    // Display result
    document.getElementById('result').innerText = `Your CGPA is: ${cgpa}`;
}
