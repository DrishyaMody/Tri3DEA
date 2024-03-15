---
toc: true
comments: false
layout: post
title: Titanic ML
courses: { compsci: {week: 26} }
type: hacks
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Titanic Survival Prediction</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .container {
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            width: 300px;
        }
        h2 {
            text-align: center;
            color: #333;
        }
        form {
            display: flex;
            flex-direction: column;
        }
        label {
            margin-top: 10px;
        }
        input, select, button {
            padding: 10px;
            margin-top: 5px;
            border: 1px solid #ddd;
            border-radius: 4px;
        }
        button {
            background-color: #5cb85c;
            color: white;
            margin-top: 20px;
        }
        button:hover {
            background-color: #4cae4c;
        }
        #predictionResult {
            margin-top: 20px;
            text-align: center;
            padding: 10px;
            background-color: #dff0d8;
            border-radius: 4px;
            display: none; /* Hide initially */
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Titanic Survival Predictor</h2>
        <form id="predictionForm">
            <label for="name">Name:</label>
            <input type="text" id="name" placeholder="Enter Name" required>

            <label for="pclass">Class:</label>
            <select id="pclass">
                <option value="1">1st Class</option>
                <option value="2" selected>2nd Class</option>
                <option value="3">3rd Class</option>
            </select>

            <label for="sex">Sex:</label>
            <select id="sex">
                <option value="male" selected>Male</option>
                <option value="female">Female</option>
            </select>

            <!-- Add other fields in a similar way -->
            <!-- ... -->

            <button type="submit">Predict Survival</button>
        </form>
        <div id="predictionResult"></div>
    </div>

    <script>
        document.getElementById('predictionForm').onsubmit = async function(e) {
            e.preventDefault();
            const formData = {
                // Gather form data. Example:
                name: document.getElementById('name').value,
                pclass: document.getElementById('pclass').value,
                sex: document.getElementById('sex').value,
                // Continue for each field
            };

            const response = await fetch('/api/titanic/predict', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify(formData),
            });

            const result = await response.json();
            const resultDiv = document.getElementById('predictionResult');
            resultDiv.style.display = 'block'; // Show the result
            resultDiv.innerText = 
              `Death Probability: ${result['Death probability']}, ` + 
              `Survival Probability: ${result['Survival probability']}`;
        };
    </script>
</body>
</html>
