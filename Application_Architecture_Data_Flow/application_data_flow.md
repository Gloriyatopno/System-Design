# Application Architecture & Data Flow Notes


## 1. Application Architecture

Application architecture describes how the components of a software application are organized and how they interact. Each component has a specific responsibility, such as displaying information, processing requests, storing data, or connecting to external services.

## 2. API Communication

An API (Application Programming Interface) allows different software components to communicate.

A REST API commonly uses the following HTTP methods:

- **GET:** Retrieve information.
- **POST:** Create a resource or submit data for processing.
- **PUT:** Replace an existing resource.
- **PATCH:** Partially update a resource.
- **DELETE:** Remove a resource.

JSON is a common format for exchanging data between a frontend and a backend.

Example request:

    GET /api/products

Example JSON response:

    {
      "id": 101,
      "name": "Laptop",
      "price": 45000
    }

## 3. Application Data Flow

Consider a user submitting a form to create a new record.

1. **User input:** The user enters information into a form.
2. **Frontend processing:** The frontend checks basic input requirements and sends an HTTP request.
3. **Backend receives the request:** The API endpoint receives the submitted data.
4. **Validation:** The backend validates the input and checks authorization.
5. **Business logic:** The backend applies the rules required by the application.
6. **Database interaction:** The backend executes a database query to store or retrieve information.
7. **Database response:** The database returns the result or reports an error.
8. **Backend response:** The backend returns an appropriate HTTP status and response, commonly in JSON.
9. **Frontend update:** The frontend displays the result to the user.

**Important:** Not every request requires a database operation. For example, a backend endpoint that returns a calculated result may process the request without reading or writing persistent data.

## 4. Database Integration

The backend communicates with the database through a database driver, library, or ORM (Object-Relational Mapping) tool.

For a PostgreSQL database, the process is:

1. The backend receives a request.
2. It validates the data.
3. It executes a parameterized SQL query.
4. PostgreSQL processes the query.
5. The backend handles the result and sends an appropriate response.

Parameterized queries help prevent SQL injection. Database credentials should be stored securely, and database access should be restricted to authorized components.

## 5. Integrating an AI Service

An AI service can add features such as:

- Text summarization.
- Chatbots and question answering.
- Sentiment analysis.
- Recommendations.
- Text classification.

### AI integration flow

1. The user submits a question or text through the frontend.
2. The frontend sends the request to the backend.
3. The backend validates the input and checks authorization.
4. The backend sends a suitable prompt or request to the AI service.
5. The AI service processes the request and returns a result.
6. The backend validates or handles the result and sends a response to the frontend.
7. The frontend displays the result.

The AI service may be called alongside database operations or independently, depending on the application's requirements.

**Security considerations:** Keep AI API keys on the backend, limit sensitive data shared with external services, handle rate limits and timeouts, and validate the returned output.

## 6. Scalability, Reliability, and Design Trade-offs

### Scalability

Scalability is the ability of an application to handle increased workload.

- Vertical scaling increases the resources of an existing server.
- Horizontal scaling adds more server instances.

### Reliability

Reliability means the application continues to operate correctly. It can be improved through error handling, monitoring, backups, appropriate timeouts, and recovery mechanisms.

### Common design trade-offs

**1. Monolith vs. microservices**

- A monolith is generally simpler to develop, deploy, and debug initially.
- Microservices allow independent deployment and scaling but add networking and operational complexity.

**2. Database queries vs. caching**

- Direct database queries are straightforward and can provide current data.
- Caching may reduce latency and database load, but introduces invalidation and stale-data concerns.

**3. Synchronous vs. asynchronous processing**

- Synchronous processing is simple when the user needs an immediate result.
- Asynchronous processing can handle long-running tasks without making the user wait for the entire operation, but requires additional coordination.

**4. AI response quality vs. latency and cost**

- Larger or more capable models may improve results for some tasks.
- They may also increase response time and cost.
- Smaller models or simpler non-AI solutions may be sufficient for straightforward tasks.

## 7. Connection to Previous Internship Phases

- **Git and clean code:** Support collaboration, version control, and maintainability.
- **React:** Provides the frontend and manages user interactions and application state.
- **Node.js and Express.js:** Handle API requests and application logic.
- **PostgreSQL:** Stores structured application data.
- **AWS:** Provides cloud infrastructure for hosting and operating applications.
- **AI and prompt engineering:** Help integrate language-model features into an application through a suitable backend integration.

Together, these skills demonstrate how an application can be designed, developed, integrated, and deployed.

## 8. Conclusion

Application architecture defines the responsibilities and connections between components. Data flow explains how information travels from the user through the frontend and backend to databases or external services and back. Good design balances maintainability, security, performance, reliability, scalability, and cost.

**Learning resource:** [System Design Primer — Donne Martin](https://github.com/donnemartin/system-design-primer)
