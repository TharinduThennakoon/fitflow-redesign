# ADR-001: Technology Stack for the FitFlow Redesign

Lab Exercise 05 - Activity 4

| Field | Details |
|---|---|
| **Title** | ADR-001: Adopt a React Native + Node/Express + Python (FastAPI) hybrid stack with PostgreSQL and Firebase for FitFlow redesign |
| **Status** | Accepted |
| **Context** | FitFlow needs a redesign that serves iOS, Android and eventually Web from a single codebase, ships fast with a small dev team, incorporates AI-powered workout planning, camera-based nutrition logging and private real-time social features, while also supporting GDPR/CCPA for health-adjacent data. |
| **Decision** | Use React Native as the client-side framework, Node.js/Express as the primary API layer, a separate Python/FastAPI microservice for AI/ML processing, PostgreSQL as the main relational database, Firebase (Firestore + Auth + Cloud Messaging) for real-time components, Redis for caching and S3-compatible object storage for media. |
| **Consequences** | Positive: fastest possible time-to-market for a small team, best-in-class AI/ML tooling in the isolated Python service, top-notch real-time features powered by Firebase, single codebase for mobile + web apps. Cons: team has to support two backend languages (Node.js + Python) and two databases (PostgreSQL + Firebase), which is slightly more complex than having everything in one system. |

## Key Components

| Component | Responsibility |
|---|---|
| React Native App | Single codebase for iOS, Android, and Web, which renders the Home Dashboard, Workout Planner, Progress, Community and Nutrition screens described in Lab 3. |
| API Gateway / Load Balancer | Transport Layer Security (TLS), routes requests to backend services, and rate limits. |
| Node.js + Express API | REST API providing endpoints for core application features such as authentication, workout planning, community interactions and nutrition logging. |
| AI Microservice (Python/FastAPI) | Generates AI-adaptive workout plans and executes computer-vision inference for nutrition photo recognition. |
| Firebase (Firestore + Cloud Messaging) | Publishes real-time social feed updates, group challenge state, and push notifications. |
| PostgreSQL | Acts as system of record for users, workout plans, and nutrition logs while enforcing relational integrity for reporting. |
| Redis Cache | Caches daily AI-generated workout plan and session data to accelerate Home Dashboard loads. |
| Cloud Storage (S3-compatible) | Stores meal photos and other media referenced by the nutrition logger. |
| Firebase Auth | Handles login, social sign-in, and session token issuance and verification. |

## Data Flow Examples

1. **Personalized workout plans:** the App -> the API -> the AI Microservice (reads the user's schedule and fitness level) -> the generated plan is cached in Redis, persisted in PostgreSQL, and returned to the App (satisfies FR1/FR4 from Lab 2).
2. **Social sharing:** the App writes a challenge/post to Firebase Firestore -> Firebase pushes real-time updates to the other members of the same private group (satisfies FR3).
3. **Nutrition tracking:** the App uploads a meal photo to the Cloud Storage -> the AI Microservice performs a computer-vision recognition -> the recognized nutrition entry is saved in PostgreSQL -> the App is updated with the logged meal (satisfies FR2).

## Security, Scalability & Integration Considerations

- **On security:** TLS for all traffic in transit; AES-256 at rest for PostgreSQL and Cloud Storage; health/fitness data anonymized or pseudonymized (as per Lab 1's data-management plan); GDPR/CCPA-compliant retention/deletion on request.
- **On scalability:** stateless Node.js and FastAPI services running inside a container (Docker) behind the load balancer for horizontal auto-scaling; Redis to absorb heavy read traffic from the Home Dashboard; CDN to cache static assets and media.
- **On integration:** the AI Microservice is deliberately decoupled and hidden behind an internal API so that the ML models (and possibly the language/runtime underneath) can be swapped out without affecting the main Node.js API.

See `architecture-diagram.png` in this folder for the full system diagram.
