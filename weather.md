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
            // Add your API call here and manipulate the #result div to display the weather information.
            // You can use JavaScript fetch or any other library to make the API request.
            // Remember to handle errors and display appropriate messages in case of failures.
        }
    </script>
</body>
</html>


















