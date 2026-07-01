<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather Dashboard</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

<div class="container">
    <h1>🌤 Weather Dashboard</h1>

    <input type="text" id="city" placeholder="Enter City Name">
    <button onclick="getWeather()">Search</button>

    <div id="weather"></div>
</div>

<script src="script.js"></script>

</body>
</html>
body{
    font-family: Arial, sans-serif;
    background:#87CEEB;
    display:flex;
    justify-content:center;
    align-items:center;
    height:100vh;
}

.container{
    background:white;
    padding:20px;
    border-radius:10px;
    text-align:center;
    width:350px;
    box-shadow:0 0 10px rgba(0,0,0,0.2);
}

input{
    width:80%;
    padding:10px;
    margin:10px;
}

button{
    padding:10px 20px;
    background:blue;
    color:white;
    border:none;
    cursor:pointer;
}

button:hover{
    background:darkblue;
}

#weather{
    margin-top:20px;
    font-size:18px;
}
const apiKey = "YOUR_API_KEY";

async function getWeather() {

    const city = document.getElementById("city").value;

    if(city===""){
        alert("Please enter a city");
        return;
    }

    const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`;

    try{

        const response = await fetch(url);

        if(!response.ok){
            throw new Error("City not found");
        }

        const data = await response.json();

        document.getElementById("weather").innerHTML = `
            <h2>${data.name}</h2>
            <p>🌡 Temperature: ${data.main.temp} °C</p>
            <p>💧 Humidity: ${data.main.humidity}%</p>
            <p>🌬 Wind Speed: ${data.wind.speed} m/s</p>
            <p>☁ Weather: ${data.weather[0].description}</p>
        `;

    }catch(error){
        document.getElementById("weather").innerHTML =
        `<p style="color:red;">${error.message}</p>`;
    }

}