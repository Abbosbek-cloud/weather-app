# 🌤️ Weather App

A beautiful and responsive weather application built with vanilla JavaScript that fetches real-time weather data from the OpenWeatherMap API. The app features an elegant UI with a dynamic background and smooth transitions.

![Weather App Preview](img/page-example.png)

## 📋 Table of Contents

- [Features](#features)
- [Demo](#demo)
- [Technologies Used](#technologies-used)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [API Reference](#api-reference)
- [Code Explanation](#code-explanation)
- [Responsive Design](#responsive-design)
- [Contributing](#contributing)
- [License](#license)

## ✨ Features

- 🔍 **City Search**: Search for weather information by city name
- 🌡️ **Real-time Data**: Fetches current temperature, weather conditions, and temperature ranges
- 📅 **Date Display**: Shows current date and day automatically
- 🎨 **Beautiful UI**: Gradient overlay with backdrop image for aesthetic appeal
- 📱 **Responsive Design**: Works seamlessly on desktop, tablet, and mobile devices
- ⚡ **Fast Performance**: Lightweight vanilla JavaScript implementation
- 🌈 **Dynamic Weather Descriptions**: Displays weather conditions based on temperature

## 🚀 Demo

To see the app in action:
1. Open `index.html` in your browser
2. Type a city name in the search bar
3. Press Enter or Space to fetch weather data

## 🛠️ Technologies Used

- **HTML5**: Semantic markup structure
- **CSS3**: Modern styling with gradients, transitions, and flexbox/grid layouts
- **JavaScript (ES6+)**: Vanilla JS for API calls and DOM manipulation
- **OpenWeatherMap API**: Weather data provider

## 📁 Project Structure

```
weather-app/
│
├── img/
│   ├── hd_bg.jpg           # Background image
│   └── images.md           # Image documentation
│
├── scripts/
│   └── script.js           # Main JavaScript file
│
├── styles/
│   └── style.css           # Stylesheet
│
├── index.html              # Main HTML file
└── README.md               # Project documentation
```

## 📥 Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/Abbosbek-cloud/weather-app.git
   cd weather-app
   ```

2. **Open in your preferred code editor**
   ```bash
   code .
   ```

3. **Open with a local server** (recommended)
   - Using VS Code Live Server extension
   - Or simply open `index.html` in your browser

## ⚙️ Configuration

### API Key Setup

The app uses OpenWeatherMap API. The current API key is included in the code:

```javascript
const api = {
  key: "16844946433fae1fa6bf480e010132d9",
  baseApi: "https://api.openweathermap.org/data/2.5/",
};
```

**⚠️ Security Note**: For production use, you should:
1. Get your own API key from [OpenWeatherMap](https://openweathermap.org/api)
2. Store it in environment variables or a config file
3. Never commit API keys to public repositories

### Getting Your Own API Key

1. Visit [OpenWeatherMap](https://openweathermap.org/api)
2. Sign up for a free account
3. Navigate to API Keys section
4. Generate a new API key
5. Replace the key in `scripts/script.js`

## 💡 Usage

### Basic Usage

1. **Search for a city**: Type the city name in the search bar
2. **Submit**: Press `Enter` or `Space` key
3. **View results**: Weather information updates instantly

### Example Cities to Try

- London
- New York
- Tokyo
- Paris
- Sydney
- Moscow

## 🌐 API Reference

The app uses OpenWeatherMap's Current Weather Data API:

**Endpoint**: `https://api.openweathermap.org/data/2.5/weather`

**Parameters**:
- `q`: City name (e.g., "London", "New York")
- `units`: Temperature unit (metric for Celsius)
- `appid`: Your API key

**Response Example**:
```json
{
  "name": "London",
  "sys": {
    "country": "GB"
  },
  "main": {
    "temp": 15.5,
    "temp_min": 13.0,
    "temp_max": 18.0
  },
  "weather": [
    {
      "description": "clear sky"
    }
  ]
}
```

## 📝 Code Explanation

### HTML Structure

The HTML file contains:
- **Main section**: Displays weather information (city, date, temperature, conditions)
- **Header section**: Contains the search input field
- **Grid layout**: 50/50 split for main content and search bar

### CSS Styling

Key styling features:
- **Grid Layout**: Uses CSS Grid for responsive layout
- **Background**: Full-screen background image with gradient overlay
- **Input Styling**: Custom search bar with focus effects
- **Responsive**: Media query for mobile devices (< 900px)

```css
.app_wrapper {
  display: grid;
  grid-template-columns: 50% 50%;
  background-image: linear-gradient(...);
}
```

### JavaScript Functionality

#### 1. **Event Listener**
```javascript
searchBox.addEventListener("keypress", (e) => {
  if (e.which == 13 || e.which == 32) {
    getResult(search.value);
  }
});
```
Listens for Enter (13) or Space (32) key presses.

#### 2. **API Fetch Function**
```javascript
function getResult(q) {
  fetch(`${api.baseApi}weather?q=${q}&units=metric&appid=${api.key}`)
    .then((weather) => weather.json())
    .then(displayResult);
}
```
Fetches weather data using the Fetch API and handles the response.

#### 3. **Display Function**
```javascript
function displayResult(weather) {
  // Updates DOM elements with weather data
  city.innerHTML = `${weather.name}, ${weather.sys.country}`;
  temperature.innerHTML = `${Math.round(weather.main.temp)}℃`;
  // ... more updates
}
```
Updates the UI with fetched weather information.

#### 4. **Weather Description Logic**
```javascript
if (weather.main.temp < 0) {
  description = "Cold";
} else if (tem > 0 || tem < 10) {
  description = "Cloudy";
} else if (tem > 10 || tem < 20) {
  description = "Wet";
} else {
  description = "Sunny";
}
```
**Note**: There's a logic issue here. The conditions should use `&&` (AND) instead of `||` (OR).

**Suggested fix**:
```javascript
if (tem < 0) {
  description = "Cold";
} else if (tem >= 0 && tem < 10) {
  description = "Cloudy";
} else if (tem >= 10 && tem < 20) {
  description = "Wet";
} else {
  description = "Sunny";
}
```

#### 5. **Date Builder Function**
```javascript
function dateBuilder(a) {
  let months = ["January", "February", ...];
  let days = ["Sunday", "Monday", ...];
  
  return `${day} ${date} ${month} ${year}`;
}
```
Formats the current date in a readable format.

## 📱 Responsive Design

The app adapts to different screen sizes:

- **Desktop (> 900px)**: Two-column grid layout
- **Mobile (< 900px)**: Single-column stacked layout

```css
@media only screen and (max-width: 900px) {
  .app_wrapper {
    grid-template-columns: 100%;
  }
}
```

## 🔧 Potential Improvements

### 1. **Code Quality**
- Fix the weather description logic (use `&&` instead of `||`)
- Add error handling for failed API requests
- Add loading states while fetching data
- Fix typo: "Novermber" → "November"

### 2. **Features**
- Add 5-day weather forecast
- Display weather icons
- Add geolocation for automatic city detection
- Include humidity, wind speed, and pressure data
- Add temperature unit toggle (Celsius/Fahrenheit)
- Implement autocomplete for city search

### 3. **Security**
- Move API key to environment variables
- Add rate limiting for API calls

### 4. **UX Improvements**
- Add animations for weather data updates
- Include error messages for invalid city names
- Add placeholder data before first search
- Implement dark/light mode toggle

## 🐛 Known Issues

1. **Weather Description Logic**: The conditional operators in the `displayResult` function use `||` (OR) when they should use `&&` (AND)
2. **Typo**: "Novermber" in the months array should be "November"
3. **No Error Handling**: App doesn't handle invalid city names or network errors
4. **API Key Exposure**: API key is hardcoded in the client-side code

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 👨‍💻 Author

**Your Name**
- GitHub: [@Abbosbek-cloud](https://github.com/Abbosbek-cloud)
- Email: abek01sulaymonov@gmail.com

## 🙏 Acknowledgments

- Weather data provided by [OpenWeatherMap](https://openweathermap.org/)
- Background image from [source]
- Inspired by modern weather app designs

## 📞 Support

For support, email abek01sulaymonov@gmail.com or open an issue in the repository.

---

**Made with ❤️ and JavaScript**