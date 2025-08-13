Cyber Data Endpoints
This repository contains structured JSON datasets representing categorized cyber-related information.
The purpose of this project is to organize and expose data in a clear, machine-readable format that can be consumed by applications, dashboards, and APIs.

📂 Data Files
attacks.json – Information about cyberattacks, including types, patterns, and details.

attributions.json – Data about attack attributions and responsible entities.

countries.json – List of countries involved or impacted.

initiatorCountries.json – Countries that initiated cyber activities or attacks.

initiatorTypes.json – Classification of entities initiating cyber actions (e.g., state actors, hacktivists, organizations).

keyInsights.json – Key insights and summarized intelligence derived from the dataset.

responses.json – Responses and countermeasures taken against attacks.

sectors.json – Industry sectors affected by cyber incidents.

🎯 Purpose
To store and manage structured cyber-related data for analysis and visualization.

To make datasets easily accessible for integration into websites, APIs, or GitHub Pages.

To serve as a reference point for research, academic projects, or security dashboards.

🌐 Usage
You can use these JSON files by fetching them directly via GitHub or GitHub Pages (if deployed).
Example (JavaScript fetch):

JavaScript >
`
fetch('https://your-username.github.io/cyber-data-endpoints/attacks.json')
  .then(response => response.json())
  .then(data => console.log(data));
`
📌 Notes
Data is stored in a clean JSON structure for ease of parsing.
This repository is designed to be scalable – more datasets can be added in the future.

