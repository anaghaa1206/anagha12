---
toc: true
comments: false
layout: post
title: Stock Data Fetcher
type: hacks
---
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stock Data Fetcher</title>
</head>
<body>
    <h1>Stock Data Fetcher</h1>
    <input type="text" id="stockSymbol" placeholder="Enter Stock Symbol (e.g., AAPL)">
    <button onclick="fetchStockData()">Fetch Stock Data</button>

    <div id="stockData"></div>

    <script>
        async function fetchStockData() {
            const symbol = document.getElementById('stockSymbol').value;
            // Check your console to ensure the URL is formed correctly
            console.log(`Fetching data for symbol: ${symbol}`);
            
            // Update the fetch URL if necessary to match your Flask app's full URL
            const response = await fetch(`http://localhost:8055/api/stockchart/chart/${symbol}`);

            if (response.ok) {
                const data = await response.json();
                displayStockData(data);
            } else {
                console.error('Failed to fetch stock data.');
                document.getElementById('stockData').innerHTML = 'Failed to fetch stock data.';
            }
        }

        function displayStockData(data) {
            // Ensure data is present
            if (!data['Time Series (Daily)']) {
                document.getElementById('stockData').innerHTML = 'No data available for this symbol.';
                return;
            }

            const timeSeries = data['Time Series (Daily)'];
            const latestDate = Object.keys(timeSeries)[0];
            const latestData = timeSeries[latestDate];

            const content = `
                <h2>Stock Data for ${document.getElementById('stockSymbol').value}</h2>
                <p>Date: ${latestDate}</p>
                <p>Open: ${latestData['1. open']}</p>
                <p>High: ${latestData['2. high']}</p>
                <p>Low: ${latestData['3. low']}</p>
                <p>Close: ${latestData['4. close']}</p>
                <p>Volume: ${latestData['5. volume']}</p>
            `;

            document.getElementById('stockData').innerHTML = content;
        }
    </script>
</body>
</html>