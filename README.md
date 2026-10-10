# ICE Task 4 - Weather Dashboard UI 

## 1. Introduction
The Weather Dashboard application is a React Native mobile application designed to display hardcoded meteorological information for three major cities in South Africa (Johannesburg, Cape Town, and Durban). The application features dynamic city selection, real-time hero background updates, current weather details, a horizontal 24-hour forecast, a detailed 5-day forecast grid, and sun/moon astronomical data.

## 2. Development Environment
The application was developed, debugged, and tested within the following environment:
* **Expo**: Framework used for building and running the React Native application.
* **React Native**: Cross-platform mobile framework utilized for UI components.
* **TypeScript**: Typed superset of JavaScript used to ensure strong type safety.
* **Institutional VM**: The virtualized workstation environment used for development.
* **BlueStacks 5**: The Android emulator environment initially intended for hosting and running the mobile app.
* **Expo Go**: The mobile client used to load and preview the application.

## 3. Error Log
The following table documents the errors identified and corrected within `App.tsx`:

| # | Location | Problem Description | Error Classification | Correction Description |
|---|---|---|---|---|
| 1 | `App.tsx` | City selection buttons checked and updated state using `weather.country` instead of `weather.city`. | Logic & State Selection | **What was wrong:** Buttons compared and set state against the country name (`South Africa`) rather than the unique city names (`Johannesburg`, etc.).<br>**Why it was wrong:** Since all three cities share the same country string, selecting any button failed to switch the active weather data.<br>**What I changed:** Updated both selection conditional checks and `setSelectedCity` calls to use `weather.city`. |
| 2 | `App.tsx` | Humidity display card rendered `selectedWeather.feelsLike` instead of humidity data. | Data Presentation | **What was wrong:** The humidity detail component displayed the feels-like temperature value instead of the humidity percentage.<br>**Why it was wrong:** Incorrect variable binding passed to the UI component property.<br>**What I changed:** Changed the value binding to `{`${selectedWeather.humidity}%`}`. |
| 3 | `App.tsx` | The 24-hour forecast ScrollView was configured with `horizontal={false}`. | Layout & Scrolling | **What was wrong:** The hourly forecast cards were stacked vertically instead of scrolling horizontally across the screen.<br>**Why it was wrong:** Violates the design specification for a side-scrolling hourly timeline.<br>**What I changed:** Changed `horizontal={false}` to `horizontal={true}`. |
| 4 | `App.tsx` | Hourly forecast loop displayed the main current temperature for every hour card. | Data Presentation | **What was wrong:** Every hourly card showed `{selectedWeather.temperature}°` statically.<br>**Why it was wrong:** Failed to map each individual hour's specific temperature from the array.<br>**What I changed:** Updated the expression to `{hour.temperature}°`. |
| 5 | `App.tsx` | The 5-day forecast `.map()` loop was missing an explicit `return` statement inside its block. | Syntax & Array Rendering | **What was wrong:** Using curly braces `{}` inside the array map function without returning rendered nothing on the screen.<br>**Why it was wrong:** JavaScript arrow functions require either an explicit `return` keyword or implicit parentheses wrapping the JSX.<br>**What I changed:** Wrapped the daily card JSX in parentheses for proper implicit rendering. |
| 6 | `App.tsx` | High and low temperatures in the 5-day forecast grid were swapped. | Data Presentation | **What was wrong:** The low temperature was displayed where the high temperature belonged, and vice versa.<br>**Why it was wrong:** Incorrect layout ordering of variables inside the daily card view.<br>**What I changed:** Reordered the elements to display high temperature first followed by low temperature. |
| 7 | `App.tsx` | Sunrise and sunset sun-moon cards both displayed `selectedWeather.sunset`. | Data Presentation | **What was wrong:** The sunrise detail card incorrectly outputted sunset data.<br>**Why it was wrong:** Property duplication oversight during data mapping.<br>**What I changed:** Updated the sunrise card value to reference `selectedWeather.sunrise`. |
| 8 | `App.tsx` | `WeatherDetail` component displayed `{label}` twice instead of `{value}`. | Component Properties | **What was wrong:** Both detail label and detail value text fields rendered the label string.<br>**Why it was wrong:** Typo in the helper component's return statement.<br>**What I changed:** Updated the value text container to render `{value}`. |
| 9 | `App.tsx` | `detailItem` width was set to `'100%'` in a wrap container, causing single-column stacking. | Styles & Layout | **What was wrong:** Current weather details stacked vertically in a single narrow column.<br>**Why it was wrong:** The container uses `flexWrap: 'wrap'`, requiring a width like `'48%'` for proper two-column grid layout.<br>**What I changed:** Changed width from `'100%'` to `'48%'` alongside a missing stylesheet comma fix. |

## 4. Testing
The corrected application was tested under the following scenarios:
* **City Selection Testing**: Tested switching between Johannesburg, Cape Town, and Durban. Verified that the background image, city name, country, current temperature, condition icon, and all associated weather details updated instantly and accurately.
* **Forecast Testing**: Verified that the 24-hour forecast scrolls smoothly horizontally and displays unique hourly temperatures, and that the 5-day forecast grid correctly renders day names, icons, conditions, and high/low temperatures.
* **Sun & Moon / Additional Details Testing**: Confirmed that sunrise, sunset, moonrise, moonset, moon phase, humidity, wind speed/direction, pressure, visibility, and UV index sections display properly formatted data.

## 5. Screenshot

*(Note: BlueStacks App Player encountered unexpected loading and resolution issues during testing, so Expo Snack was utilized to successfully verify and capture the completed interface performance.)*

## 6. Conclusion
Investigating and correcting the Weather Dashboard application provided valuable practical experience in identifying debugging errors across TypeScript logic, component property binding, array rendering syntax, and React Native StyleSheet layouts. Successfully resolving these issues ensured that all user interface sections function cohesively and deliver accurate data representation.
