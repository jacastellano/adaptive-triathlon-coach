# MVP Scope

## Objective

The objective of the MVP is to validate whether an AI-powered application can help an amateur triathlete adapt training decisions based on a baseline plan, target races, performance metrics, completed activities, and subjective athlete status.

The MVP should prove that the system can answer a practical question:

> Based on what was planned, what I have actually done, and how I currently feel, what should I train next?

## MVP Principles

- The system adapts an existing baseline training plan.
- The system does not generate a complete training plan from scratch.
- The user remains in control of the final training decision.
- Recommendations must be practical, understandable, and aligned with the athlete’s context.
- The MVP should prioritize usefulness over advanced analytics.
- Manual input is acceptable for the first version.
- External integrations are not required for the MVP.

## In Scope

The MVP will include the following capabilities:

### 1. Race Management

The system must allow the user to define target races, including:

- race name;
- race date;
- race distance;
- priority classification: A, B, or C;
- optional notes.

### 2. Baseline Training Plan

The system must support a baseline training plan including:

- training phases;
- phase dates;
- weekly objectives;
- estimated weekly training hours;
- general weekly availability;
- planned sessions.

The baseline plan may be created externally with ChatGPT and then stored in the application.

### 3. Performance Metrics and Training Zones

The system must allow the user to register performance metrics by discipline, such as:

- swimming CSS or pace zones;
- cycling FTP or power zones;
- running pace, heart rate, or threshold zones.

Each metric should include:

- discipline;
- value;
- date of test or estimation;
- optional notes.

### 4. Garmin Activity Import

The system must allow the user to manually upload Garmin activity files.

Supported formats for the MVP:

- ZIP;
- FIT;
- TCX.

The system should extract relevant training data where possible, such as:

- sport type;
- duration;
- distance;
- pace or speed;
- heart rate;
- power;
- cadence;
- elevation;
- laps or intervals, when available.

### 5. Athlete Subjective Status

The system must allow the user to register subjective status information, such as:

- fatigue;
- sleep quality;
- stress;
- motivation;
- muscle soreness or pain;
- available time;
- free text notes.

This information will be used to contextualize recommendations.

### 6. Weekly Training Proposal

The system must generate a weekly training proposal aligned with:

- target races;
- current training phase;
- baseline plan;
- recent completed activities;
- performance metrics;
- subjective athlete status.

The proposal should include:

- planned sessions for the week;
- objective of each session;
- expected intensity;
- estimated duration;
- relevant zones or target ranges;
- short reasoning behind the recommendation.

### 7. Activity Report

After importing a completed activity, the system must generate an activity report including:

- summary of the activity;
- comparison with the planned session, if applicable;
- intensity analysis;
- relevant observations;
- impact on the current week;
- short recommendation for the next training decision.

### 8. Weekly Report

The system must generate a weekly report including:

- completed training summary;
- planned vs completed comparison;
- distribution by discipline;
- subjective status summary;
- key observations;
- risks or warning signs;
- recommendation for the following week.

## Out of Scope

The MVP will not include:

- automatic integration with Garmin Connect;
- automatic integration with Strava;
- automatic synchronization with external calendars;
- mobile native application;
- multi-user support;
- coach dashboard;
- payments or subscriptions;
- advanced performance modeling;
- CTL, ATL, TSB or similar advanced load metrics;
- full training plan generation from scratch;
- social features;
- notifications;
- race prediction models;
- nutrition planning;
- injury diagnosis;
- medical advice.

## System Inputs

The MVP will use the following inputs:

- target races classified as A, B, or C;
- baseline training plan;
- performance metrics and training zones;
- Garmin activity files;
- subjective athlete status.

## System Outputs

The MVP will generate the following outputs:

- weekly training proposal;
- completed activity report;
- weekly progress and recommendation report.

## Main User Flow

The main MVP flow is:

1. The user defines target races.
2. The user stores a baseline training plan.
3. The user registers performance metrics and training zones.
4. The user uploads completed Garmin activities.
5. The user enters subjective status information.
6. The system analyzes plan, activity data, metrics, and subjective context.
7. The system generates a weekly training proposal.
8. After each activity, the system generates an activity report.
9. At the end of the week, the system generates a weekly report.

## Success Criteria

The MVP will be considered successful if it can:

- generate a coherent weekly proposal from a baseline plan;
- use performance metrics to prescribe useful training intensities;
- analyze Garmin activity files with enough accuracy to summarize completed workouts;
- compare planned and completed training;
- include subjective athlete status in its recommendations;
- produce clear and actionable reports;
- help the user make better training decisions without requiring excessive manual work.

## Open Questions

- Should the first version store the baseline training plan manually or import it from Markdown?
- Which Garmin format should be prioritized first: FIT, TCX, or ZIP?
- How detailed should the weekly training proposal be in the first version?
- Should athlete subjective status be registered daily, weekly, or both?
- Should activity reports be generated automatically after upload or manually on request?
- What data model should be used for planned sessions and completed activities?
- Should AI recommendations be stored as reports or generated dynamically each time?