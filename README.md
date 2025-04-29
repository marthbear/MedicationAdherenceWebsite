# Medication Adherence Web App

A lightweight, responsive web application to help patients track their medication adherence and for providers to manage prescriptions, view patient feedback, and monitor dosing schedules. Built with plain HTML/CSS/JavaScript and Firebase for authentication & data storage.

---

## Table of Contents

1. [Features](#features)  
2. [Tech Stack](#tech-stack)  
3. [Project Structure](#project-structure)  
4. [Prerequisites](#prerequisites)  
5. [Installation & Setup](#installation--setup)  
6. [Usage](#usage)  
   - [Styling (med-style.css)](#styling-med-stylecss)  
   - [Patient Views](#patient-views)  
   - [Provider Views](#provider-views)  
   - [LocalStorage Demo Page](#localstorage-demo-page)  
7. [Folder Layout](#folder-layout)  
8. [Contributing](#contributing)  
9. [License](#license)  

---

## Features

- **User Authentication** (Firebase)  
  - Email/password sign-up and login for **patients** and **providers**  
  - Role-based routing (patient dashboard vs provider dashboard)

- **Patient Dashboard**  
  - **Adherence Tracker**: calendar view with daily “med-box” pills; click to mark taken  
  - **Medication Feedback**: patients can view or submit simple feedback forms  
  - Styled modal to see prescription details and “Mark as Taken” button

- **Provider Dashboard**  
  - **Link Patients** by email (manual search + Firestore subcollection)  
  - **Create Prescriptions**: set start/end dates, dose times; Firestore stores doseDates & takenDates arrays  
  - **View Patient Feedback**: per-prescription “patientFeedback” in cards

- **Reusable Styles** (`med-style.css`)  
  - Reset & box-sizing, full-height background, container cards  
  - Form controls, buttons, link-buttons, cards & modals, calendar table, portal layout  
  - Utility classes: `.hidden`, `.status-message`, progress bars, `.med-box`

- **LocalStorage Demo**  
  - Simple static page (`MedicationAdherenceWebsite.html`) showing how prescriptions can be stored & read from `localStorage` without Firebase.

---

## Tech Stack

- **Frontend**:  
  - HTML5  
  - CSS3 (custom stylesheet `med-style.css`)  
  - Vanilla JavaScript (ES modules)  

- **Backend & Auth**:  
  - Firebase Authentication (email/password)  
  - Firestore (NoSQL document database)

- **Hosting / Dev**:  
  - Serve statically (e.g. GitHub Pages, Firebase Hosting, any static-file server)  
  - No build tools required

---

## Project Structure

├── assets/ │ └── med-bg.jpg # Background image for pages ├── med-style.css # Centralized stylesheet ├── index.html # Landing page (portal to patient/provider) ├── ProviderLogin.html # Provider sign-in ├── CreateProviderAccount.html # Provider sign-up ├── ProviderDashboard.html # Main provider UI ├── ProviderMedicationAdherenceWebsite.html │ # LocalStorage demo for providers ├── PatientLogin.html # Patient sign-in ├── CreatePatientAccount.html # Patient sign-up ├── PatientDashboard.html # Main patient UI ├── Adherence.html # Patient calendar tracker ├── PatientMedFeedback.html # Patient feedback form / view └── README.md # This file



---

## Prerequisites

1. **Firebase Project**  
   - Enable **Authentication** (Email/Password)  
   - Enable **Firestore** in test or locked mode  
   - Obtain your Firebase config object

2. **Local Server** (optional but recommended)  
   - `npm install -g http-server` & run `http-server`  
   - Or use Python: `python -m http.server 8000`

---

## Installation & Setup

1. **Clone the repo**  
   ```bash
   git clone https://github.com/your-username/med-adherence-webapp.git
   cd med-adherence-webapp

2. **Add Firebase config**
In every <script type="module"> block, replace the firebaseConfig placeholder with your own:
```javascript
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_AUTH_DOMAIN",
  projectId: "YOUR_PROJECT_ID",
  // …etc.
};
```


3. **Place assets/ folder**
Ensure assets/med-bg.jpg sits alongside your HTML files or update background-image: url(...) in med-style.css accordingly.

4. **Serve the files**
http-server .        # or python -m http.server
open http://localhost:8080/  # or :8000

## Usage
Styling (med-style.css)

    Provides a reset, container card layout, portal section for links, forms, buttons, cards, modals, and a responsive calendar.

    All pages share the same look & feel; simply include:
<link rel="stylesheet" href="med-style.css">
    
        in the <head> of each HTML file.
    
        The CSS is modular and can be easily adapted for other projects.

### Patient Views

#### `PatientLogin.html`
- Sign in or navigate to `CreatePatientAccount.html`.

#### `PatientDashboard.html`
- Two buttons at the top:
    - **View Adherence Tracker** → Navigates to `Adherence.html`.
    - **Medication Feedback** → Navigates to `PatientMedFeedback.html`.
- Calendar displays days with colored `.med-box` pills; clicking a pill opens a modal.

#### `Adherence.html`
- Dedicated calendar-only view, similar to the dashboard.

#### `PatientMedFeedback.html`
- Form or list for patients to leave or view feedback on prescriptions.

---

### Provider Views

#### `ProviderLogin.html` / `CreateProviderAccount.html`
- Sign in or sign up for providers.

#### `ProviderDashboard.html`
- **Link Patient**: Search by email and store under `users/{providerUID}/linkedPatients/`.
- **Your Patients List**: Select a patient to display:
    - **Prescription Section**: Create new prescriptions.
    - **Feedback Section**: View patient comments.

#### `ProviderMedicationAdherenceWebsite.html`
- LocalStorage demo for Rx entry and dose tracking without Firebase.

---

### LocalStorage Demo Page

#### `MedicationAdherenceWebsite.html`
- Simple client-side demo storing a prescriptions array in browser `localStorage`.
- Useful as a prototype before integrating Firebase.

## Folder Layout

```plaintext
│   README.md
│   
└───Medication Adherence System
    │   .firebaserc
    │   .gitignore
    │   Adherence.html
    │   CreatePatientAccount.html
    │   CreateProviderAccount.html
    │   firebase.json
    │   med-style.css
    │   Medication Adherence UML diagram.pdf
    │   MedicationAdherence.js
    │   MedicationAdherenceWebsite.html
    │   MedicationAdherenceWebsiteLogin.html
    │   PatientDashboard.html
    │   PatientLogin.html
    │   PatientMedFeedback.html
    │   ProviderDashboard.css
    │   ProviderDashboard.html
    │   ProviderLogin.html
    │   ProviderMedicationAdherenceWebsite.html
    │   storage.rules
    │   style.css
    │
    ├───assets
    │       background.png
    │       createProviderAccount.css
    │       doctorbackground.png
    │       doctorbackgroundwide.png
    │       haroldbackground.png
    │       haroldbackgroundwide.png
    │       med-bg.jpg
    │       medicationadherencebackground.png
    │       MedicationAdherenceWebsiteLogin.css
    │       PatientDashboard.css
    │       PatientLogin.css
    │       ProviderLogin.css
    │       ProviderMedicationAdherenceWebsite.css
    │
    └───public
            404.html
            index.html
```

## Contributing

    Fork this repository

    Create a topic branch (git checkout -b feature/foo)

    Commit your changes (git commit -m 'Add feature')

    Push to branch (git push origin feature/foo)

    Open a Pull Request

Please adhere to existing code style and add tests if you extend any logic.
    
        If you have any questions, feel free to reach out.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
```