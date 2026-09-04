# OTAMS — Online Tutoring Appointment Management System

[![CI](https://github.com/Diraclol/OTAMS/actions/workflows/ci.yml/badge.svg)](https://github.com/Diraclol/OTAMS/actions/workflows/ci.yml)

An Android app for booking tutoring sessions, built as the team project for SEG 2105 (Introduction
to Software Engineering) at the University of Ottawa, Fall 2025. Three roles: students browse tutors
and book time slots, tutors publish availability and manage bookings, and an administrator approves
new accounts. Firebase Authentication handles sign-in; Cloud Firestore stores tutors, students,
time slots, bookings and ratings.

Java · Android (minSdk 31, targetSdk 36) · Firebase Auth + Firestore · JUnit, Hamcrest, Mockito

## Team

Built by Group 33: Daniel Nguyen, Colin Gordon, Conall McCooeye, Katie Yoon, and [TEAMMATE — the
`ivasliv` handle]. This repository is a mirror of the team's original at
[uOttawaSEG/project-group-33](https://github.com/uOttawaSEG/project-group-33), preserved here with
its full history and every author's commits intact. The original remains the course record.

## Iterations

The project was delivered in four graded iterations, tagged `v0.1` through `v0.4`:

1. Repository setup, registration, login, welcome screens
2. Administrator approval workflow
3. Tutor availability and scheduling logic
4. Student booking flow, ratings, and full integration

## Tests

Local JUnit tests under `app/src/test`, run in CI on every push:

| Test | What it verifies |
|---|---|
| `TutorTest` | Tutor model initialization and field consistency |
| `TutorHandlingTest` | Tutor management: adding, updating, and handling tutor data |
| `TimeSlotTest` | Time-slot creation, validation, and formatting |
| `StudentTest` | Student model properties and session/list-modification behaviour |

## Building

Open in Android Studio, or:

```
./gradlew testDebugUnitTest      # unit tests
./gradlew assembleDebug          # debug APK
```

The app expects an `app/google-services.json` from a Firebase project with Authentication (email /
password) and Firestore enabled. The one in the repo points at the course project.

## Known limitations

This was a first software-engineering course project, and it shows in a few places worth being
honest about:

- **The administrator account is hardcoded in the app** (`Administrator.java`). Anyone with the
  APK can extract it. The right design is server-side roles — a claim on the user record checked by
  the backend's security rules, never by the client. My later project
  [MacTrack](https://github.com/Diraclol/MacTrack) documents that model in its
  [security assessment](https://github.com/Diraclol/MacTrack/blob/main/docs/SECURITY.md); this
  project is part of why that rule exists.
- **Firestore security rules were course-scope**, not production-scope.
- **Tests cover the models, not the Firebase-backed flows.** The booking and approval paths were
  verified manually against the live backend.

## Structure

```
app/src/main/java/com/example/group_33_project/   application source
app/src/main/res/                                  layouts, drawables, strings
app/src/test/                                      JUnit tests
```
