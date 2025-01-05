# Microservices Architecture for Social Media Application

VidStream is a simplified video-sharing platform built with a modular and scalable microservices architecture. Inspired by popular social media apps, it handles video uploads, processing, and streaming, designed for efficient service deployment and enhanced scalability.

## Overview

The platform is designed to:
- Enable video sharing and engagement with users.
- Identify trending hashtags based on interactions.
- Manage user subscriptions and recommend content dynamically.

The microservices are independently scalable and deployable, ensuring flexibility and ease of maintenance.

## Architecture

VidStream utilizes a microservices architecture with the following key components:

### Microservices

#### Video Microservice (VM)
- **Purpose**: Manages video operations like posting, listing, and engagement.
- **Tech Stack**:
  - Framework: Micronaut
  - Database: Cassandra
  - Messaging Queue: Kafka
- **Responsibilities**: Handles video data, tracks user engagement, and publishes interaction events.

#### Trending Hashtag Microservice (THM)
- **Purpose**: Identifies top-liked hashtags over a specified time window.
- **Tech Stack**:
  - Framework: Micronaut
  - Database: PostgreSQL
  - Data Streaming: Kafka Streams
- **Responsibilities**: Aggregates likes per tag and dynamically updates trending hashtags.

#### Subscription Microservice (SM)
- **Purpose**: Manages user subscriptions to hashtags and recommends content.
- **Tech Stack**:
  - Framework: Micronaut
  - Database: Neo4j
  - Messaging Queue: Kafka
- **Responsibilities**: Handles subscriptions and recommends videos based on interactions.

### Event-Driven Communication
- **Messaging Queue**: Kafka facilitates communication between microservices using event-driven architecture.

### Database Technologies
- **Cassandra**: Stores video data and user interactions.
- **PostgreSQL**: Supports trending hashtag aggregation.
- **Neo4j**: Manages relationships for user subscriptions.

## Build and Deployment

### Prerequisites
- Java 17
- Docker & Docker Compose
- Gradle

### Building the Microservices
Navigate to each microservice directory and run:
```bash
./gradlew build
./gradlew jibDockerBuild
```
This creates a Docker image for each service using Google Jib.

### Running the Application
Use Docker Compose for orchestration:
```bash
docker-compose up
```
This starts all microservices, databases, and Kafka instances.

## CLI Client
Interact with the microservices using a Command-line Interface (CLI):

- **Post a Video**:
  ```bash
  cli post -t=<title> -u=<userId> -T=<tags>
  ```
- **Like a Video**:
  ```bash
  cli like-video -u=<userId> -v=<videoId>
  ```
- **Show Trending Hashtags**:
  ```bash
  cli current-top -l=<limit>
  ```

Run `cli --help` for the full list of commands.

## Quality Assurance

- **Unit and Integration Testing**: High test coverage with JaCoCo.
- **System Testing**: Ensures proper inter-service communication and data integrity.
- **Vulnerability Scanning**: Docker images are scanned using Trivy and Docker Scout.
