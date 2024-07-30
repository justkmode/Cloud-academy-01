# Cloud-academy-01
Week 3 - System Design Applications - 🚀 Project - Create your Architecture

### Week 3 - System Design Applications: E-commerce Platform

---

### Part 1: Monolithic Architecture Design

### Core Functionalities:

1. **User Registration:** Handles user signup, login, and profile management.
2. **Product Catalog:** Manages product listings, search functionality, and product details.
3. **Shopping Cart:** Allows users to add, remove, and view items in their cart.
4. **Order Processing:** Manages order creation, payment processing, and order tracking.

### High-Level Architecture Diagram:

```
|-----------------------|
|       UI Layer        |
|-----------------------|
        |     |     |
        V     V     V
|----------------------------------|
|         Business Logic Layer     |
|----------------------------------|
| User Management | Product Catalog |
| Shopping Cart   | Order Processing |
|----------------------------------|
        |     |     |
        V     V     V
|----------------------------------|
|        Data Interface Layer      |
|----------------------------------|
| User DB | Product DB | Order DB  |
|----------------------------------|

```

### Discussion:

- **Advantages:**
    - **Simplicity:** A single codebase makes development straightforward.
    - **Uniformity:** Consistent coding standards and development practices.
- **Disadvantages:**
    - **Scalability:** Scaling the application means scaling the entire monolith, which can be inefficient.
    - **Flexibility:** Difficulty in adopting new technologies for different parts of the application.
    - **Deployment:** Any change, regardless of size, requires redeploying the entire application.

---

### Part 2: Refactoring into Microservices

### Microservices:

1. **User Service:** Manages user-related functionalities.
2. **Product Service:** Handles product catalog functionalities.
3. **Cart Service:** Manages the shopping cart.
4. **Order Service:** Processes orders and payments.

### Updated Architecture Diagram:

```
|-------------------|
|       UI Layer    |
|-------------------|
        |     |     |      |     |
        V     V     V      V     V
|--------------------------------------------------|
|              API Gateway/Service Mesh            |
|--------------------------------------------------|
| User Service | Product Service | Cart Service | Order Service |
|--------------------------------------------------|
| User DB      | Product DB      | Cart DB      | Order DB      |
|--------------------------------------------------|

```

### Discussion:

- **Advantages:**
    - **Scalability:** Each service can be scaled independently based on demand.
    - **Flexibility:** Different services can be developed using the most suitable technology stack.
    - **Deployment:** Independent deployment of services reduces the risk and impact of changes.
- **Challenges:**
    - **Deployment Complexity:** Requires robust CI/CD pipelines for each service.
    - **Development Complexity:** Increased complexity in managing inter-service communication and data consistency.
    - **Consistency:** Ensuring data consistency across services can be challenging and may require implementing patterns like Sagas.

---

### Part 3: Incorporating Serverless Architecture

### Serverless Functions:

1. **User Authentication:** Handled by AWS Lambda functions triggered by API Gateway.
2. **Payment Processing:** Managed by Lambda functions for handling payments securely.

### Updated Architecture Diagram:

```
|-------------------|
|       UI Layer    |
|-------------------|
        |     |     |      |     |
        V     V     V      V     V
|--------------------------------------------------|
|              API Gateway/Service Mesh            |
|--------------------------------------------------|
| User Service | Product Service | Cart Service | Order Service |
|--------------------------------------------------|
| User DB      | Product DB      | Cart DB      | Order DB      |
|--------------------------------------------------|
          |                        |                    |
          V                        V                    V
     Lambda for Auth          Lambda for Payment  Lambda for Order Processing

```

### Discussion:

- **Benefits:**
    - **Scaling:** Functions automatically scale with the number of requests.
    - **Cost:** Pay-per-use model can be more cost-effective for variable loads.
    - **Operational Management:** Reduced operational overhead as the cloud provider manages the infrastructure.
- **Challenges:**
    - **Cold Starts:** Serverless functions can have latency issues during cold starts.
    - **Complexity:** Integrating serverless functions with the existing microservices architecture requires careful planning.
    - **Vendor Lock-In:** Heavy reliance on a specific cloud provider's services.

---

### Comparison Report

### Scalability:

- **Monolithic:** Limited by the capacity of the single instance it runs on.
- **Microservices:** High scalability, each service can be independently scaled.
- **Serverless:** Automatic and seamless scaling based on demand.

### Development Complexity:

- **Monolithic:** Lower complexity, single codebase.
- **Microservices:** Higher complexity due to multiple services and inter-service communication.
- **Serverless:** Medium complexity, but managing functions and integration with services can be challenging.

### Deployment:

- **Monolithic:** Simple but can be risky as the entire application must be deployed together.
- **Microservices:** Complex, requires sophisticated CI/CD pipelines.
- **Serverless:** Simplifies deployment of individual functions but managing versions and integrations can be complex.

### Maintenance:

- **Monolithic:** Easier to maintain a single codebase but difficult to manage as it grows.
- **Microservices:** Easier to maintain smaller, focused services but requires strong governance.
- **Serverless:** Low maintenance for infrastructure, but function code must be well-managed.

### Cost Implications:

- **Monolithic:** Costly for large-scale applications due to resource wastage.
- **Microservices:** More cost-effective but requires careful resource management.
- **Serverless:** Cost-efficient for variable loads, pay-per-use model.

### Suitability:

- **Monolithic:**
    - **Small Scale:** Suitable for small, less complex applications.
    - **Consistent Load:** Better for applications with stable and predictable load.
- **Microservices:**
    - **Large Scale:** Ideal for large, complex applications with diverse functionalities.
    - **Variable Load:** Suitable for applications with varying load patterns.
- **Serverless:**
    - **Variable Load:** Best for applications with highly variable load.
    - **Event-Driven:** Suitable for event-driven workloads and applications needing rapid scalability.

---

### Conclusion

Each architectural style has its own strengths and trade-offs. The choice depends on the application's scale, complexity, and workload patterns. Understanding these differences helps in making informed decisions to build efficient, scalable, and maintainable systems.
