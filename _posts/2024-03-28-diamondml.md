---
toc: true
comments: true
layout: post
title: Diamond ML
type: hacks
courses: { compsci: {week: 28} }
---

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Diamond Price Prediction</title>
<style>
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    margin: 0;
    padding: 20px;
    color: #333; /* Darker text for better contrast */
}

h1 {
    color: #0056b3; /* Slightly brighter for headings */
}

form {
    background: #fff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

label {
    margin-top: 10px;
    display: inline-block;
    color: #333; /* Ensuring label text is also darker for contrast */
}

input, select {
    margin-bottom: 10px;
    border: 1px solid #ddd;
    border-radius: 4px;
    padding: 8px;
    width: calc(100% - 22px);
}

button {
    background-color: #4caf50; /* Changing button color for a fresh look */
    color: white;
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

button:hover {
    background-color: #45a049;
}

#result {
    margin-top: 20px;
    padding: 20px;
    background-color: #e2e2e2;
    border-radius: 4px;
    color: #333; /* Darker text in the result box for readability */
}

.legend {
    margin-top: 20px;
    background: #fff;
    padding: 10px;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    color: #333; /* Ensuring legend text is also darker for contrast */
}

.legend h2 {
    color: #0056b3; /* Heading color in the legend for consistency */
}

.legend p {
    font-size: 14px;
    line-height: 1.6;
}
</style>
<script>
async function predictPrice() {
    const carat = document.getElementById('carat').value;
    const cut = document.getElementById('cut').value;
    const color = document.getElementById('color').value;
    const clarity = document.getElementById('clarity').value;
    const depth = document.getElementById('depth').value;
    const table = document.getElementById('table').value;
    const x = document.getElementById('x').value;
    const y = document.getElementById('y').value;
    const z = document.getElementById('z').value;
    const data = {
        carat: parseFloat(carat),
        cut: cut,
        color: color,
        clarity: clarity,
        depth: parseFloat(depth),
        table: parseFloat(table),
        x: parseFloat(x),
        y: parseFloat(y),
        z: parseFloat(z)
    };
    const response = await fetch('http://127.0.0.1:8032/api/diamond/predict', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify(data)
    });

    const result = await response.json();

    if (response.ok) {
        document.getElementById('result').textContent = 'Predicted Price: ' + result.prediction;
    } else {
        document.getElementById('result').textContent = 'Error: ' + result.error;
    }
}

    
</script>
</head>
<body>
<h1>Diamond Price Predictor</h1>
<form onsubmit="event.preventDefault(); predictPrice();">
    <label for="carat">Carat:</label>
    <input type="number" id="carat" step="0.01" required><br>

    <label for="cut">Cut:</label>
    <select id="cut" required>
        <option value="Ideal">Ideal</option>
        <option value="Premium">Premium</option>
        <option value="Good">Good</option>
        <option value="Fair">Fair</option>
        <option value="Poor">Poor</option>
    </select><br>

    <label for="color">Color:</label>
    <select id="color" required>
        <option value="D">D</option>
        <option value="E">E</option>
        <option value="F">F</option>
        <option value="G">G</option>
        <option value="H">H</option>
        <option value="I">I</option>
        <option value="J">J</option>
        <!-- Add other options as needed -->
    </select><br>

    <label for="clarity">Clarity:</label>
    <select id="clarity" required>
        <option value="IF">IF</option>
        <option value="VVS1">VVS1</option>
        <option value="VVS2">VVS2</option>
        <option value="VS1">VS1</option>
        <option value="VS2">VS2</option>
        <option value="SI1">SI1</option>
        <option value="SI2">SI2</option>
        <option value="I1">I1</option>
        <!-- Add other options as needed -->
    </select><br>

    <label for="depth">Depth (%):</label>
    <input type="number" id="depth" step="0.1" required><br>

    <label for="table">Table (%):</label>
    <input type="number" id="table" step="0.1" required><br>

    <label for="x">Length (x in mm):</label>
    <input type="number" id="x" step="0.01" required><br>

    <label for="y">Width (y in mm):</label>
    <input type="number" id="y" step="0.01" required><br>

    <label for="z">Depth (z in mm):</label>
    <input type="number" id="z" step="0.01" required><br>

    <button type="submit">Predict Price</button>
</form>

<div id="result"></div>

<!-- Legend explaining the parameters -->
<div class="legend">
    <h2>Parameter Legend</h2>
    <p><strong>Carat:</strong> Weight of the diamond. A higher carat value indicates a larger diamond.</p>
    <p><strong>Cut:</strong> Quality of the diamond's cut, affecting its symmetry, brightness, and overall visual appearance. Ranges from Poor to Ideal.</p>
    <p><strong>Color:</strong> Diamond color grade, which ranges from D (colorless) to Z (a yellow or brown hue).</p>
    <p><strong>Clarity:</strong> The absence of inclusions and blemishes. Clarity grades range from Flawless (no inclusions) to Included (obvious inclusions).</p>
    <p><strong>Depth (%):</strong> The height of a diamond, measured from the culet to the table, divided by its average girdle diameter.</p>
    <p><strong>Table (%):</strong> The width of the diamond's table (top surface) expressed as a percentage of its average diameter.</p>
    <p><strong>Length (x in mm), Width (y in mm), Depth (z in mm):</strong> Physical dimensions of the diamond.</p>
</div>

</body>
</html>
