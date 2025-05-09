# Airbnb Clone Project
A clone of Airbnb made for the ALX backend Prodev project.
## 🚀 Objective
The backend for the Airbnb Clone project is designed to provide a robust and scalable foundation for managing user interactions, property listings, bookings, and payments. This backend will support various functionalities required to mimic the core features of Airbnb, ensuring a smooth experience for users and hosts.

## 🏆 Project Goals
User Management: Implement a secure system for user registration, authentication, and profile management.  
Property Management: Develop features for property listing creation, updates, and retrieval.  
Booking System: Create a booking mechanism for users to reserve properties and manage booking details.  
Payment Processing: Integrate a payment system to handle transactions and record payment details.  
Review System: Allow users to leave reviews and ratings for properties.  
Data Optimization: Ensure efficient data retrieval and storage through database optimizations.  
## 🛠️ Features Overview
### 1. API Documentation
OpenAPI Standard: The backend APIs are documented using the OpenAPI standard to ensure clarity and ease of integration.  
Django REST Framework: Provides a comprehensive RESTful API for handling CRUD operations on user and property data.  
GraphQL: Offers a flexible and efficient query mechanism for interacting with the backend.  
### 2. User Authentication
Endpoints: /users/, /users/{user_id}/  
Features: Register new users, authenticate, and manage user profiles.
### 3. Property Management
Endpoints: /properties/, /properties/{property_id}/  
Features: Create, update, retrieve, and delete property listings.
### 4. Booking System
Endpoints: /bookings/, /bookings/{booking_id}/  
Features: Make, update, and manage bookings, including check-in and check-out details.
### 5. Payment Processing
Endpoints: /payments/  
Features: Handle payment transactions related to bookings.
### 6. Review System
Endpoints: /reviews/, /reviews/{review_id}/  
Features: Post and manage reviews for properties.
### 7. Database Optimizations
Indexing: Implement indexes for fast retrieval of frequently accessed data.  
Caching: Use caching strategies to reduce database load and improve performance.
## ⚙️ Technology Stack
* Django: A high-level Python web framework used for building the RESTful API.
* Django REST Framework: Provides tools for creating and managing RESTful APIs.
* PostgreSQL: A powerful relational database used for data storage.
* GraphQL: Allows for flexible and efficient querying of data.
* Celery: For handling asynchronous tasks such as sending notifications or processing payments.
* Redis: Used for caching and session management.
* Docker: Containerization tool for consistent development and deployment environments.
* CI/CD Pipelines: Automated pipelines for testing and deploying code changes.
## 👥 Team Roles
Backend Developer: Responsible for implementing API endpoints, database schemas, and business logic.  
Database Administrator: Manages database design, indexing, and optimizations.  
DevOps Engineer: Handles deployment, monitoring, and scaling of the backend services.  
QA Engineer: Ensures the backend functionalities are thoroughly tested and meet quality standards.
## 📈 API Documentation Overview
REST API: Detailed documentation available through the OpenAPI standard, including endpoints for users, properties, bookings, and payments.  
GraphQL API: Provides a flexible query language for retrieving and manipulating data.
## 📌 Endpoints Overview
## REST API Endpoints
### Users

GET /users/ - List all users  
POST /users/ - Create a new user  
GET /users/{user_id}/ - Retrieve a specific user  
PUT /users/{user_id}/ - Update a specific user  
DELETE /users/{user_id}/ - Delete a specific user  
### Properties

GET /properties/ - List all properties  
POST /properties/ - Create a new property  
GET /properties/{property_id}/ - Retrieve a specific property  
PUT /properties/{property_id}/ - Update a specific property  
DELETE /properties/{property_id}/ - Delete a specific property  
### Bookings

GET /bookings/ - List all bookings  
POST /bookings/ - Create a new booking  
GET /bookings/{booking_id}/ - Retrieve a specific booking  
PUT /bookings/{booking_id}/ - Update a specific booking  
DELETE /bookings/{booking_id}/ - Delete a specific booking  
### Payments

POST /payments/ - Process a payment  
### Reviews

GET /reviews/ - List all reviews  
POST /reviews/ - Create a new review  
GET /reviews/{review_id}/ - Retrieve a specific review  
PUT /reviews/{review_id}/ - Update a specific review  
DELETE /reviews/{review_id}/ - Delete a specific review  

## 💾 Database Design

This section outlines the core entities and their relationships within the database schema.

### Key Entities

1.  **Users**
    * `user_id`: Primary Key, unique identifier for the user.  
    * `email`: Unique identifier for login, required.  
    * `password_hash`: Hashed password for security.  
    * `first_name`: User's first name.  
    * `created_at`: Timestamp of user creation.  

2.  **Properties**
    * `property_id`: Primary Key, unique identifier for the property.  
    * `host_id`: Foreign Key referencing `Users(user_id)`, indicating the owner/host.  
    * `title`: Name or title of the property listing.  
    * `address`: Physical address of the property.  
    * `price_per_night`: Cost to book the property for one night.   
    * `created_at`: Timestamp of property listing creation.   

3.  **Bookings**
    * `booking_id`: Primary Key, unique identifier for the booking.  
    * `guest_id`: Foreign Key referencing `Users(user_id)`, indicating the user who made the booking.  
    * `property_id`: Foreign Key referencing `Properties(property_id)`, indicating the property being booked.  
    * `check_in_date`: Start date of the booking.  
    * `check_out_date`: End date of the booking.  
    * `total_price`: Calculated total cost for the stay.  
    * `booking_status`: Current status (e.g., 'confirmed', 'pending', 'cancelled').  

4.  **Reviews**
    * `review_id`: Primary Key, unique identifier for the review.  
    * `user_id`: Foreign Key referencing `Users(user_id)`, indicating the user who wrote the review.  
    * `property_id`: Foreign Key referencing `Properties(property_id)`, indicating the property being reviewed.  
    * `rating`: Numerical rating (e.g., 1-5 stars).  
    * `comment`: Textual feedback from the user.  
    * `created_at`: Timestamp of when the review was submitted.  

5.  **Payments**
    * `payment_id`: Primary Key, unique identifier for the payment.  
    * `booking_id`: Foreign Key referencing `Bookings(booking_id)`, linking the payment to a specific booking.  
    * `amount`: The monetary value of the payment.  
    * `payment_status`: Current status (e.g., 'succeeded', 'failed', 'pending').  
    * `payment_date`: Timestamp of when the payment was processed.  
    * `transaction_id`: Unique identifier provided by the payment processor.  

### Relationships

* A **User** can own (host) multiple **Properties** (One-to-Many: User -> Properties).  
* A **User** can make multiple **Bookings** (One-to-Many: User -> Bookings).  
* A **User** can write multiple **Reviews** (One-to-Many: User -> Reviews).   
* A **Property** belongs to one **User** (host) (Many-to-One: Property -> User).  
* A **Property** can have multiple **Bookings** (One-to-Many: Property -> Bookings).  
* A **Property** can have multiple **Reviews** (One-to-Many: Property -> Reviews).  
* A **Booking** is made by one **User** (guest) (Many-to-One: Booking -> User).  
* A **Booking** is for one **Property** (Many-to-One: Booking -> Property).  
* A **Booking** typically has one associated **Payment** (One-to-One: Booking <-> Payment, usually).  
* A **Review** is written by one **User** (Many-to-One: Review -> User).  
* A **Review** pertains to one **Property** (Many-to-One: Review -> Property).  
* A **Payment** corresponds to one **Booking** (Many-to-One: Payment -> Booking).  

## ✨ Feature Breakdown

This section details the core functional components of the Airbnb Clone backend.

* **User Management**
    This feature provides the necessary infrastructure for handling user accounts. It includes secure registration, login authentication (verifying user identity), and allows users to manage their profile details, establishing the foundation for interactions within the platform.

* **Property Management**
    This component enables hosts to create, display, update, and remove property listings. It involves storing and retrieving property details like location, description, pricing, and availability, thereby populating the platform with rentable spaces.

* **Booking System**
    This feature facilitates the core reservation process for properties. Users can check availability, make bookings for specific dates, and manage their reservation details, coordinating the temporary rental agreement between guests and hosts.

* **Payment Processing**
    This integrates secure payment handling for booking transactions. It manages the collection of funds from guests upon booking confirmation and ensures the recording of payment statuses, enabling the financial aspect of the rental process.

* **Review System**
    This allows authenticated users (typically guests after a stay) to submit ratings and written feedback about properties. This contributes to building trust within the community by providing insights into property quality and host service based on past user experiences.

* **Data Optimization**
    This backend aspect focuses on ensuring the application runs efficiently, even with large amounts of data. Techniques like database indexing and caching are employed to speed up data retrieval and reduce server load, leading to a smoother user experience.

## 🔐 API Security

Ensuring the security of the API, user data, and transactions is a top priority for this project. The following measures are implemented to maintain a secure environment:

### Key Security Measures Implemented

* **Authentication:**
    * **Mechanism:** Secure token-based authentication (e.g., JWT - JSON Web Tokens) will be used to verify the identity of users making requests to protected endpoints.
    * **Purpose:** Ensures that only registered and logged-in users can access specific functionalities like booking properties or managing their profiles.

* **Authorization:**
    * **Mechanism:** Permissions checks are implemented at the endpoint level to ensure users can only perform actions they are allowed to (e.g., a user can only modify their own profile or delete properties they host).
    * **Purpose:** Prevents users from accessing or modifying data that doesn't belong to them, enforcing roles like guest vs. host.

* **HTTPS/TLS Encryption:**
    * **Mechanism:** All communication between the client applications and the backend API will be encrypted using HTTPS (TLS).
    * **Purpose:** Protects data in transit from eavesdropping or tampering, securing sensitive information like login credentials, personal details, and payment information.

* **Input Validation & Sanitization:**
    * **Mechanism:** All incoming data from requests (query parameters, request bodies) is rigorously validated against expected formats and sanitized to remove potentially malicious code.
    * **Purpose:** Mitigates risks such as SQL Injection, Cross-Site Scripting (XSS), and other injection attacks that could compromise the database or user sessions.

* **Rate Limiting:**
    * **Mechanism:** Limits are imposed on the number of requests an IP address or user can make to the API within a specific time window.
    * **Purpose:** Helps protect the service against brute-force login attempts and Denial-of-Service (DoS) attacks, ensuring platform availability.

* **Secure Password Storage:**
    * **Mechanism:** User passwords are not stored in plaintext. Instead, strong hashing algorithms (e.g., bcrypt, Argon2) with unique salts are used.
    * **Purpose:** Makes it computationally infeasible for attackers to recover original passwords even if they gain access to the database.

### Importance of Security in Key Areas

* **Protecting User Data:** Security measures like **Authentication**, **Authorization**, and **HTTPS** are crucial to safeguard users' personal information (profiles, booking history) from unauthorized access or breaches, maintaining user privacy and trust.
* **Securing Property Listings:** **Authorization** ensures that only property owners (hosts) can modify or delete their listings, preventing vandalism or unauthorized changes to crucial platform content. **Input Validation** prevents malicious content in descriptions or titles.
* **Ensuring Booking Integrity:** **Authentication** and **Authorization** prevent unauthorized users from making, viewing, or cancelling bookings. **HTTPS** protects sensitive travel details during transmission.
* **Securing Payments:** This is highly critical. **HTTPS** encrypts payment-related communication. Secure handling of API keys for the payment gateway (using environment variables) and **Input Validation** prevent tampering with transaction details, safeguarding against financial fraud.
* **Maintaining Platform Reliability:** **Rate Limiting** is essential to prevent malicious actors from overwhelming the server, ensuring the platform remains available and responsive for legitimate users.

## 🔄CI/CD Pipeline
A Continuous Integration/Continuous Deployment (CI/CD) pipeline is an automated process designed to streamline and improve the software development lifecycle. It involves integrating code changes frequently (Continuous Integration) and automatically preparing and deploying those changes to production (Continuous Deployment/Delivery).

### Why are CI/CD Pipelines Important for this Project?
Implementing a CI/CD pipeline for the Airbnb Clone backend offers several key benefits:

**Faster and More Frequent Releases:** Automating the build, test, and deployment process allows us to release new features, bug fixes, and updates more rapidly and reliably.
Improved Code Quality:** Continuous Integration involves running automated tests (unit, integration) on every code change. This helps catch bugs early in the development cycle, ensuring a higher quality codebase.
**Reduced Risk:** By deploying small, frequent changes, the risk associated with each deployment is significantly reduced compared to large, infrequent releases. Automated testing provides confidence in the stability of the application.
**Consistent Deployments:** Docker containers, as part of the pipeline, ensure that the application runs in consistent environments from development to production, eliminating "it works on my machine" issues.
**Earlier Feedback:** Developers receive rapid feedback on their code changes regarding integration issues and test failures, allowing for quicker identification and resolution of problems.
### Tools for Implementation
Several tools can be used to build a robust CI/CD pipeline for this project, leveraging the existing technology stack:

**GitHub Actions:** A powerful, integrated CI/CD service provided by GitHub, ideal for projects hosted on GitHub. It allows for defining workflows to automatically build, test, and deploy code upon pushes or pull requests.
**Docker:** Essential for creating consistent and isolated environments for building and running the application, ensuring that the deployment environment mirrors the development and testing environments.
**Django Management Commands/pytest:** Used within the CI pipeline to run automated tests (e.g., python manage.py test or pytest) to verify the correctness of the code.
**Database Migration Tools:** Integrating database schema migrations into the pipeline ensures that database changes are applied consistently across environments.

