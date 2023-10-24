---
layout: default
title: Student Blog
---

<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather Application</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }

        .container {
            text-align: center;
            padding: 20px;
            border: 2px solid #ddd;
            border-radius: 5px;
            width: 300px;
        }

        input[type="text"] {
            width: 100%;
            padding: 10px;
            margin-bottom: 20px;
            box-sizing: border-box;
            border: 1px solid #ddd;
            border-radius: 5px;
        }

        button {
            background-color: #4CAF50;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            width: 100%;
        }

        button:hover {
            background-color: #45a049;
        }

        #result {
            margin-top: 20px;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
        }
    </style>
</head>

<body>
    <div class="container">
        <h2>Weather Application</h2>
        <input type="text" id="location" placeholder="Enter city name" autofocus onkeyup="handleKeyPress(event)">
        <button onclick="getWeather()">Get Weather</button>
        <div id="result"></div>
    </div>

    <script>
        function handleKeyPress(event) {
            if (event.key === 'Enter') {
                getWeather();
            }
        }

        function getWeather() {
            const locationInput = document.getElementById('location');
            const resultDiv = document.getElementById('result');
            const location = locationInput.value.trim();

            if (location === '') {
                resultDiv.innerText = 'Please enter a location';
                return;
            }

            resultDiv.innerText = 'Loading...';

            fetch('https://backend.stu.nighthawkcodingsociety.com/api/weather/' + location)
                .then(response => response.json())
                .then(data => {
                    resultDiv.innerText = "Current Temperature in " + location + " is " + data["current"]["feelslike_f"] + " °F"+ " Current Windspeed in " + location + " is " +data["current"]["wind_mph"] + " MPH";

                })
                .catch(error => {
                    console.error('Error fetching data:', error);
                    resultDiv.innerText = 'An error occurred. Please try again later.';
                });
        }
    </script>
</body>

</html>

<div>
    <button><a href="https://tanvi-3.github.io/tanvipampati3/">Wind Speed</a></button>
</div>

<div>
    <button><a href="https://tanvi-3.github.io/tanvipampati3/">Temperature</a></button>
</div>