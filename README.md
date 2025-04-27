<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Weather App</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="container">
    <h1>🌦️ Weather App</h1>
    <input type="text" id="cityInput" placeholder="Enter city name" />
    <button onclick="getWeather()">Get Weather</button>
    <div id="weatherResult"></div>
  </div>

  <script src="script.js"></script>
</body>
</html>
body {
    font-family: Arial, sans-serif;
    text-align: center;
    background: #f0f0f0;
    padding: 50px;
  }
  
  .container {
    background: white;
    padding: 20px;
    border-radius: 10px;
    display: inline-block;
  }
  
  input {
    padding: 10px;
    width: 200px;
  }
  
  button {
    padding: 10px;
    margin-left: 10px;
  }
  
  #weatherResult {
    margin-top: 20px;
    font-size: 18px;
  }
  
const apiKey = "cb618880920c88e9cf2245b99c1bdcd9"; // 🔑 Replace with your actual OpenWeatherMap API key

function getWeather() {
  const city = document.getElementById('cityInput').value;
  const resultDiv = document.getElementById('weatherResult');

  if (!city) {
    resultDiv.innerHTML = '⛔ Please enter a city name!';
    return;
  }

  const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`;

  fetch(url)
    .then(response => {
      if (!response.ok) {
        throw new Error('City not found!');
      }
      return response.json();
    })
    .then(data => {
      const { name, main, weather } = data;
      resultDiv.innerHTML = `
        <h2>${name}</h2>
        <p>🌡️ Temp: ${main.temp}°C</p>
        <p>💧 Humidity: ${main.humidity}%</p>
        <p>🌥️ Condition: ${weather[0].description}</p>
      `;
    })
    .catch(error => {
      resultDiv.innerHTML = `❌ Error: ${error.message}`;
    });
}

