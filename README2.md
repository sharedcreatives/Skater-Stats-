# SkaterStatsPro
SkaterStatsPro is a microservices-based platform built using Laravel, designed for scalability and maintainability.

Break down the application into distinct services based on business capabilities:

	1.	User Service: Handles user registration, authentication, and profile management.
	2.	Player Service: Manages player profiles, statistics, and related data.
    3.  Coach Service: Manages coach profiles, statistics, and related data.
	4.	Team Service: Handles team information, rosters, and management.
	5.	Game Service: Manages game schedules, results, and statistics.
	6.	Notification Service: Sends notifications to users about game updates, player stats, etc.
	7.	Gateway Service: Serves as the API gateway to route requests to the appropriate microservices.

# Architecture

SkaterStatsPro follows a microservices pattern, where each service runs independently. Communication between services is handled via RESTful APIs.

[Diagram Placeholder]

# Getting Started

## Prerequisites

Ensure you have the following installed:

* Docker
* Docker Compose

## Installation


Clone the repository: `git clone cd hockey-stats`

Build and start the services: `docker-compose up --build`

Each service will be available on the following ports:

* User Service: http://localhost:8001
* Coach Service: http://localhost:8002
* Player Service: http://localhost:8003
* Game Service: http://localhost:8004
* Team Service: http://localhost:8005
* Notification Service: http://localhost:8006
* Gateway Service: http://localhost:8000


## Running the Services

After building the images, you can start the services using: `docker-compose up`

To stop the services: `docker-compose down`

## API Endpoints

Each service exposes a set of RESTful endpoints. Below are examples for each service.

#### Set Up Each Microservice

a. User Service 
Functionality: User registration, login, profile updates.
Endpoints:
* POST /api/users/register
* POST /api/users/login
* GET /api/users/profile

b. Player Service
Functionality: Player profile management, statistics.
Endpoints:
* POST /api/players
* GET /api/players/{id}
* PUT /api/players/{id}
* DELETE /api/players/{id}
* GET /api/players/{id}/stats
* POST /api/players/{id}/stats
* PUT /api/players/{id}/stats/{stat_id}
* DELETE /api/players/{id}/stats/{stat_id}

c. Team Service
Functionality: Team information, roster management.
Endpoints:
* POST /api/teams
* GET /api/teams/{id}
* PUT /api/teams/{id}
* DELETE /api/teams/{id}
* 
d. Game Service
Functionality: Game schedules, results, statistics.
Endpoints:

## Environment Variables

Each service requires specific environment variables. Below is an example configuration for the User Service.

env
