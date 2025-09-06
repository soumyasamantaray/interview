# Java Microservices Demo with Spring Boot & Spring Cloud

This repository contains a collection of simple, runnable examples demonstrating core microservices patterns using Spring Boot and Spring Cloud. It's designed to help you understand and get started with building distributed systems in Java.

## Table of Contents

-   [Features](#features)
-   [Prerequisites](#prerequisites)
-   [Project Structure](#project-structure)
-   [How to Run](#how-to-run)
    -   [1. Service Discovery (Eureka Server & Client)](#1-service-discovery-eureka-server--client)
    -   [2. API Gateway (Spring Cloud Gateway)](#2-api-gateway-spring-cloud-gateway)
    -   [3. Centralized Configuration (Spring Cloud Config Server & Client)](#3-centralized-configuration-spring-cloud-config-server--client)
    -   [4. Resilience (Resilience4j Circuit Breaker)](#4-resilience-resilience4j-circuit-breaker)
-   [Key Technologies Used](#key-technologies-used)
-   [Contributing](#contributing)
-   [License](#license)

## Features

This repository demonstrates the implementation of the following microservices patterns:

*   **Service Discovery:** Using Spring Cloud Netflix Eureka for service registration and discovery.
*   **API Gateway:** Implementing a centralized entry point with Spring Cloud Gateway for routing, and potentially other cross-cutting concerns.
*   **Centralized Configuration:** Managing application configurations externally with Spring Cloud Config Server and Client.
*   **Resilience & Fault Tolerance:** Applying the Circuit Breaker pattern using Resilience4j to prevent cascading failures.

## Prerequisites

Before running these examples, ensure you have the following installed:

*   **Java Development Kit (JDK) 17 or higher**
*   **Apache Maven 3.6.0 or higher**
*   An IDE like IntelliJ IDEA, VS Code, or Eclipse (optional, but recommended for development)

## Project Structure

The repository is organized into separate Spring Boot projects, each demonstrating a specific microservice pattern:




## How to Run

To run these examples, you will typically need to start the infrastructure services first (Eureka, Config Server, Gateway) before starting the individual microservices.

**General Steps for each project:**

1.  Navigate to the project directory (e.g., `cd eureka-server`).
2.  Build the project: `mvn clean install`
3.  Run the Spring Boot application: `mvn spring-boot:run` or execute the main class from your IDE.

---

### 1. Service Discovery (Eureka Server & Client)

This setup involves the `eureka-server` and `user-service`.

1.  **Start Eureka Server:**
    *   Go to `eureka-server` directory.
    *   Run `mvn spring-boot:run` (default port: `8761`).
    *   Verify by opening `http://localhost:8761` in your browser. You should see the Eureka dashboard.

2.  **Start User Service (Eureka Client):**
    *   Go to `user-service` directory.
    *   Run `mvn spring-boot:run` (default port: `8081`).
    *   Refresh `http://localhost:8761`. You should now see `USER-SERVICE` registered.
    *   Test the user service directly: `http://localhost:8081/users/1`

---

### 2. API Gateway (Spring Cloud Gateway)

This uses the previously started `eureka-server` and `user-service`.

1.  **Ensure Eureka Server and User Service are running.** (See Section 1)

2.  **Start API Gateway:**
    *   Go to `api-gateway` directory.
    *   Run `mvn spring-boot:run` (default port: `8080`).
    *   The gateway will register with Eureka and use it to find `user-service`.

3.  **Test via Gateway:**
    *   Open `http://localhost:8080/users/1`. This request will be routed by the API Gateway to the `user-service`.

---

### 3. Centralized Configuration (Spring Cloud Config Server & Client)

This setup involves the `config-server` and `my-service`.

1.  **Prepare Config Server Local Repository:**
    *   Ensure the `config-repo` directory exists inside `config-server` and contains `my-service.yml` as described in the code example.

2.  **Start Config Server:**
    *   Go to `config-server` directory.
    *   Run `mvn spring-boot:run` (default port: `8888`).
    *   Verify configuration is accessible: `http://localhost:8888/my-service/default` (or `http://localhost:8888/my-service/dev` if you add a `my-service-dev.yml`).

3.  **Start My Service (Config Client):**
    *   Go to `my-service` directory.
    *   Run `mvn spring-boot:run` (default port: `8082`).
    *   The `my-service` will automatically fetch its configuration from the `config-server` during startup.

4.  **Test My Service:**
    *   Open `http://localhost:8082/greet`. You should see the greeting fetched from `my-service.yml` via the Config Server.

---

### 4. Resilience (Resilience4j Circuit Breaker)

This example is standalone and demonstrates a single service using Resilience4j.

1.  **Start Resilience Demo Service:**
    *   Go to `resilience-demo-service` directory.
    *   Run `mvn spring-boot:run` (default port: `8083`).

2.  **Test Circuit Breaker:**
    *   **Success:** `http://localhost:8083/call-backend-a?fail=false` (should always succeed)
    *   **Failure:** `http://localhost:8083/call-backend-a?fail=true`
        *   Call the `fail=true` endpoint repeatedly (e.g., 5-6 times).
        *   Observe the console output. After a few failures, the circuit will open, and subsequent calls will immediately return the fallback message without executing the actual service logic.
        *   Wait for about 5 seconds (the `waitDurationInOpenState` in `application.yml`). The circuit will transition to `HALF_OPEN`.
        *   Call `http://localhost:8083/call-backend-a?fail=false` a few times. If these calls succeed, the circuit will close. If they fail again, it will re-open.
    *   **Monitor Circuit Breaker State:** `http://localhost:8083/actuator/circuitbreakers`

---

## Key Technologies Used

*   **Spring Boot:** For rapid application development and standalone, production-ready Spring applications.
*   **Spring Cloud:** A set of tools for common patterns in distributed systems.
    *   **Spring Cloud Netflix Eureka:** Service Discovery.
    *   **Spring Cloud Gateway:** API Gateway.
    *   **Spring Cloud Config:** Centralized Configuration.
*   **Resilience4j:** A lightweight, easy-to-use fault tolerance library for Java 8 and beyond.
*   **Maven:** Build automation tool.

## Contributing

Feel free to fork this repository, open issues, or submit pull requests if you have suggestions, improvements, or find any bugs.

## License

This project is open-source and available under the [MIT License](LICENSE).
