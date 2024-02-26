---
toc: true
comments: true
layout: post
title: Tri 2 Individual Review
type: hacks
courses: { compsci: {week: 24} }
---
#### StockSense-Data Project Requirements

#### Component A

Requirement: Input Instructions
The project captures input from the user via an HTML form. The user enters a stock symbol in the input field and triggers the fetchStockData() function by clicking the button.


```html
<!-- HTML Input for Stock Symbol -->
<input type="text" id="stockSymbol" placeholder="Enter Stock Symbol (e.g., AAPL)">
<button onclick="fetchStockData()">Fetch Stock Data</button>
```

Requirement: Use of at least one list (or other collection type) to represent a collection of
data that is stored and used to manage program complexity and help fulfill
the program’s purpose



In the JavaScript function displayStockData(), a collection (JavaScript object) is used to store and process the stock data fetched from the API.



For the JavaScript code:

```javascript
// JavaScript: Processing and Displaying Stock Data using a Collection (Object)
function displayStockData(data) {
    if (!data['Time Series (Daily)']) {
        document.getElementById('stockData').innerHTML = 'No data available for this symbol.';
        return;
    }

    const timeSeries = data['Time Series (Daily)'];
    const latestDate = Object.keys(timeSeries)[0];
    const latestData = timeSeries[latestDate];
    // More code follows...
}
```


Requirement: At least one procedure that contributes to the program’s intended purpose,
where you have defined: the procedure’s name, the return type (if necessary), one or more parameters


In the Flask backend, a procedure get within the StockDataAPI class is defined to fetch stock data from the Alpha Vantage API. This procedure is a method with a return type of JSON data or an error message and takes one parameter, symbol.



```python
class StockDataAPI(Resource):
    def get(self, symbol):
        # Procedure body...
        return jsonify(data)  # Return type is JSON
```

Requirement: An algorithm that includes sequencing, selection, and iteration that is in the
body of the selected procedure


Within the getStockData() function in the model, an algorithm demonstrates sequencing (executing HTTP request), selection (checking for errors), and iteration (parsing through the Time Series (Daily) data).


```python
# Model: Algorithm to Fetch and Parse Stock Data
def getStockData(symbol):
    # Sequencing: Making an HTTP GET request
    conn.request("GET", f"/query?function=TIME_SERIES_DAILY&symbol={encodedSymbol}&apikey={access_key}", payload, headers)
    res = conn.getresponse()
    data = res.read()
    decodedString = data.decode("utf-8")
    j = json.loads(decodedString)
    
    # Selection: Error Handling
    try:
        latestDate = next(iter(j['Time Series (Daily)']))
    except KeyError:
        return {"error": "Failed to fetch or parse stock data from Alpha Vantage"}
    
    # Iteration: Extracting the latest data
    latestData = j['Time Series (Daily)'][latestDate]
    # More code follows...
```


Requirement: Calls to your student-developed procedure


The fetchStockData() function in the frontend calls the displayStockData() procedure to process and display the fetched stock data.


```javascript
// Frontend: Calling displayStockData() within fetchStockData()
async function fetchStockData() {
    // Code to fetch data...
    const data = await response.json();
    displayStockData(data);  // Procedure call
}
```

Requirement: Instructions for output (tactile, audible, visual, or textual) based on input and
program functionality


The output is displayed visually in the HTML document within the #stockData div. The displayStockData() function updates this div with the fetched stock data.


```javascript
// JavaScript: Output Display in HTML
function displayStockData(data) {
    // Code to process data...
    const content = `
        <p>Date: ${latestDate}</p>
        <p>Open: ${latestData['1. open']}</p>
        // Additional data fields...
    `;
    document.getElementById('stockData').innerHTML = content;  // Visual Output
}
```

#### Component B

link to video: https://youtu.be/_S6PDHjsv1M

requirements:
□ Input to your program
□ At least one aspect of the functionality of your program
□ Output produced by your program
Your video may NOT contain:
□ Any distinguishing information about yourself
□ Voice narration (though text captions are encouraged)
Your video must be:
□ Either .webm, .mp4, .wmv, .avi, or .mov format
□ No more than 1 minute in length
□ No more than 30MB in file size