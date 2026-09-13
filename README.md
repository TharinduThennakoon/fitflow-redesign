# FitFlow Redesign

Redesign of the FitFlow fitness app, addressing declining retention, app-store ratings, and
onboarding drop-off through AI-powered personalized workouts, private social community
features, and camera-based nutrition tracking.

This repository accompanies IT3060 - Human Computer Interaction, Lab Exercises 01-05
(Year 3, Semester 2, 2026), SLIIT.

## Project Structure

```
fitflow-redesign/
├── frontend/            # React Native app (iOS, Android, Web)
├── backend/             # Node.js + Express API
├── ai-service/          # Python + FastAPI AI/ML microservice
├── docs/
│   ├── tech-stack-comparison.md
│   ├── decision-matrix.md
│   ├── architecture-diagram.png
│   └── adr/
│       └── ADR-001-technology-stack.md
├── .gitignore
└── README.md
```

## Technology Stack

| Layer | Choice |
|---|---|
| Frontend | React Native (iOS, Android, Web via React Native Web) |
| Backend API | Node.js + Express |
| AI/ML service | Python + FastAPI + TensorFlow Lite |
| Primary database | PostgreSQL |
| Real-time / social | Firebase (Firestore + Cloud Messaging) |
| Authentication | Firebase Auth |
| Caching | Redis |
| Media storage | S3-compatible object storage |

See `docs/tech-stack-comparison.md`, `docs/decision-matrix.md`, and
`docs/adr/ADR-001-technology-stack.md` for the full comparison and rationale
(Lab Exercise 05, Activities 1-4).

## Core Features

- **AI Workout Planner** - adaptive plans that fit the time a user actually has available.
- **Nutrition Logger** - camera-based meal logging using computer vision.
- **Community** - private, invite-only groups and challenges.
- **Progress Tracking** - weekly charts, streaks, and goal tracking.

## Design Background

The product research, personas, wireframes, and clickable prototype behind this stack were
produced in Lab Exercises 01-04:

- Lab 1-2: stakeholder research, thematic analysis, personas, and requirements.
- Lab 3: Crazy 8s, interface variants, wireframes, and a clickable low-fidelity prototype.
- Lab 4: usability testing plan, SUS/SEQ results, and prioritized recommendations.
- Lab 5 (this repo): technology stack selection and system architecture.

## Getting Started

```bash
# Frontend
cd frontend
npm install
npm start

# Backend API
cd backend
npm install
npm run dev

# AI microservice
cd ai-service
pip install -r requirements.txt
uvicorn main:app --reload
```

## Contributing

- Create a feature branch from `main`.
- Open a pull request; at least one review is required before merging (branch protection
  enabled on `main`).


