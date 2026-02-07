---
title: Requirements
has_children: false
nav_order: 3
---

# Requirements


## User stories

**As a** worker **I want to** know the weather for this week **so that** I can plan my outfit accordingly and schedule meetings based on that information.

**As a** sport enthusiast **I want to** know the weather for next week **so that** I can choose the best day to plan activities.

**As a** person, **I want to** receive alerts about extreme weather events **so that** I can stay safe.

## Requirements analysis

The Mete.io application had the following requirements:

### Functional:

1 - **Location-based indicators**

**Requirement**: When the user opens the application it should display primary indicators based on the user’s location when geolocation permissions have been granted.

**Acceptance criteria**:
- when the user opens the app for the first time it requests geolocation permissions that the user can agree to or refuse;

- if the user agrees, the app displays primary indicators for that position (temperature, humidity, wind speed and direction, cloud formation and atmospheric events);

- if the user disagrees, the app displays a search bar to type a specific location and an icon on the upper left side of the screen to repeat the permission request.


2 - **Secondary indicators**

**Requirement**: Implementation of secondary indicators (e.g. air quality and pollen) that the user can choose to display.

**Acceptance criteria**: 

- when the app is first opened the secondary indicators are not visible as default configuration;

- clicking the “+” icon on the main screen allows to select the secondary indicators;

- the chosen ones will appear on the main page alongside the main indicators.


3 - **Forecast and accuracy indication**

**Requirement**: The user should be able to see the weather forecast for up to a week. Forecasts tend to be less accurate after 72 hours, colored dots should be used to indicate the level of accuracy.

**Acceptance criteria**: 
- when the user opens the forecast they should see it for the next 7 days;

- for each day there should be a colored dot (green or red) representing the forecast’s accuracy;

- when the colored dot is clicked it should show a description of the accuracy (green with accuracy higher than 95% while red with accuracy lower or equal to 95%).


4 - **Choice of location**

**Requirement**: Provide the option to change the geographic location for the weather of a different region. Store previously selected locations in the past and show them to the user as possible options.

**Acceptance criteria**: 
- when the user selects the search bar on top of the screen, they should be able to see previously searched locations as suggested options;

- when the user selects the search bar on top of the screen, they should be able to type in a location of interest;

- once the user has chosen the location, the main page indicators and the forecast should be displayed for that location.


5 - **Alerts**

**Requirement**: Show warnings for possible extreme events (e.g. heat wave, flood, heavy thunderstorm, volcanic eruptions) and an icon to be redirected to the official website of the organization issuing the alert.

**Acceptance criteria**: 
- in case of warnings issued for the currently selected location, there should be an alert on the main screen;

- when the user clicks on the alert, they should be redirected to the webpage of the official institution that has issued the warning for more information.


### Non-functional:

1 - **Performance**

**Requirement**: The app should respond to the user’s actions quickly, without noticeable delays.

**Acceptance criteria**: 
- the main screen should load within 2 seconds under assumption of normal network conditions;
- weather data should update within 3 seconds after a location change.


2 - **Usability**

**Requirement**: The application should be easy to understand and use.

**Acceptance criteria**: 
- primary indicators should be visible without required actions;
- icons should be clear and understandable for users.


3 - **Privacy and Security**

**Requirement**: The application should protect the user’s personal data and securely handle external connections.

**Acceptance criteria**: 
- location data should be used only to provide weather information;
- location data should not be stored or shared without the user’s consent;
- all data requests should be made using secure connections (HTTPS).


4 - **Compatibility**

**Requirement**: The app should work across common devices and operating systems.

**Acceptance criteria**: 
- the application runs correctly on Windows 10+ (choice based on market share analysis worldwide);
- the UI adapts to different screen sizes.


5 - **Availability and reliability**

**Requirement**: The app should be available and provide consistent data.

**Acceptance criteria**: 

- in case of data fetching failure, the user is informed by an error message.


### Implementation:

1 - **Programming language**

**Requirement**: The app should be developed using Python and Kivy.

**Acceptance criteria**: 
- Python should be used for the backend;
- Kivy should be used for the GUI.


2 - **External services**

**Requirement**: The app should use external APIs to retrieve weather data.

**Acceptance criteria**: 
- data should be obtained from Open–Meteo, a public weather API.


3 - **Data storage**

**Requirement**: The app should store local data efficiently.

**Acceptance criteria**: 
- previously searched locations should be stored locally;
- stored data is deleted when the app is uninstalled.


### Glossary:

**Primary indicators** - basic weather parameters such as temperature, humidity, wind speed and direction.

**Secondary indicators** - optional indicators such as air quality or pollen levels.

**Forecast accuracy** - an estimation of how reliable a forecast is, expressed through color-coded indicators.

**Geolocation** - automatic detection of the user’s geographic position.

