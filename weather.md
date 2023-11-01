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
        .button-container {
            display: flex;
            justify-content: space-between;
        }
        .button-container button {
            background-color: #4CAF50;
            color: white;
            padding: 5px 10px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            flex: 1;
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
        .button-spacing {
            margin-right: 10px;
        }
    </style>


<body>
    <div class="container">
    <label class="switch">
    <input type="checkbox" id="tempSwitch" onclick="toggleTemperatureUnit()">
    <span class="slider round"></span>
</label>
<span id="tempLabel">Metric Units</span>

        <h2>Weather Application</h2>
        <img src="FocusArea__Weather-02.jpg"  height="200" width="200">

        <input type="text" id="location" placeholder="Enter city name" autofocus onkeyup="handleKeyPress(event)">
        <div class="button-container">
            <button class="button-spacing" onclick="getWindSpeed()">Wind Speed</button>
            <button class="button-spacing" onclick="getTemperature()">Temperature</button>
            <button class="button-spacing" onclick="getPrecipitation()">Precipitation</button>
        </div>
        <div id="result"></div>
    </div>
    <script>
        function handleKeyPress(event) {
            if (event.key === 'Enter') {
                getWeather();
            }
        }

        function getWindSpeed() {
            fetchWeatherData('wind_mph');
        }

        function getTemperature() {
            fetchWeatherData('feelslike_f');
        }

        function getPrecipitation() {
            fetchWeatherData('precip_in');
        }

        function capitalizeFirstLetter(string) {
            return string.charAt(0).toUpperCase() + string.slice(1);
        }

        function fetchWeatherData(dataType) {
            const locationInput = document.getElementById('location');
            const resultDiv = document.getElementById('result');
            const location = capitalizeFirstLetter(locationInput.value.trim());


            if (location === '') {
                resultDiv.innerText = 'Please enter a location';
                return;
            }

            resultDiv.innerText = 'Loading...';

            fetch('http://127.0.0.1:8531/api/weather/' + location)
                .then(response => response.json())
                .then(data => {
                    let imageFetchUrl = 'http://127.0.0.1:8531/api/cityimage/' + location;
                    fetch(imageFetchUrl)
                        .then(response => response.json())
                        .then(imageData => {
                            let imageUrl = imageData.image_url; // Assuming the URL is stored in a field named 'url'
                            console.log("IMAGE_URL===="+ imageUrl)
                            

                            if (dataType === 'wind_mph') {
                                resultDiv.innerHTML = `<h2>Current Wind Speed in ${location} is ${data["current"]["wind_mph"]} MPH</h2>`;
                            } else if (dataType === 'feelslike_f') {
                                resultDiv.innerHTML = `<h2>Current Temperature in ${location} is ${data["current"]["feelslike_f"]} °F</h2>`;
                            } else if (dataType === 'precip_in') {
                                resultDiv.innerHTML = `<h2>Current Precipitation in ${location} is ${data["current"]["precip_in"]} inches</h2>`;
                            }
                            let imgElement = document.createElement('img');
                            imgElement.src = imageUrl;
                            resultDiv.appendChild(imgElement);
                            })
                        .catch(error => {
                            console.error('Error fetching image:', error);
                            resultDiv.innerText += 'An error occurred fetching the image. Please try again later.';
                        });
                })
                .catch(error => {
                    console.error('Error fetching data:', error);
                    resultDiv.innerText = 'An error occurred. Please try again later.';
                });
        }
                
               

    </script>           
</body>



<html>

<head>
    <title>Fetch Image from API</title>
</head>

<body>
    <script>
        // Replace the URL with the appropriate API endpoint
        const url = 'http://127.0.0.1:8531/api/cityimage/';

        // Fetch the image from the API
        fetch(url)
            .then(response => {
                // Check if the request was successful
                if (!response.ok) {
                    throw new Error('Network response was not ok');
                }
                return response.blob();
            })
            .then(blob => {
                // Create an object URL from the blob
                const objectURL = URL.createObjectURL(blob);

                // Create an image element
                const img = document.createElement('img');

                // Set the src attribute to the object URL
                img.src = objectURL;

                // Append the image to the document body or any other desired element
                document.body.appendChild(img);
            })
            .catch(error => {
                console.error('There has been a problem with your fetch operation:', error);
            });
    </script>
</body>

</html>
