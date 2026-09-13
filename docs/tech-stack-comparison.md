# Technology Stack Comparison

Lab Exercise 05 - Activities 1 & 2

## Activity 1: Frontend Framework Comparison

Four options were compared for the redesign of FitFlow. The requirements included a
seamless experience across iOS, Android, and the web, smooth workout animations, camera
based computer vision technology for logging nutritional information and real time social
media features.

| Criterion | Flutter | React Native | Kotlin Multiplatform | Swift |
|---|---|---|---|---|
| Development speed | Fast reload, single codebase | Fast reload, single codebase, extensive component libraries | Medium - shares logic only, separate native UIs still needed | Slow - iOS only, Android needs a separate codebase |
| Code reusability | 95% incl. web | 90% incl. web via React Native Web | 40-60% (business logic only) | 0% (iOS only) |
| Performance | Near native (compiled, Skia renderer) | Near native (New Architecture) | Native performance | Best native performance, but iOS-only |
| Ecosystem support | Strong, Google backed, growing fast | Largest JS ecosystem, Meta backed, huge npm library pool | Newer, smaller community | Mature but iOS-only |
| Learning curve | Requires learning Dart | Easiest for a JS/React background | Requires Kotlin + native UI knowledge (SwiftUI/Jetpack Compose) | Requires Swift + Xcode |
| Web compatibility | Flutter Web supported, decent but heavier bundle | Good via react native web | Compose Multiplatform Web is experimental | None |
| AI/ML integration | Good via tflite_flutter and platform channels | Good via TensorFlow.js/TFLite bridges and native modules | Can call native ML Kit | Best on device, iOS-only |
| Real-time features | Mature (Firebase WebSocket packages) | Mature (Firebase, Socket.io widely used) | Fine, but more native wiring needed | Fine, iOS-only |
| Maintenance cost | Low, one codebase | Low - one codebase, large hiring pool for JS devs | Medium - still two native UI layers to maintain | High - fully separate Android app required |
| Security | Comparable when best practices followed | Comparable when best practices followed | Slightly more OS-level control | Slightly more OS-level control (iOS only) |

### Recommendation

I would recommend **React Native** for the FitFlow redesign because it provides the
fastest route to a single codebase covering iOS, Android, and a future web dashboard (via
React Native Web) that would directly address the case study's requirement for a seamless
cross-platform experience. It also best fits the existing skill set on this project
(MERN-stack/JavaScript experience) and reduces onboarding time for the team. The AI/ML
integration story (TensorFlow Lite bridges, cloud inference calls) is mature enough for the
AI workout engine and camera-based nutrition logging, and its real-time library support
(Firebase, Socket.io) directly serves the social/community features.

Flutter was the closest alternative and remains a strong option if the team were starting
with a Dart-first skill set, but React Native's larger ecosystem and lower switching cost
make it the better fit here. Kotlin Multiplatform and Swift/SwiftUI were not selected as
the primary framework because it would require maintaining separate native UI layers (KMP)
or an entirely separate Android codebase (Swift), which conflicts with the project's
speed-to-market and small-team maintainability goals.

## Activity 2: Backend, Database and Authentication Comparison

### Backend Frameworks

| Criterion | Node.js / Express | Python | Go |
|---|---|---|---|
| Performance | I/O-heavy APIs (event loop) Good | Good, async-first, performs well for ML model serving | Excellent well compiled, very high concurrency |
| AI/ML integration | Requires exposing a Python service for most ML libraries. | Best - native access to TensorFlow/scikit-learn | Weak - few native ML ecosystem support |
| Ecosystem | Huge npm ecosystem, same language as RN frontend | Strong, particularly for data/AI tooling | Smaller web ecosystem but very strong for infra tooling |
| Learning curve | Low learning curve for a JS/MERN-stack developer | Low-medium (Python is accessible) | Medium-high (new language, less familiar syntax) |
| Real-time support | Excellent (Socket.io, native WebSockets support) | Good (WebSocket support in FastAPI) | Good (goroutines good for real time) but more manual wiring |
| Team fit | Full-stack MERN experience match | Would add a second language to the stack | Would add a third, unfamiliar language |

### Database Options

| Criterion | PostgreSQL | MongoDB | Firebase (Firestore) | DynamoDB |
|---|---|---|---|---|
| Scalability | Vertically scaled, horizontally scalable with read replicas/partitioning | Scales horizontally well out of the box | Easy to scale automatically, managed by Google | Massive auto-scaling, AWS managed |
| Query performance for relational data | Excellent join capability for users/workouts/social connections | Better for simple joins only | Limited query flexibility (NoSQL document model) | Very limited flexibility for ad hoc queries |
| Health/fitness data handling | Strong relational integrity + JSONB for flexible fields (e.g. workout plans) | Flexible schema fits various plan structures but does not enforce integrity | Best for activity logs, not so good for relational integrity | Good for high volume simple lookups not relational data |
| Real-time sync | Requires extra tooling (e.g. Supabase Realtime, LISTEN/NOTIFY) | Change Streams available but more involved setup | Best in class for built-in real-time listeners | Streams available but not developer friendly |
| Cost/ops overhead | Self-managed or managed (RDS/Cloud SQL), predictable cost | Atlas (managed) available, not cheap | Pay for what you read/write, and it can scale up | Pay by request, can be cost effective at scale but have complex pricing |

### Authentication Options

| Criterion | Firebase Auth | AWS Cognito | Auth0 | Supabase Auth |
|---|---|---|---|---|
| Ease of integration | It's easiest if you're already using Firebase for its real-time capabilities | More setup, best if the rest of infra is AWS | Very developer-friendly SDKs | Easy assuming the user already has a Supabase/Postgres project |
| Social login support | It's excellent (Google/Apple/Facebook) | Good, more configuration needed | Excellent, wide provider list | Good provider list, growing |
| Compliance features | Pretty basic; should be suitable for GDPR/CCPA with suitable data handling | Strong enterprise compliance tooling | Strong enterprise compliance tooling | Open source and transparent, makes auditing easier |
| Cost at scale | Generous free tier, and cheap at the volume FitFlow would be using | Cost effective within AWS ecosystem | Costs take off exponentially with large user bases | Low costs, scales with Supabase plan |

### Recommendation

Node.js/Express is recommended for the primary API because of the shared JavaScript
context with the React Native frontend (for reduced context-switching in a small team)
plus its robust real-time features for the social features. A small Python/FastAPI
microservice is recommended for the AI workout recommendation and nutrition
computer-vision models, since Python's ML ecosystem (TensorFlow, OpenCV, scikit-learn) is
unmatched - this hybrid approach allows the main app to remain rapid to develop while
giving the AI features the best possible tooling.

For the database, a hybrid is recommended: PostgreSQL as the system of record for the
users, workout plans, and nutrition logs (where relational integrity and health-data
structure are important), paired with Firebase Firestore for the real-time
social/community features (feeds, notifications, live group activity) where Firestore's
built-in real-time sync is unmatched.

Firebase Auth is recommended for authentication since the app has already been using
Firebase for real-time data - this avoids adding an extra vendor, keeps costs low at
FitFlow's expected scale, and provides the social login options (Google/Apple) that one
would expect in a modern consumer fitness app. GDPR/CCPA compliance (already established
as a requirement in Lab Exercise 01's consent and data-management plan) is addressed at
the data-handling layer - encryption at rest/in transit and anonymized identifiers -
rather than requiring a heavier enterprise IAM tool like Cognito or Auth0 at this stage;
FitFlow is a consumer wellness app rather than a HIPAA-covered entity, and GDPR/CCPA (not
HIPAA) is the binding compliance requirement.
