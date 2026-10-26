# Full-Stack Application Architecture

## 1. Overview

A full-stack application combines a frontend, backend, database, and any required external services. Each component has a specific responsibility, and they communicate to provide a complete application.

## 2. Roles of the Components

| Component | Responsibility | Example technologies |
|---|---|---|
| Frontend | Displays the interface and handles user interactions | HTML, CSS, JavaScript, React |
| Backend | Processes requests and implements business logic | Node.js, Express.js, Python, Flask |
| API | Defines communication between application components | REST, HTTP, JSON |
| Database | Stores and retrieves persistent information | PostgreSQL |
| External services | Provide third-party functionality | Weather or payment APIs |
| Infrastructure | Hosts and supports application operation | AWS |

## 3. How a Request Works

1. A user interacts with the frontend.
2. The frontend sends an HTTP request to a backend endpoint.
3. The backend validates the request and executes the required logic.
4. If needed, the backend queries or updates the database or contacts an external service.
5. The backend returns a response, commonly as JSON.
6. The frontend processes the response and updates the user interface.

## 4. Example: Weather Application

A React weather page sends a request to an Express backend. The backend returns weather information in JSON format. React receives the response, updates its state, and displays the weather details.

Example response:

    {
      "location": "Mumbai",
      "temperature": 28,
      "condition": "Cloudy"
    }

This demonstrates the connection between frontend development, backend APIs, HTTP communication, JSON data, and state management.

## 5. How My Previous Internship Phases Connect

- **Phase 1 — Development fundamentals:** Git/GitHub, Big-O notation, problem-solving, and clean code support collaboration and maintainability.
- **Phase 2 — Full-stack development:** Node.js, Express.js, PostgreSQL, React, and API integration demonstrate how frontend, backend, and database components work together.
- **Phase 3 — AI and prompt engineering:** Prompt design and LLM integration help build applications that use AI capabilities, provided the model is connected securely through the backend or another suitable integration.
- **AWS learning:** Cloud computing, EC2, storage, and IAM concepts help explain how applications can be hosted, their resources managed, and access controlled.

## 6. Conclusion

Full-stack development focuses on implementing the individual components of an application. System design focuses on planning how those components interact and how the overall system can meet requirements for performance, security, reliability, and scalability.
