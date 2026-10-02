# Route Closure Check 🛣️

**Route Closure Check** is a web-based application designed to help drivers navigate England's strategic road network (motorways and main A-roads) by checking for planned road closures along their route. 

By inputting an origin, destination, vehicle type, and departure time, the app calculates the route and cross-references estimated arrival times at specific road segments with the official National Highways road closure reports.

---

## Features

* **Intelligent Routing:** Utilizes OpenStreetMap (OSRM) to calculate accurate driving routes.
* **Vehicle-Specific Estimates:** Adjusts estimated average speeds based on vehicle type (Car, Van, HGV) to accurately predict when you will arrive at specific points on the route.
* **Smart Closure Matching:** 
  * Extracts main roads (e.g., M1, A1(M)) from the routing data.
  * Calculates the heading/bearing of travel to filter closures by direction (Northbound, Southbound, etc.).
  * Compares your segment arrival time against the start and end times of planned closures.
* **Multilingual Interface:** Fully localized in English, Persian (Farsi - with RTL support), and Italian.
* **Offline/Manual Fallback:** Includes a manual `.xlsx` file upload feature to bypass strict CORS policies on the National Highways website.
* **Sleek UI:** A responsive, dark-mode "tarmac" aesthetic that mimics UK highway signage.

---

## How It Works (Under the Hood)

1. **Geocoding:** The app uses the **Nominatim API** to convert your origin and destination addresses into GPS coordinates.
2. **Routing:** The coordinates are sent to the **OSRM API** (Project OSRM), which returns turn-by-turn navigation steps, distances, and durations.
3. **Data Parsing:** The app scans the route steps for recognized UK motorways and A-roads using regular expressions (`/\b([AM]\d+[A-Z]?(?:\(M\))?)\b/g`).
4. **Data Cross-Referencing:** Using **SheetJS (xlsx)**, the app parses the National Highways planned closures Excel spreadsheet (`closures.xlsx`) and cross-references the time you are expected to be on a specific road with the schedule of the closure.

---

## Setup & Installation

Because the application relies on fetching external APIs and local files, it must be run through a local web server (opening the HTML file directly in the browser via `file://` will cause CORS/fetch errors).

1. Clone or download the repository.
2. Ensure you have the required directory structure
