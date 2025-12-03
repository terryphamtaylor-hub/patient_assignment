Patient Assignment App

Overview

The Patient Assignment App is a standalone, browser-based tool designed to automate the distribution of patients to medical teams. It replaces manual assignment processes with an algorithmic approach that balances workload, respects team location preferences, and handles specialty patients (e.g., Sarcoma, Gyn).

The application is built as a single HTML file containing React code and Tailwind CSS, making it extremely portable and easy to run without any installation or build steps.

Features

Team Management:

Configure starting patient counts.

Toggle "Low Cap" status (10 patients) vs Standard Cap (16 patients).

Define preferred locations and locations to avoid.

Patient Management:

Add unassigned patients manually or via bulk entry.

Specify patient attributes: Name, Location, Specialty Type (Sarcoma/Gyn), and Admission status (H&P needs).

Intelligent Assignment Algorithm:

Prioritizes continuity of care and geographic clustering.

Balances workload across teams.

Respects specialty preferences (Sarcoma/Gyn teams).

Performs "swaps" to optimize H&P (History & Physical) distribution.

Fast Data Entry: Text-based bulk import for rapid setup at the start of a shift.

Overflow Handling: Interactive modal to assign support teams (Backups, Moonlighters) when standard teams reach capacity.

Reporting: Generates a detailed assignment report and a summary of team loads.

How to Run

Save the provided code as an .html file (e.g., patient_assignment.html).

Open the file in any modern web browser (Chrome, Edge, Firefox, Safari).

No internet connection is required to run the logic, though an internet connection is needed initially to load the libraries (React, Tailwind) from the CDNs.

Usage Guide

1. Setting Up Teams

The app loads with default teams (A-P). You can modify their state directly on the dashboard cards:

Starting Patients: Enter the number of patients the team already carries.

Low Cap: Check this box to limit the team to 10 patients (default is 16).

Other Locations: Add comma-separated locations the team is already covering to encourage clustering.

2. Adding Patients

You can add patients in two ways:

Manual Entry: Use the form at the top to add patients one by one.

Fast Data Entry: Click the "Fast Data Entry" button to paste formatted text.

Patient Format: (AdmittingTeam; PatientName; Location; Gyn Y/N; Sarcoma Y/N; H&P Y/N)

Example: (M; John Doe; G22; N; N; Y)

3. Running the Assignment

Click "Assign Unassigned Patients". The algorithm will:

Assign specialty patients to specialty teams.

Assign patients to teams with matching geographic preferences.

Distribute remaining patients to balance the load.

Run optimization passes to swap patients for better geographic clustering or H&P balance.

4. Handling Overflows

If all teams reach their "Cap" (10 or 16), an Over Cap Modal will appear.

Select support teams (e.g., Team M, Moonlighters) to take the excess load.

Define their role (Rounding, Admitting, or Hybrid).

You can also choose to "Overcap rounding teams by 1" to squeeze one extra patient onto existing teams before using backups.

Algorithm Logic

The assignment logic proceeds in specific phases:

Specialty Phase: Assigns Sarcoma/Gyn patients to teams that prefer them.

Location Phase: Assigns patients to teams that have a "Priority 1" preference for the patient's location.

General Phase: Assigns remaining patients, attempting to avoid "Avoid Locations" defined by the teams.

Balancing & Swapping:

Load Balancing: Ensures no team is significantly more burdened than others.

H&P Upgrades/Downgrades: Swaps patients between teams to ensure H&Ps are distributed evenly or assigned to teams with capacity.

Geographic Swaps: Swaps patients between teams if it results in better geographic clustering for both.

Tech Stack

HTML5

React (via CDN, using Babel Standalone for in-browser JSX compilation)

Tailwind CSS (via CDN for styling)

Customization

To modify team defaults (names, default preferences), look for the defaultTeamDataArray constant in the <script> section of the HTML file.
