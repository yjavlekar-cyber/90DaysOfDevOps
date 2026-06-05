# Day 34 – Docker Compose: Real-World Multi-Container Apps
A Three tier tourism website including frontend, backend and database.
what do we have as code:
1.Backend (Flask)
  Processes application logic, handles page routing, and manages data flow for the contact form.
  Connects the user interface to the database and cache, ensuring content is delivered dynamically.

2.Frontend (Nginx & CSS)
  Acts as a high-speed reverse proxy that secures the backend and serves static files like images.
  Uses a custom "Coastal Blue & Sand" CSS theme to provide a modern, responsive user experience.

3.Database (MySQL)
  Provides persistent storage for tourist attraction details and saves all visitor-submitted messages.
  Automatically builds its own tables and seeds them with data the moment the container starts.

4.Cache (Redis)
  Stores frequently requested information in-memory to eliminate the need for repeated database queries.
  Ensures the "Places" page loads instantly for visitors by serving cached data in milliseconds.
