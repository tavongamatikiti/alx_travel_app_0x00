# ALX Travel App - Database Modeling and Data Seeding

A comprehensive Django-based travel booking platform with REST API support, featuring Listing, Booking, and Review models with database seeding capabilities.

## Project Overview

This project is part of the ALX Backend Python curriculum, focusing on database modeling and data seeding in Django. It implements a complete travel booking system with properties (listings), customer bookings, and user reviews, along with serializers for API data representation and a management command to seed the database with sample data.

## Key Features

- **Listing Model**: Properties available for booking with host information, pricing, and availability dates
- **Booking Model**: Customer bookings with status tracking and guest management
- **Review Model**: User reviews with ratings and unique constraints
- **REST API**: Full REST API support using Django REST Framework
- **Data Seeding**: Management command to populate database with realistic sample data
- **Swagger/OpenAPI Documentation**: Automatic API documentation available at `/swagger/`
- **PostgreSQL Database**: Robust database configuration with environment variable management

## Models Structure

### Listing Model
- `listing_id`: UUID primary key
- `host`: ForeignKey to User
- `title`: Property title
- `description`: Detailed description
- `location`: Property location
- `price_per_night`: Decimal price
- `max_guests`: Maximum number of guests
- `available_from`: Availability start date
- `available_to`: Availability end date
- Timestamps: `created_at`, `updated_at`

### Booking Model
- `booking_id`: UUID primary key
- `listing`: ForeignKey to Listing
- `user`: ForeignKey to User
- `check_in_date`: Check-in date
- `check_out_date`: Check-out date
- `number_of_guests`: Guest count
- `total_price`: Total booking price
- `status`: Booking status (pending, confirmed, cancelled, completed)
- Timestamps: `created_at`, `updated_at`

### Review Model
- `review_id`: UUID primary key
- `listing`: ForeignKey to Listing
- `user`: ForeignKey to User
- `rating`: Rating from 1 to 5
- `comment`: Review comment
- Timestamps: `created_at`, `updated_at`
- Unique constraint: One review per user per listing

## Technology Stack

- **Backend Framework**: Django 5.2.7
- **API Framework**: Django REST Framework 3.16.1
- **Database**: PostgreSQL / SQLite
- **API Documentation**: drf-yasg (Swagger/OpenAPI)
- **Task Queue**: Celery with Redis
- **CORS**: django-cors-headers

## Project Structure

```
alx_travel_app_0x00/
├── listings/                      # Main listings app
│   ├── models.py                  # Listing, Booking, Review models
│   ├── serializers.py             # DRF serializers with validation
│   ├── views.py                   # API views
│   ├── urls.py                    # URL routing
│   ├── management/
│   │   └── commands/
│   │       └── seed.py            # Database seeding command
│   └── migrations/
│       └── 0001_initial.py        # Initial database migration
├── settings.py                    # Project settings
├── urls.py                        # Main URL configuration
├── manage.py                      # Django management script
├── requirements.txt               # Python dependencies
└── README.md                      # This file
```

## Installation

### Prerequisites

- Python 3.8 or higher
- PostgreSQL 12 or higher (or SQLite for development)
- pip (Python package manager)
- Virtual environment tool

### Setup Instructions

1. **Clone the repository**
   ```bash
   git clone https://github.com/tavongamatikiti/alx_travel_app_0x00.git
   cd alx_travel_app_0x00
   ```

2. **Create and activate virtual environment**
   ```bash
   python3 -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Set up environment variables**
   ```bash
   cp .env.example .env
   ```

   Edit `.env` file with your configuration:
   ```
   SECRET_KEY=your-secret-key-here
   DEBUG=True
   DB_NAME=alx_travel_app_db
   DB_USER=postgres
   DB_PASSWORD=your_password
   DB_HOST=localhost
   DB_PORT=5432
   ```

5. **Run migrations**
   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

6. **Seed the database with sample data**
   ```bash
   python manage.py seed
   ```

   This command will create:
   - 5 sample users
   - 20 property listings across various global locations
   - 30 bookings with different statuses
   - 6 reviews with ratings

7. **Create superuser (optional)**
   ```bash
   python manage.py createsuperuser
   ```

8. **Run development server**
   ```bash
   python manage.py runserver
   ```

The application will be available at `http://localhost:8000`

## API Endpoints

### Listings
- `GET /api/listings/` - List all listings
- `POST /api/listings/` - Create a new listing
- `GET /api/listings/{id}/` - Get listing details
- `PUT /api/listings/{id}/` - Update a listing
- `DELETE /api/listings/{id}/` - Delete a listing

### Bookings
- `GET /api/bookings/` - List all bookings
- `POST /api/bookings/` - Create a new booking
- `GET /api/bookings/{id}/` - Get booking details
- `PUT /api/bookings/{id}/` - Update a booking
- `DELETE /api/bookings/{id}/` - Delete a booking

### Reviews
- `GET /api/reviews/` - List all reviews
- `POST /api/reviews/` - Create a new review
- `GET /api/reviews/{id}/` - Get review details
- `PUT /api/reviews/{id}/` - Update a review
- `DELETE /api/reviews/{id}/` - Delete a review

## API Documentation

Once the server is running, you can access the API documentation at:

- **Swagger UI**: http://localhost:8000/swagger/
- **ReDoc**: http://localhost:8000/redoc/
- **JSON Schema**: http://localhost:8000/swagger.json

## Database Seeding

The `seed` management command populates the database with realistic sample data for development and testing:

```bash
python manage.py seed
```

**What it does:**
- Clears existing data (Reviews, Bookings, Listings, non-superuser Users)
- Creates 5 sample users with authentication
- Generates 20 realistic property listings with:
  - Various property types (Studio, Penthouse, Villa, Cabin, etc.)
  - Global locations (New York, Paris, Tokyo, London, etc.)
  - Random pricing ($50-$500 per night)
  - Different guest capacities
- Creates 30 bookings with various statuses
- Generates 6 reviews with ratings

## Serializers and Validation

### ListingSerializer
- Nested host information (read-only)
- Date validation (available_to must be after available_from)
- Price and guest validation

### BookingSerializer
- Nested listing and user information
- Check-out date must be after check-in date
- Guest count cannot exceed listing capacity
- Total price validation

### ReviewSerializer
- Nested user information
- Rating validation (1-5)
- Unique review per user-listing combination

## Development

### Running Tests

```bash
python manage.py test
```

### Database Migrations

```bash
# Create migrations
python manage.py makemigrations

# Apply migrations
python manage.py migrate

# Show migrations
python manage.py showmigrations
```

### Clearing and Reseeding Database

```bash
# The seed command automatically clears existing data
python manage.py seed
```

## Learning Objectives

This project demonstrates:

1. **Django Models**: Defining models with proper fields, relationships, and constraints
2. **ForeignKey Relationships**: One-to-many relationships between User, Listing, Booking, and Review
3. **Data Validation**: Using Django validators and custom validation methods
4. **REST API Serializers**: Converting Django models to JSON for API responses
5. **Management Commands**: Creating custom Django commands for database operations
6. **Database Seeding**: Populating databases with realistic test data
7. **UUID Primary Keys**: Using UUIDs instead of integer IDs for better security
8. **Indexes and Constraints**: Optimizing database queries and ensuring data integrity

## Best Practices Implemented

- UUID primary keys for all models
- Proper model relationships with `related_name`
- Database indexes for frequently queried fields
- Validators for data integrity (MinValueValidator, MaxValueValidator)
- Unique constraints to prevent duplicate reviews
- Nested serializers for API responses
- Custom validation in serializers
- Proper use of Django's auto_now and auto_now_add for timestamps
- Management commands for database operations

## Troubleshooting

### Database Connection Issues

If you encounter database connection errors:
1. Ensure PostgreSQL is running
2. Verify database credentials in `.env`
3. Check if the database exists
4. Ensure PostgreSQL is listening on the correct port

### Seed Command Issues

If the seed command fails:
1. Ensure migrations are up to date: `python manage.py migrate`
2. Check that the database is accessible
3. Verify User model is properly configured

### Import Errors

If you see import errors:
1. Ensure virtual environment is activated
2. Reinstall dependencies: `pip install -r requirements.txt`
3. Check Python version compatibility

## Project Files

### Required Files (as per ALX requirements)

- ✅ `listings/models.py` - Contains Listing, Booking, and Review models
- ✅ `listings/serializers.py` - Contains serializers for Listing and Booking models
- ✅ `listings/management/commands/seed.py` - Management command to seed database
- ✅ `README.md` - This documentation file

## License

This project is part of the ALX Software Engineering program.

## Repository

- **GitHub Repository**: alx_travel_app_0x00
- **Directory**: alx_travel_app

## Author

Tavonga Matikiti - ALX Software Engineering Student

## Acknowledgments

- ALX Africa for the project structure and requirements
- Django and Django REST Framework communities
- Contributors and maintainers

---

**Happy Coding!** ✨