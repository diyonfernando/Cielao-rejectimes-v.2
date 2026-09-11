# Cielao-rejectimes-v.2

CIELAO is a student focused university application designed to make course information easier to access in one place. It allows students to search and filter courses, view course details and progress, save courses, and manage simple settings through a clean, modern interface.

Target domain: Education / University Student Productivity

Problem statement: Students need a simple place to access and search course information.

How CIELAO solves it: Course search, filtering, course details, progress display, settings, and navigation.

Main features: Splash screen, Home, Course Details, Settings, FlatList with 10 courses, search/filter, animated navigation. 

It connects to the supplied MockAPI Field resource and uses AsyncStorage for local persistence.

_**Changes Made in V2**_

REST API Integration

Replaced the original hard-coded course list with live MockAPI data.

Connected the app to https://6aa159b62703577aa1e393e8.mockapi.io/Field.

Added GET to load courses when the app starts.

Added pull-to-refresh using GET.

Added POST to create courses.

Added PUT to update existing courses.

Added DELETE with a confirmation alert.

Created a reusable request helper to send JSON and check HTTP status codes.

Added response normalization so missing optional fields do not crash the interface.

_**MockAPI Record Identifiers**_

The supplied resource returns its primary key as Field instead of the conventional id.

Added support for course.id, course.Field, and course.field.

Edit and Delete use /Field/{record identifier}.

_**Local Persistence**_

Added @react-native-async-storage/async-storage.

The latest successful API response is cached under @cielao/course-cache-v1.

Saved-course identifiers are stored under @cielao/saved-courses-v1.

Cached courses are restored when the API cannot be reached.

Added a Save Offline button and saved-course total in Settings.

_**User Interface and State Handling**_

Added a loading screen while API data is requested.

Added pull-to-refresh feedback.

Added empty states for an empty API and unmatched searches.

Added offline status messages with a Retry button.

Added a reusable Add and Edit course form.

Added required-field validation for course code, title, and lecturer.

Added progress validation from 0 to 100.

Added submission indicators to prevent repeated requests.

Preserved course search and the progress filter.

Added scrolling to the detail, form, and settings screens.

Updated the greeting to WELCOME BACK (USERS NAME).

_**Demonstration Sequence**_

Launch the app and allow it to load records from MockAPI.

If the API is empty, tap Add first course. Otherwise, tap Add.

Complete the form and create a record to demonstrate POST.

Pull down on the Home list to demonstrate GET.

Open the course, tap Edit, change its progress, and update it to demonstrate PUT.

Tap Save Offline, disable the connection, and reload to show cached data.

Restore the connection, open the course, and tap Delete to demonstrate DELETE.

**Project Structure**

App.js contains the screens, reusable components, API functions, AsyncStorage logic, state management, and styles.

assets/ contains the application images and fonts.

app.json contains the Expo application configuration.

package.json contains the SDK 57 dependencies and run commands.

CSI2114_Sprint_2_Technical_Summary.docx describes the architecture, REST integration, persistence, challenges, and design decisions.

_**API Data Fields**_

The app sends the following fields as JSON:

code

title

lecturer

time

room

progress

description

The MockAPI resource supplies its record identifier in the Field property. The app also supports the conventional id property.

Example response:

{
  "Field": "1",
  "code": "CSI2114",
  "title": "Mobile Application Development",
  "lecturer": "Semini Perera",
  "time": "Monday 9:00 AM",
  "room": "Lab 03",
  "progress": 70,
  "description": "React Native course"
}
