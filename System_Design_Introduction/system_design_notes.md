# Introduction to System Design

## 1. What Is System Design?

System design is the process of planning how different components of a software application will work together. It defines the application's architecture, components, communication, data storage, security, performance, and ability to handle growth.

**Example:** Before building an online shopping website, we decide how customers will browse products, how the server will process orders, where product details will be stored, and how payments will be handled.

## 2. Why Is System Design Important?

- **Scalability:** Helps an application handle more users and requests.
- **Performance:** Helps reduce delays and improve response times.
- **Reliability:** Helps the system continue working when a component fails.
- **Security:** Protects user information and application resources.
- **Maintainability:** Makes the application easier to update and debug.
- **Cost efficiency:** Helps select appropriate resources without unnecessary expense.

## 3. Client-Server Architecture

Client-server architecture is a model in which a client sends requests to a server, and the server processes those requests and returns responses.

- **Client:** The application or device making a request, such as a web browser.
- **Server:** Receives requests, performs processing, and sends responses.
- **Request:** A message sent from the client to the server.
- **Response:** The result returned by the server.
- **HTTP/HTTPS:** Common protocols used for communication between web clients and servers.

**Example:** When a user opens a weather application, the frontend requests weather information from the backend API. The backend retrieves the required data and returns it to the frontend.

## 4. Components of a Full-Stack Application

### Frontend
The frontend is the user-facing part of the application. It displays information and accepts user input.

**Technologies:** HTML, CSS, JavaScript, React.

### Backend
The backend processes requests, applies business logic, validates input, and communicates with databases and external services.

**Technologies:** Node.js, Express.js, Python, Flask.

### Database
The database stores and manages application data, such as user accounts, products, orders, or travel entries.

**Technologies:** PostgreSQL, MySQL, MongoDB.

### API
An Application Programming Interface (API) defines how different software components communicate. A REST API commonly uses HTTP methods such as GET, POST, PUT, PATCH, and DELETE.

### External Services
These are third-party services that provide additional functionality, such as payment processing, email delivery, maps, weather information, or authentication.

### Hosting and Infrastructure
These provide the environment in which an application runs. Cloud services such as AWS can host servers, store files, manage networks, and support deployment.

## 5. High-Level System Design Concepts

### Scalability
Scalability is the ability of a system to handle increased workload.

- **Vertical scaling:** Increasing the resources of an existing server, such as CPU or RAM.
- **Horizontal scaling:** Adding more servers or instances to share the workload.

### Performance
Performance describes how efficiently a system responds to requests and processes work.

- **Latency:** The time taken to complete a request or receive a response.
- **Throughput:** The amount of work or number of requests processed in a given time.

### Availability and Reliability
Availability refers to how often a system is accessible. Reliability refers to its ability to operate correctly over time.

### Load Balancing
A load balancer distributes incoming requests across multiple servers to avoid overloading one server and improve availability.

### Caching
Caching stores frequently accessed data temporarily so that future requests can be served faster and may require fewer database queries.

### Database Design
Database design determines how information is organized, related, stored, and retrieved. The choice of database depends on data structure, consistency requirements, query patterns, and expected workload.

### Security
Security includes authentication, authorization, input validation, encryption, secure communication, and protecting sensitive data.

### Fault Tolerance
Fault tolerance is the ability of a system to continue providing service when some components fail. Redundancy, backups, and failover mechanisms can help.

### Monolithic and Microservices Architecture
- **Monolithic architecture:** Most application functionality is built and deployed as one application.
- **Microservices architecture:** Application functionality is divided into smaller services that can be developed and deployed independently.

A monolith can be a good starting point for a small application. Microservices can help when independent scaling or deployment is valuable, but they introduce additional complexity.

## 6. Basic System Design Process

1. Understand the application's requirements.
2. Identify the users and main features.
3. Estimate the expected workload when necessary.
4. Identify the frontend, backend, database, APIs, and external services.
5. Draw a high-level architecture.
6. Decide how components communicate and how data flows.
7. Consider security, scalability, performance, and reliability.
8. Identify potential bottlenecks and improve the design.

## 7. Conclusion

System design connects software development with architectural planning. Understanding the responsibilities of each component and how they communicate helps developers build applications that are easier to maintain, secure, reliable, and scalable.

**Learning resource:** [System Design Primer — Donne Martin](https://github.com/donnemartin/system-design-primer)
