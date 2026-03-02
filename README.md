# lab4-SD
Lab 4: API Consumption & DOM Manipulation
Objective

In this lab, you will learn how to consume external REST APIs and dynamically update the DOM using JavaScript. You will build a country information app that fetches data from the REST Countries API and displays it with proper styling and error handling.
Learning Outcomes

By the end of this lab, you will be able to:

    Fetch data from REST APIs using the Fetch API
    Parse JSON responses
    Dynamically update the DOM with JavaScript
    Handle asynchronous operations with async/await
    Implement error handling for API calls
    Apply CSS styling to dynamic content

Time Estimate

2.5 hours
Prerequisites

    Basic understanding of HTML, CSS, and JavaScript

Requirements
Part 1: Repository Setup

    Create a GitHub Repository named: <student-id>-lab4
        Example: 2345678-lab4
        Clone it to your local machine

    Create three files in the repository:
        index.html
        styles.css
        script.js

    Commit regularly as you work — aim for at least 3 meaningful commits

Part 2: HTML Structure

Your index.html must include these elements with the exact IDs specified:

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Country Explorer</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <h1>Country Explorer</h1>
    </header>

    <main>
        <div class="search-container">
            <input type="text" id="country-input" placeholder="Enter country name...">
            <button id="search-btn">Search</button>
        </div>

        <div id="loading-spinner" class="spinner"></div>

        <section id="country-info" class="country-card">
            <!-- Country info will be populated here -->
        </section>

        <section id="bordering-countries" class="border-grid">
            <!-- Bordering countries will be populated here -->
        </section>

        <div id="error-message" class="error"></div>
    </main>

    <script src="script.js"></script>
</body>
</html>

Required IDs:

    country-input - Text input for country name
    search-btn - Search button
    loading-spinner - Loading indicator
    country-info - Section for country details
    bordering-countries - Section for neighboring countries
    error-message - Error message display

Part 3: CSS Requirements

Your styles.css must include these required classes with specific CSS properties:
1. Loading Spinner (.spinner)

Must have a CSS animation:

.spinner {
    /* Your styling */
    animation: spin 1s linear infinite; /* Required */
}

@keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
}

2. Country Card (.country-card)

Must have visible styling (background, padding, etc.)
3. Border Grid (.border-grid)

Must use either CSS Grid or Flexbox:

.border-grid {
    display: grid; /* or display: flex */
    /* Additional layout properties */
}

4. Error Styling (.error)

Must have distinct styling to stand out:

.error {
    color: /* error color */;
    /* Additional styling */
}

5. Hidden State

Add a class to hide/show elements:

.hidden {
    display: none;
}

Part 4: JavaScript Functionality

Your script.js must implement:
1. API Fetching

Use the REST Countries API: https://restcountries.com/v3.1/name/{country}

// Example API call
const response = await fetch(`https://restcountries.com/v3.1/name/${countryName}`);
const data = await response.json();

2. Required Functionality

    Search trigger: Click button OR press Enter in input
    Loading state: Show spinner while fetching, hide when done
    Display country info:
        Country name
        Capital city
        Population (formatted with commas)
        Region
        Flag image
    Display bordering countries: Name and flag for each neighbor
    Error handling: Show user-friendly error messages

3. DOM Update Pattern

// Example DOM updates
document.getElementById('country-info').innerHTML = `
    <h2>${country.name.common}</h2>
    <p><strong>Capital:</strong> ${country.capital[0]}</p>
    <p><strong>Population:</strong> ${country.population.toLocaleString()}</p>
    <p><strong>Region:</strong> ${country.region}</p>
    <img src="${country.flags.svg}" alt="${country.name.common} flag">
`;

4. Code Structure

// Required: Use async/await OR .then() for API calls
// Required: Use try/catch OR .catch() for error handling

async function searchCountry(countryName) {
    try {
        // Show loading spinner
        // Fetch country data
        // Update DOM
        // Fetch bordering countries
        // Update bordering countries section
    } catch (error) {
        // Show error message
    } finally {
        // Hide loading spinner
    }
}

// Event listeners
document.getElementById('search-btn').addEventListener('click', () => {
    const country = document.getElementById('country-input').value;
    searchCountry(country);
});

Part 5: API Response Structure

The REST Countries API returns data in this format:

[
    {
        "name": {
            "common": "South Africa",
            "official": "Republic of South Africa"
        },
        "capital": ["Pretoria"],
        "population": 59308690,
        "region": "Africa",
        "borders": ["BWA", "LSO", "MOZ", "NAM", "SWZ", "ZWE"],
        "flags": {
            "svg": "https://flagcdn.com/za.svg",
            "png": ""
        }
    }
]

To get bordering country details, fetch by country code: https://restcountries.com/v3.1/alpha/{code}
Submission
Deliverables

    Git Bundle File
        Create a bundle of your repository:

        git bundle create <student-id>-lab4.bundle --all

        Submit the bundle file to Moodle
        File must be named exactly: <student-id>-lab4.bundle

    Deploy to GitHub Pages

    Demo your deployed site to a tutor before leaving the lab

Example Submission Filename

If your student ID is 2345678:

2345678-lab4.bundle

Evaluation Criteria

Your submission will be automatically marked:
HTML Structure (25 points)
Criteria 	Points
Bundle extracts successfully 	3
File index.html exists 	3
#country-input ID exists 	3
#search-btn ID exists 	3
#loading-spinner ID exists 	3
#country-info ID exists 	3
#bordering-countries ID exists 	3
#error-message ID exists 	4
CSS Requirements (25 points)
Criteria 	Points
File styles.css exists 	3
.spinner class exists 	4
.spinner has animation property 	6
.country-card class exists 	4
.border-grid class exists 	4
.border-grid uses grid or flex 	4
JavaScript Requirements (50 points)
Criteria 	Points
File script.js exists 	3
Uses fetch() API 	10
Uses async/await OR .then() 	10
Uses try/catch OR .catch() 	10
Uses getElementById or querySelector 	7
Updates DOM (innerHTML/textContent) 	10

Total: 100 points
Important Notes

    File names must be EXACTLY as specified
    HTML IDs must be EXACTLY as specified (case-sensitive)
    CSS class names must be EXACTLY as specified
    The REST Countries API is free and does not require authentication
    Handle the case where a country has no bordering countries (e.g., islands)

Tips for Success

    Test with different countries:
        Countries with borders: "South Africa", "Germany", "Brazil"
        Island nations (no borders): "Japan", "Australia"
        Invalid names: "Atlantis", "xyz123"

    Format population numbers:

    population.toLocaleString() // 59308690 → "59,308,690"

    Hide/show elements:

    element.classList.add('hidden');
    element.classList.remove('hidden');

    Debug in browser:
        Use console.log() to inspect API responses
        Check Network tab in DevTools for API calls

    API Documentation:
        https://restcountries.com/

Good luck!
