# SkaterStats

SkaterStats is a microservices-based platform built using Laravel, designed for scalability and maintainability.

Break down the application into distinct services based on business capabilities:

- User Service: User registration, login, profile updates.
- Player Service: Player profile management, statistics.
- Team Service: Team information, roster management.
- Game Service: Game schedules, results, statistics.
- Notification Service: Email notifications, reminders.
- Gateway Service: API gateway, authentication, routing.
- Coach Service: Coach profile management, statistics.
- Stat Service: Player and team statistics.
- Schedule Service: Game schedules, reminders.

# Architecture

SkaterStats follows a microservices pattern, where each service runs independently. Communication between services is handled via RESTful APIs.

[Diagram Placeholder]

# Getting Started

## Prerequisites

Ensure you have the following installed:

- Docker
- Docker Compose

## Installation

Clone the repository: `git clone`

Build and start the services: `docker-compose up --build`

Each service will be available on the following ports:

- User Service: http://user-service.test
- Coach Service: http://coach-service.test
- Player Service: http://player-service.test
- Game Service: http://game-service.test
- Team Service: http://team-service.test
- Notification Service: http://notification-service.test
- Gateway Service: http://gateway.test

## Running the Services

After building the images, you can start the services using: `docker-compose up`

To stop the services: `docker-compose down`

## API Endpoints

Each service exposes a set of RESTful endpoints. Below are examples for each service.

#### Set Up Each Microservice

a. User Service
Functionality: User registration, login, profile updates.
Endpoints:

- POST /api/users/register
- POST /api/users/login
- GET /api/users/profile

b. Player Service
Functionality: Player profile management, statistics.
Endpoints:

- POST /api/players
- GET /api/players/{id}
- PUT /api/players/{id}
- DELETE /api/players/{id}
- GET /api/players/{id}/stats
- POST /api/players/{id}/stats
- PUT /api/players/{id}/stats/{stat_id}
- DELETE /api/players/{id}/stats/{stat_id}

c. Team Service
Functionality: Team information, roster management.
Endpoints:

- POST /api/teams
- GET /api/teams/{id}
- PUT /api/teams/{id}
- DELETE /api/teams/{id}
- d. Game Service
  Functionality: Game schedules, results, statistics.
  Endpoints:

## Environment Variables

Each service requires specific environment variables. Below is an example configuration for the User Service.

env
