---
title: Design
has_children: false
nav_order: 4
---

# Design

## Architecture

The app Mete.io adopts a layered architecture structure. The reason behind this choice is the separation of concerns meaning that each layer has a specific responsibility. 

This has other beneficial effects like easier testing and maintenance but also simplifies future development.

Other architectures were evaluated but the Event-Based Architecture and the Shared Dataspace Architecture could add too much complexity to the system.

### Architectural overview
The system is structured into the following layers:

**Presentation Layer (User Interface)**

This layer reacts to user actions and displays data but contains no business logic. 

Responsibilities: user interaction and presentation logic.

Components:

- MeteioApp (main Kivy application);
- Screen components (e.g. MainScreen, ForecastScreen);
- UI widgets (buttons, indicators, dialogs).

**Application layer**

This layer handles business logic (access, interaction, update) and depends on the domain layer. 

Responsibilities: coordination of use cases and workflows.

Components:

- WeatherService;
- ForecastService;
- AlertService.

**Domain layer** 

This layer contains all the weather-related domain models.

Responsibility: representation of weather-related concepts and rules.

Components are Entities (WeatherReport, Forecast, Alert, Location) and Value objects (Coordinates, AccuracyLevel).

**Infrastructure layer** 

This layer handles communication with the external Open-Meteo API and local file storage.

Responsibility: technical concerns and external interactions with API.

Components:

- WeatherAPIClient;
- LocalLocationRepository;
- API adapters.

![UML Components diagram](/  ) 


## Infrastructure
Mete.io is a **non-distributed system**. All components run on the **user’s machine** and the external weather data is accessed through Open-Meteo API while the geolocalized position is stored locally.
## Modelling

The domain is simple and can be represented by a single bounded context called **Weather Information**.

Main domain concepts include:

- Entities: WeatherReport, Forecast, Alert, Location
- Value objects: Coordinates, AccuracyLevel
- Services: ForecastService, AlertService
- Repositories: LocalLocationRepository (for previously searched locations)


### Object-oriented modelling
Defined classes and responsibilities:
- **WeatherReport** represents current weather data
  - Attributes: temperature, humidity, wind_speed, wind_direction, cloud_coverage, events
  - Methods: none (data holder)
- **Forecast**: represents daily forecast and accuracy
  - Attributes: date, weather_report, accuracy_level
  - Methods: get_accuracy_description()
- **Alert**: represents weather warnings
  - Attributes: type, description, source_url
  - Methods: none
- **Location**: represents a geographic location
  - Attributes: name, latitude, longitude
  - Methods: __eq__, __repr__
- **WeatherAPIClient**: fetches data from external APIs
  - Methods: fetch_current_weather(), fetch_forecast(), fetch_alerts()
- **LocalLocationRepository**: manages local persistence
  - Methods: save(location), list_all()

![UML class diagrams](/ )

## Interaction
Components interact synchronously (components wait for call results, the control flow is linear):
- User Interface interacts with the Application layer via method calls


- Application layer interacts with the Infrastructure layer via service interfaces
- Infrastructure layer interacts with Open-Meteo APIs via HTTPS requests

An Example can be:
1. User selects a location
2. UI calls ForecastService.get_week_forecast(location)
3. Service calls API client
4. Response is returned
5. UI updates the screen

![UML sequence diagram](/ )

## Behaviour

All the components of the Presentation Layer are event-driven, the user inputs (e.g. pressing on the search bar) produce events that are sent to the application layer.

Most of the domain objects should be stateless, represent snapshots of data and typically not evolve over time.

The only stateful elements should be the ones related to UI (e.g. main screen, selected location) and the previously searched locations in the local storage.

Local storage is updated when locations are searched.

![UML UI state diagram](/ )

## Data-related aspects
Only previously searched locations need to be stored as persistent data. The type of storage is lightweight local storage as a key-value pair.

LocalLocationRepository performs all local storage queries. 

When the app is opened it loads saved locations, and when the user searches a new location it gets saved.

The types of queries are related to reading all the stored locations and appending new ones.

**Shared data between components**

The Location objects are shared between various components across presentation, application, and domain layers. They are immutable and represent a core domain concept.


**Integrity Pattern**

The system consists of a single bounded context, so most of the studied model integrity patterns should not be applicable.

The Anti-Corruption Layer pattern could be applied to prevent external model changes from propagating into the domain, preserving the integrity of the internal model.

The infrastructure layer isolates the internal domain model from the external weather provider’s data model by encapsulating API calls using an API adapter and translating external JSON responses into internal domain entities.

