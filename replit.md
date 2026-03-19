# Pizza Restaurants - Phase 4 Code Challenge

## Overview
A Flask + React application for managing Pizza Restaurants. This is a code challenge focused on implementing a RESTful API with SQLAlchemy models and relationships.

## Architecture

### Backend (Flask)
- **Location:** `server/`
- **Port:** 8000 (dev), 5000 (production via gunicorn)
- **Framework:** Flask + Flask-RESTful + Flask-SQLAlchemy + Flask-Migrate
- **Database:** SQLite (`server/app.db`)

### Frontend (React)
- **Location:** `client/`
- **Port:** 5000
- **Framework:** React (Create React App)
- **Proxy:** Forwards API calls to `http://127.0.0.1:8000`

## Models
- `Restaurant` - has many Pizzas through RestaurantPizza
- `Pizza` - has many Restaurants through RestaurantPizza
- `RestaurantPizza` - join table with `price` (1-30 validation), cascades deletes

## API Routes
- `GET /restaurants` - list all restaurants
- `GET /restaurants/<id>` - get restaurant with its pizzas
- `DELETE /restaurants/<id>` - delete restaurant (cascades to RestaurantPizzas)
- `GET /pizzas` - list all pizzas
- `POST /restaurant_pizzas` - create a new RestaurantPizza

## Workflows
- **Start application** - React frontend on port 5000 (webview)
- **Backend API** - Flask API on port 8000 (console)

## Setup Commands
```bash
# Install Python deps
pip install flask flask-migrate flask-sqlalchemy sqlalchemy-serializer flask-restful gunicorn

# Install Node deps
npm install --prefix client

# Setup DB
FLASK_APP=server/app.py flask db init
FLASK_APP=server/app.py flask db migrate -m "initial"
FLASK_APP=server/app.py flask db upgrade head
python server/seed.py
```

## Deployment
Configured for autoscale with gunicorn serving the Flask app on port 5000.
