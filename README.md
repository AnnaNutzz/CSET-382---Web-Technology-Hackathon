# CityPulse — Smart City Information Dashboard

CityPulse is an interactive, client-side smart city dashboard designed to provide real-time civic awareness, data visualization, and citizen engagement. It is built entirely with **vanilla HTML, CSS, and JavaScript**, simulating a modern urban data portal without any backend database or server.

This project focuses on usability, interactivity, and clear data presentation through a clean, responsive UI, with all data (alerts, weather, etc.) stored in static JavaScript arrays or objects.

-----

## 🚀 Features

The application simulates a Single Page Application (SPA) by dynamically showing and hiding four main views:

  * **1. Home Dashboard:**

      * Displays summarized city data (Temperature, AQI, Traffic) from preloaded JavaScript objects.
      * Features a dynamic SVG-based arc for the Air Quality Index (AQI) that changes color and length based on the value.
      * Includes a live-updating date and time clock.

  * **2. City Alerts & News:**

      * Renders a dynamic list of simulated civic alerts (e.g., Traffic, Health, Weather).
      * Includes JavaScript-powered filtering by alert type and sorting by date or type.
      * Clicking an alert opens a custom modal for more details.

  * **3. Interactive City Map:**

      * Uses an SVG-based map divided into clickable zones (Parks, Hospitals, Schools, Malls).
      * Hover animations highlight zones using CSS and JavaScript.
      * Clicking a zone triggers a custom modal popup with zone-specific information.

  * **4. Feedback & Citizen Connect:**

      * Provides a contact form for users to submit feedback.
      * Features robust, client-side form validation for Name, Email, and Message fields using JavaScript.
      * On successful validation, a custom popup confirms the (simulated) submission.

-----

## 🛠️ Technology Stack & Constraints

This project was built adhering to specific technical requirements:

  * **Technologies:**

      * **HTML5:** For semantic structure.
      * **CSS3:** For all styling, layout (Flexbox/Grid), and animations.
      * **JavaScript (ES6+):** Vanilla JavaScript is used for *all* dynamic behavior, including DOM manipulation, event listeners, view-switching, and form validation.

  * **Key Constraints:**

      * **No Backend:** The project is 100% client-side. All data is static and stored in JavaScript arrays or objects within the HTML file.
      * **No `alert()` / `confirm()`:** A primary requirement was to avoid native browser popups. All modals and notifications are custom-built HTML/CSS overlays controlled by JavaScript.
      * **Single-File Deployment:** The entire application (HTML, CSS, and JS) is contained within a single `CityPulse.html` file, making it extremely portable and easy to deploy on any static host (like GitHub Pages).

-----

## ⚙️ How to Use

There is no installation or build process required.

1.  Download the `CityPulse.html` file.
2.  Open the file in any modern web browser (e.g., Chrome, Firefox, Edge).

That's it\! The dashboard is fully functional locally.

-----

## 💡 Code Highlights

The project's interactivity is powered by lightweight, vanilla JavaScript functions.

### SPA-like View Switching

A single function manages which "view" is active by toggling its `display` style, simulating a multi-page application.

```javascript
// From CityPulse.html
function setView(name){
  $$('.view').forEach(v=>v.style.display='none');
  $('#view-'+name).style.display='block';
  $$('#nav .nav-btn').forEach(b=>b.classList.toggle('active', b.dataset.view===name));
}
```

### Custom Modal Logic

This code controls the custom HTML overlay, fulfilling the "no alert()" requirement.

```javascript
// From CityPulse.html
const overlay = $('#overlay');
function openModal(title, html){
  $('#modal-title').textContent = title;
  $('#modal-body').innerHTML = html;
  overlay.classList.add('show');
}
function closeModal(){
  overlay.classList.remove('show');
}
```

### Client-Side Form Validation

The contact form uses an event listener to prevent default submission and run custom validation logic, displaying errors directly in the DOM.

```javascript
// From CityPulse.html
$('#contact-form').addEventListener('submit', (e)=>{
  e.preventDefault();
  let ok = true;
  // ...
  if(!/^\S+@\S+\.\S+$/.test(email)){
    $('#err-email').textContent='Please enter a valid email.';
    $('#err-email').style.display='block';
    ok=false;
  }
  // ...
  if(!ok) return;

  openModal('Message sent', ...); // Show custom success modal
});
```
