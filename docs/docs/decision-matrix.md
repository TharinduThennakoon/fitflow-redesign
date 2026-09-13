# Technology Decision Matrix

Lab Exercise 05 - Activity 3

Three complete stack options were scored 1 (poor) to 5 (excellent) in accordance with
weighted criteria that prioritized FitFlow's emphasis on rapid iteration by a small team
and strong AI/ML support with reliable real-time social features.

| Criterion | Weight | A - React Native + Node/Express + Postgres/Firebase + Firebase Auth | B - Flutter + NestJS + MongoDB + Auth0 | C - Kotlin Multiplatform + Go + DynamoDB + AWS Cognito |
|---|---|---|---|---|
| Performance | 20% | 4 | 4 | 5 |
| Scalability | 15% | 4 | 4 | 5 |
| Development speed | 20% | 5 | 4 | 2 |
| Security/Compliance | 15% | 4 | 4 | 5 |
| Cost | 10% | 5 | 3 | 3 |
| AI/ML support | 10% | 4 | 4 | 3 |
| Maintainability | 10% | 5 | 4 | 3 |

## Weighted Totals

| Option | Weighted Score (/5) |
|---|---|
| **A - React Native + Node/Express + PostgreSQL/Firebase + Firebase Auth (Recommended)** | **4.40** |
| B - Flutter + NestJS + MongoDB + Auth0 | 3.90 |
| C - Kotlin Multiplatform + Go + DynamoDB + AWS Cognito | 3.65 |

## Recommended Technology Stack

- **Frontend:** React Native (iOS, Android, Web via React Native Web)
- **Backend:** Node.js + Express (main API), Python + FastAPI (AI microservice)
- **Database:** PostgreSQL (system of record) + Firebase Firestore (real-time social features)
- **Authentication:** Firebase Auth
- **AI/ML:** TensorFlow Lite (on-device) + cloud-hosted models for heavier inference
- **Caching:** Redis (daily workout plan cache, session data)
- **Storage:** Cloud object storage (e.g. S3-compatible) for meal photos and media

Option A appears optimal compared to others since its overall rating is the highest
(4.40/5). This solution is the most cost-effective and quick to develop, which fits best
with the requirement of launching the redesigned website as soon as possible with a small
team. Moreover, its performance and security parameters are sufficient for the needs of
the above-mentioned company, which can be said to match the requirements of the case
study.
