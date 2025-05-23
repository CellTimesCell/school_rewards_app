# School Rewards App

A comprehensive web application for managing a school-based points reward system. Teachers can award points to students for good behavior, academic achievements, and participation. Students can track their points and compete on a leaderboard.

## Overview

This application provides a complete solution for schools to implement a digital rewards system. It replaces traditional paper-based tracking with a modern web and mobile-friendly platform that makes awarding and tracking points quick and effortless.

## Features

### User Roles

- **Students**: View earned points, transaction history, personal QR code, and the school leaderboard
- **Teachers**: Award points to students by scanning QR codes, view transaction history
- **Administrators**: Manage users, view all transactions, system configuration

### Key Functionality

- **QR Code Integration**: Students receive unique QR codes for easy identification
- **Points Tracking**: Real-time updating and caching of point totals
- **Leaderboard**: Motivates students through healthy competition
- **Mobile API**: RESTful API with JWT authentication for mobile applications
- **Responsive Design**: Works on desktop and mobile browsers

## Technology Stack

- **Backend**: Python + Flask
- **Database**: PostgreSQL (with SQLAlchemy ORM)
- **Caching**: Redis
- **Authentication**: Flask-Login + JWT (for API)
- **Frontend**: HTML, CSS, JavaScript
- **Task Queue**: Celery + Redis (for background processing)
- **Monitoring**: Prometheus (optional)
- **Deployment**: Docker, Docker Compose

## Project Structure

```
school_rewards_app/
├── app/                    # Main application package
│   ├── __init__.py         # Application factory pattern
│   ├── models.py           # Database models
│   ├── routes.py           # Web routes
│   ├── api_routes.py       # API endpoints
│   ├── forms.py            # Form definitions
│   ├── cache.py            # Caching functions
│   ├── celery.py           # Async task configuration
│   ├── static/             # Static assets (CSS, JS, images)
│   ├── templates/          # Jinja2 templates
│   └── utils.py            # Utility functions
├── migrations/             # Database migrations
├── config.py               # Application configuration
├── run.py                  # Application entry point
├── requirements.txt        # Python dependencies
├── Dockerfile              # Container definition
└── docker-compose.yml      # Multi-container setup
```

## Setup Instructions

### Local Development

1. **Clone the repository**:
   ```bash
   git clone [repository-url]
   cd school_rewards_app
   ```

2. **Create a virtual environment**:
   ```bash
   python -m venv venv
   # On Windows:
   venv\Scripts\activate
   # On macOS/Linux:
   source venv/bin/activate
   ```

3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Set up environment variables**:
   Create a `.env` file in the project root with the following variables:
   ```
   FLASK_APP=run.py
   FLASK_ENV=development
   SECRET_KEY=your-secret-key
   DATABASE_URL=postgresql://username:password@localhost/school_rewards
   ```

5. **Initialize the database**:
   ```bash
   flask db upgrade
   ```

6. **Run the application**:
   ```bash
   flask run
   # Or
   python run.py
   ```

### Docker Deployment

1. **Build and run with Docker Compose**:
   ```bash
   docker-compose up -d
   ```

2. **Access the application**:
   Open `http://localhost` in your browser

## Using the Application

### Initial Login

The application comes with pre-configured test accounts:

- **Admin**: Username: `admin`, Password: `admin123`
- **Teacher**: Username: `teacher1`, Password: `teacher123`
- **Student**: Username: `student1`, Password: `student123`

### Common Tasks

- **Awarding Points** (Teacher):
  1. Login as a teacher
  2. Navigate to "Scan QR Code"
  3. Scan a student's QR code
  4. Enter the points and description
  5. Submit the form

- **Viewing Points** (Student):
  1. Login as a student
  2. The dashboard shows total points and recent transactions
  3. Visit "Leaderboard" to see rankings

- **Adding Users** (Admin):
  1. Login as an administrator
  2. Navigate to the admin dashboard
  3. Select "Add Student" or "Add Teacher"
  4. Fill in the required information

## API Documentation

The application provides a RESTful API for mobile integration:

- **Authentication**: `POST /api/v1/auth/login`
- **Scan QR Code**: `POST /api/v1/scan-qr`
- **Award Points**: `POST /api/v1/add-points`
- **View Transactions**: `GET /api/v1/transactions`

All API requests (except login) require a JWT token in the Authorization header:
```
Authorization: Bearer <token>
```

## Monitoring

The application includes Prometheus integration for monitoring:

- Metrics available at `/metrics` endpoint when `PROMETHEUS_METRICS=True`
- Basic metrics include request counts, response times, and error rates

## Contributing

Contributions to the School Rewards App are welcome! Here's how you can contribute:

1. **Fork the repository**: Create your own copy of the project
2. **Create a feature branch**: `git checkout -b feature/your-feature-name`
3. **Commit your changes**: `git commit -am 'Add some feature'`
4. **Push to the branch**: `git push origin feature/your-feature-name`
5. **Submit a pull request**: Open a PR from your fork to the main repository

Please make sure your code follows the existing style and includes appropriate tests.

When contributing, please also:
- Add comments to your code where necessary
- Update documentation if you change functionality
- Follow the code of conduct

## License

MIT License

Copyright (c) 2025 School Rewards App

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
