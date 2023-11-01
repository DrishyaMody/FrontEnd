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
    <button class="button-spacing" onclick="getMetric()">Metric Units</button>
</label>

        <h2>Weather Application</h2>
        <img src="https://backend.stu.nighthawkcodingsociety.com/static/assets/sunny_weather.png" id = "weatherIcon"  height="200" width="200">

        <input type="text" id="location" placeholder="Enter city name" autofocus onkeyup="handleKeyPress(event)">
        <div class="button-container">
            <button class="button-spacing" onclick="getWindSpeed()">Wind Speed</button>
            <button class="button-spacing" onclick="getTemperature()">Temperature</button>
            <button class="button-spacing" onclick="getPrecipitation()">Precipitation</button>
        </div>
        <div id="result"></div>
    </div>


    <script>
        let isMetric = false;

        function handleKeyPress(event) {
            if (event.key === 'Enter') {
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

        function getMetric() {
            isMetric = !isMetric;
            alert(isMetric);
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

            fetch('https://backend.stu.nighthawkcodingsociety.com/api/weather/' + location)
                .then(response => response.json())
                .then(data => {
                    let imageFetchUrl = 'https://backend.stu.nighthawkcodingsociety.com/api/cityimage/' + location;
                    fetch(imageFetchUrl)
                        .then(response => response.json())
                        .then(imageData => {
                            let imageUrl = imageData.image_url; // Assuming the URL is stored in a field named 'url'
                            console.log("IMAGE_URL===="+ imageUrl)
                            var image = document.getElementById('weatherIcon')
                            image.src = data["current"]["weatherIcon_url"]

                            if (dataType === 'wind_mph' && isMetric === true) {
                                resultDiv.innerHTML = `<h2>Current Wind Speed in ${location} is ${parseFloat(data["current"]["wind_mph"]*1.61).toFixed(2)} KPH </h2>`;
                            } else if (dataType === 'feelslike_f' && isMetric === true) {
                                resultDiv.innerHTML = `<h2>Current Temperature in ${location} is ${parseFloat((data["current"]["feelslike_f"]-32)*(0.55)).toFixed(2)} °C</h2>`;
                            } else if (dataType === 'precip_in' && isMetric === true) {
                                resultDiv.innerHTML = `<h2>Current Precipitation in ${location} is ${parseFloat(data["current"]["precip_in"]*2.54).toFixed(2)} cm</h2>`;
                            } else if (dataType === 'wind_mph' && isMetric === false) {
                                resultDiv.innerHTML = `<h2>Current Wind Speed in ${location} is ${data["current"]["wind_mph"]} MPH </h2>`;
                            } else if (dataType === 'feelslike_f' && isMetric === false) {
                                resultDiv.innerHTML = `<h2>Current Temperature in ${location} is ${data["current"]["feelslike_f"]} °F</h2>`;
                            } else if (dataType === 'precip_in' && isMetric === false) {
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


