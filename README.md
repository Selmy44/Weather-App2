<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }
    </style>
</head>
<body>
    <h1>Weather App</h1>
    <label for="cityInput">Enter city:</label>
    <input type="text" id="cityInput" placeholder="Enter city name">
    <button onclick="getWeather()">Get Weather</button>

    <div id="weatherInfo"></div>

    <script>
        function getWeather() {
            const apiKey = 'YOUR_OPENWEATHERMAP_API_KEY'; // Replace with your actual API key
            const cityInput = document.getElementById('cityInput').value;

            if (!cityInput) {
                alert('Please enter a city name');
                return;
            }

            const apiUrl = `https://api.openweathermap.org/data/2.5/weather?q=${cityInput}&appid=${apiKey}&units=metric`;

            fetch(apiUrl)
                .then(response => response.json())
                .then(data => {
                    displayWeather(data);
                })
                .catch(error => {
                    console.error('Error fetching weather data:', error);
                    alert('Error fetching weather data. Please try again.');
                });
        }

        function displayWeather(data) {
            const weatherInfo = document.getElementById('weatherInfo');

            const cityName = data.name;
            const temperature = data.main.temp;
            const description = data.weather[0].description;

            const weatherHtml = `
                <h2>${cityName}</h2>
                <p>Temperature: ${temperature} &deg;C</p>
                <p>Description: ${description}</p>
            `;

            weatherInfo.innerHTML = weatherHtml;
        }
    </script>
</body>
</html>
