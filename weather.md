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

        input[type="San Diego"] {
            width: 100%;
            padding: 10px;
            margin-bottom: 20px;
            box-sizing: border-box;
        }

        button {
            background-color: #4CAF50;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        button:hover {
            background-color: #45a049;
        }

        #result {
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Weather Application</h2>
        <input type="text" id="location" placeholder="Enter location">
        <button onclick="getWeather()">Get Weather</button>
        <div id="result"></div>
    </div>

<script>
    function getWeather() {
        const location = document.getElementById('location').value;
        // Replace 'your_api_url_here' with your actual API endpoint
        fetch('https://backend.stu.nighthawkcodingsociety.com/api/weather/' + location)
            .then(response => response.json())
            .then(data => {
                document.getElementById('result').innerText = "Current Temperature in "+ location +" is: "+ JSON.stringify(data["current"]["feelslike_f"], null, 2)+ " °F";
            })
            .catch(error => {
                console.error('Error fetching data:', error);
                document.getElementById('result').innerText = 'An error occurred. Please try again later.';
            });
    }
</script>
</body>
</html>


















