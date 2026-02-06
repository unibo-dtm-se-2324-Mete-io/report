---
title: Validation
has_children: false
nav_order: 6
---

# Validation

## Testing approach

Mete.io followed Test Driven Development (TDD) and unittest was chosen for testing.

Test Driven Development focuses on the idea of transforming requirements’ acceptance criteria into tests before development, to make sure the requirements are clearly verifiable.

It is possible to test software at different levels of granularity like: **Unit testing** (single component), **Integration testing** (multiple components and their expected interaction), **System testing** (system as a whole) and **Acceptance testing** (validation of requirements from the users’ perspective).

Using a combination of all these tests allows to have control over every component and reduces the resources needed to fix problems in the code.

All the testing files need to be in a separate directory with its own dependencies, following python project conventions.

## Testing (Automated)

### Unit testing

Unit tests are used to validate the isolated behaviour of each unit to make sure it fulfills its responsibility.

The acceptance criteria can be used to shape the test cases to have a clear view of all the potential behaviours, then domain constraints (valid ranges for weather values) and edge cases (missing/invalid input) need to be considered.

The testing can be defined before the actual programming by using test doubles and shaping them based on the classes that will be implemented later. Mocks or stubs can replace external inputs (Open-Meteo) so that tests can run without network access.

The test coverage should cover all possible identified classes.

Example unit tests (conceptual descriptions):

**Forecast accuracy classification**

Component tested: **Forecast**

Scenario 1: forecast attribute “date” is 1-3 days ahead (estimated accuracy >95%)

Expected behaviour 1: attribute “accuracy_level” is “green”

Scenario 2:  forecast attribute “date” is 4-7 days ahead (estimated accuracy <95%) 

Expected behaviour 2: attribute “accuracy_level” is “red”

The accuracy logic could possibly be implemented with the “datetime” python module, using datetime.date as forecast date, date.today() as the current date and timedelta.days for the difference between the two (less than 3 / more or equal to 4).

Purpose: validates business logic for accuracy thresholds


**ForecastService weekly forecast generation**

Component tested: **ForecastService**

Scenario: service receives 7 daily weather entries

Expected behaviour: exactly 7 Forecast objects are returned

Purpose: validates correct handling of weekly forecasts


**Location validation**

Component tested: **Location**

Scenario 1: invalid coordinates (“latitude” attribute absolute value > 90)

Expected behaviour 1: error message

Scenario 2: invalid coordinates (“longitude” attribute absolute value > 180)

Expected behaviour 2: error message

Purpose: enforces domain constraints

### Integration testing

Integration tests validate the correct interaction between components.

It is possible to use the previously shown diagrams to have a precise overview of the system and evaluate all the possible interactions between components.

Example integration tests (conceptual descriptions):

**ForecastService + WeatherAPIClient**

Components involved:
- ForecastService
- WeatherAPIClient (mocked HTTP responses)

Scenario: Weather API returns valid JSON forecast data

Expected behaviour: Data is correctly transformed into domain Forecast objects

Purpose: validates that API data mapping and service logic work together


**Application services + LocalLocationRepository**

Components involved:

- Application services (location search logic)
- LocalLocationRepository

Scenario: User searches for a new location, then selects the search bar again

Expected behaviour: Location is added to the LocalLocationRepository, then Location appears in suggested search options

Purpose: validates persistence integration

**UI controller + ForecastService**

Components involved:

- UI controller (logic only)
- ForecastService

Scenario: User selects a different location (clicks on the searchbar widget - enters/selects the location)

Expected behaviour: UI controller requests updated forecast from the ForecastService

Purpose: validates correct coordination between UI logic and application logic

### System testing

System tests validate the overall behaviour of the application end-to-end (input to output) covering main use cases.

The system testing should be modeled based on the acceptance criteria present in the requirements.

Containerization with Docker could be implemented to run tests in a clean, reproducible environment with standardized installation.

Example system tests (conceptual descriptions):

**App startup with geolocation enabled**

Scenario: User opens the app and grants geolocation permission

Expected behaviour: Primary weather indicators are displayed for the determined Location

Requirement covered: Functional requirement 1

**Weekly forecast visualization**

Scenario: User opens ForecastScreen

Expected behaviour: Forecast displayed for 7 days, each day has an accuracy indicator

Requirement covered: Functional requirement 3

**Extreme weather alert**

Scenario: API reports a severe weather warning

Expected behaviour: Alert is visible on MainScreen, clicking on the alert opens the official source website

Requirement covered: Functional requirement 5

## Acceptance test (manual)

Acceptance tests validate that the system meets the requirements from the users’ perspective.

Each requirement has at least one corresponding acceptance test validating its acceptance criteria.

Since Mete.io has a graphical user interface, some aspects would be more effectively validated manually, such as:
- UI usability;
- navigation between screens;
- indicators and icons being visually correct;
- error communication to the user.

All tests would be repeatable following documented steps.

Manual acceptance tests examples:

**Secondary indicators selection**

Steps:

1. Open the application

2. Click the “+” icon

3. Select the air quality indicator

4. Expected result: the air quality indicator appears on MainScreen

5. Requirement covered: Functional requirement 2

**Location search**

Steps:

1. Click the search bar widget

2. Type in a location name

3. Select a result (corresponding to a Location object)

Expected result: MainScreen updates, showing weather indicators for the selected Location

Requirement covered: Functional requirement 4

The acceptance test would be considered successful if all acceptance criteria for the corresponding requirements are satisfied and no functional issues arise.

