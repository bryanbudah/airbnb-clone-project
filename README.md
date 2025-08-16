# AirBnB Clone Project

## Project Overview
This is a clone of the AirBnB web application, developed as part of the ALX Software Engineering program. The project will implement core features of AirBnB including user authentication, property listings, bookings, and reviews.

## Tech Stack
- **Frontend**: HTML5, CSS3, JavaScript
- **Backend**: Python (Flask framework)
- **Database**: MySQL (with SQLAlchemy ORM)
- **Infrastructure**: Nginx web server, Ubuntu
- **Deployment**: AWS (optional)

## Project Goals
1. Implement a console application to manage AirBnB objects
2. Develop a RESTful API for the application
3. Build a dynamic web interface
4. Add user authentication and authorization
5. Implement database storage

## Getting Started
1. Clone this repository
2. Set up virtual environment: `python3 -m venv venv`
3. Install dependencies: `pip install -r requirements.txt`
4. Run the console: `./console.py`

## Team Roles

### Backend Developer
**Responsibilities:**
- Develop server-side logic using Python/Flask
- Implement RESTful API endpoints
- Integrate with database systems
- Ensure data security and protection
- Optimize application performance

### Frontend Developer
**Responsibilities:**
- Implement responsive UI components
- Develop interactive features with JavaScript
- Ensure cross-browser compatibility
- Collaborate with designers for UI/UX implementation
- Optimize frontend performance

### Database Administrator (DBA)
**Responsibilities:**
- Design and maintain database schema
- Optimize queries and database performance
- Implement data migration scripts
- Ensure data integrity and security
- Set up database backups and recovery

### Full Stack Developer
**Responsibilities:**
- Work on both frontend and backend components
- Ensure seamless integration between systems
- Implement end-to-end features
- Troubleshoot cross-system issues
- Maintain code consistency across layers

### DevOps Engineer
**Responsibilities:**
- Configure and maintain deployment infrastructure
- Set up CI/CD pipelines
- Monitor system performance and logs
- Implement scaling solutions
- Manage cloud resources (AWS/Azure/GCP)

### Quality Assurance Engineer
**Responsibilities:**
- Develop test plans and cases
- Execute manual and automated tests
- Report and track bugs
- Ensure compliance with requirements
- Perform regression testing

### Project Manager
**Responsibilities:**
- Define project scope and timelines
- Coordinate between team members
- Track progress and milestones
- Manage stakeholder communication
- Mitigate risks and resolve blockers
## Technology Stack

This project utilizes the following technologies:

- **Django**: A high-level Python web framework used for building the backend RESTful APIs and handling server-side logic.
  
- **Django REST Framework**: A powerful toolkit built on top of Django for creating Web APIs, used to implement the REST API endpoints.

- **PostgreSQL**: A relational database system used for persistent data storage, offering scalability and reliability for user and property data.

- **GraphQL**: A query language for APIs that allows clients to request exactly the data they need, implemented to provide flexible data retrieval options alongside REST endpoints.

- **React**: A JavaScript library for building user interfaces, used to create the interactive frontend components of the application.

- **Next.js**: A React framework that enables server-side rendering and static site generation, used to improve performance and SEO.

- **Docker**: A platform for containerization, used to package the application and its dependencies into containers for consistent deployment across environments.

- **AWS (Amazon Web Services)**: Cloud services used for hosting the application, storing media files, and other infrastructure needs.

- **Redis**: An in-memory data store used for caching and improving application performance.

- **Celery**: A distributed task queue system used for handling asynchronous tasks like email notifications and background processes.
## Database Design

The database consists of the following core entities with their relationships:

### 1. Users
**Fields:**
- `id` (Primary Key)
- `username` (Unique)
- `email` (Unique)
- `password` (Hashed)
- `role` (Host/Guest)
- `profile_image`

**Relationships:**
- A User can list **multiple** Properties (as a Host)
- A User can make **multiple** Bookings (as a Guest)
- A User can write **multiple** Reviews

### 2. Properties
**Fields:**
- `id` (Primary Key)
- `title`
- `description`
- `price_per_night`
- `location` (City/Country)
- `amenities` (JSON/Array)
- `host_id` (Foreign Key → Users)

**Relationships:**
- Belongs to **one** User (Host)
- Can have **multiple** Bookings
- Can have **multiple** Reviews
- Can have **multiple** Images

### 3. Bookings
**Fields:**
- `id` (Primary Key)
- `check_in_date`
- `check_out_date`
- `total_price`
- `status` (Confirmed/Pending/Cancelled)
- `guest_id` (Foreign Key → Users)
- `property_id` (Foreign Key → Properties)

**Relationships:**
- Belongs to **one** User (Guest)
- Belongs to **one** Property
- Can have **one** associated Payment
- Can have **one** Review

### 4. Reviews
**Fields:**
- `id` (Primary Key)
- `rating` (1-5)
- `comment`
- `created_at`
- `guest_id` (Foreign Key → Users)
- `property_id` (Foreign Key → Properties)
- `booking_id` (Foreign Key → Bookings)

**Relationships:**
- Belongs to **one** User (Guest)
- Belongs to **one** Property
- Belongs to **one** Booking

### 5. Payments
**Fields:**
- `id` (Primary Key)
- `amount`
- `payment_method`
- `transaction_id`
- `status` (Success/Failed/Pending)
- `booking_id` (Foreign Key → Bookings)

**Relationships:**
- Belongs to **one** Booking

### 6. PropertyImages
**Fields:**
- `id` (Primary Key)
- `image_url`
- `is_primary` (Boolean)
- `property_id` (Foreign Key → Properties)

**Relationships:**
- Belongs to **one** Property
Users
│
├─── Hosts Properties (1-to-Many)
│    └─── Property has Bookings (1-to-Many)
│         └─── Booking has Payment (1-to-One)
│
└─── Makes Bookings (1-to-Many)
     └─── Booking has Review (1-to-One)