# MVP Scope

## Objective

The objective of the MVP is to validate whether an AI-powered application can help an amateur triathlete adapt training decisions based on a baseline plan, target races, performance metrics, completed activities, and subjective athlete status.

The MVP should prove that the system can answer a practical question:

> Based on what was planned, what I have actually done, and how I currently feel, what should I train next?

---

## MVP Principles

- The system adapts an existing baseline training plan.
- The system does not generate a complete training plan from scratch.
- The user remains in control of the final training decision.
- Recommendations must be practical, understandable, and aligned with the athlete’s context.
- Subjective athlete status must actively influence recommendations.
- The MVP should prioritize usefulness over advanced analytics.
- Manual input is acceptable for the first version.
- External integrations are not required for the MVP.
- The MVP should preserve generated recommendations and reports for later review.
- The MVP must avoid medical diagnosis or medical advice.

---

## In Scope

The MVP will include the following capabilities:

### 1. Race Management

The system must allow the user to define target races, including:

- race name;
- race date;
- race distance;
- priority classification: A, B, or C;
- optional notes.

---

### 2. Baseline Training Plan

The system must support a baseline training plan including:

- training phases;
- phase dates;
- weekly objectives;
- target weekly training hours;
- general weekly availability;
- planned sessions.

The baseline training plan will be entered manually through forms.

The basic planning unit will be the training week. Each training week must belong to a training phase and include:

- training phase;
- week objective;
- target training hours;
- planned sessions, when defined.

The baseline plan may be created externally with ChatGPT, but the MVP will not support Markdown import in the first version.

---

### 3. Planned Sessions

The system must support planned sessions as separate entities from completed activities.

A planned session represents what the athlete expected to do.

A planned session should include:

- training week;
- discipline;
- planned date;
- estimated duration;
- expected intensity;
- objective;
- target zones or ranges, when applicable;
- description or notes;
- status.

Planned sessions may have the following status:

- planned;
- completed;
- partially completed;
- skipped;
- replaced;
- moved;
- cancelled.

A planned session may be linked to more than one completed activity when needed, for example in brick sessions or split workouts.

---

### 4. Performance Metrics and Training Zones

The system must allow the user to register performance metrics by discipline, such as:

- swimming CSS or pace reference;
- cycling FTP or power reference;
- running pace, heart rate, or threshold reference.

Each metric should include:

- discipline;
- value;
- unit;
- date of test or estimation;
- optional notes.

The MVP will store training zones as structured ranges whenever possible.

Each training zone should include:

- discipline;
- zone name;
- lower bound;
- upper bound;
- unit;
- optional description;
- optional notes.

Free text notes may complement structured ranges, but they should not replace them.

---

### 5. Garmin Activity Import

The system must allow the user to manually upload Garmin activity files.

For the MVP, TCX files will be prioritized first because they are XML-based, easier to inspect, easier to parse, and enough to validate the first activity analysis flow.

ZIP files will be supported as containers when they include TCX or FIT files.

FIT files may be supported later because they are more complete but require specific parsing libraries.

The first Garmin activity analysis should extract, when available:

- sport type;
- activity date;
- duration;
- distance;
- average pace or speed;
- average heart rate;
- maximum heart rate;
- average power;
- normalized power, if available;
- cadence;
- elevation gain;
- laps or intervals.

The MVP will store laps or intervals as structured data when they are available in the uploaded activity file.

The MVP will not persist full activity time-series data points by default. The system may parse detailed data temporarily during activity processing, but the first persisted version will focus on activity summary data and laps or intervals when available.

---

### 6. Completed Activities

The system must support completed activities as separate entities from planned sessions.

A completed activity represents what the athlete actually did.

A completed activity may optionally be linked to one planned session, but this link is not mandatory.

The MVP must support:

- completed activities linked to planned sessions;
- completed activities without a planned session;
- completed activities imported from Garmin files;
- completed activities with subjective athlete feedback.

For the MVP, one completed activity should be linked to at most one planned session.

Unplanned activities will still be included in weekly volume, discipline distribution, reports, and recommendations.

The system may suggest a possible match between a completed activity and a planned session, but the user remains responsible for confirming the link.

---

### 7. Activity Subjective Feedback

For each completed activity, the user will manually provide subjective feedback.

The feedback will include:

- perceived effort from 1 to 10;
- perceived sensations:
  - very weak;
  - weak;
  - normal;
  - strong;
  - very strong;
- free text comment.

This subjective feedback will be used together with Garmin activity data to generate the activity report and support future recommendations.

---

### 8. Athlete Subjective Status

The system must allow the user to register subjective status information, such as:

- fatigue;
- sleep quality;
- stress;
- motivation;
- muscle soreness;
- pain notes;
- available time;
- free text notes.

Athlete subjective status will be registered flexibly by date.

The user may add subjective status entries when needed, especially before generating or adjusting a weekly training proposal.

The MVP will not require mandatory daily check-ins.

Weekly reports may summarize all subjective status entries registered during the week.

Subjective athlete status must actively influence weekly recommendations. The system should use fatigue, sleep quality, stress, motivation, soreness, pain, available time, and free text notes to decide whether to maintain, reduce, simplify, or adjust planned training.

Poor subjective status should not be treated as simple context. It should be considered a relevant input for recommendation safety and training adaptation.

---

### 9. Weekly Training Proposal

The system must generate a weekly training proposal aligned with:

- target races;
- current training phase;
- baseline plan;
- planned sessions;
- recent completed activities;
- performance metrics;
- training zones;
- subjective athlete status.

The proposal should include:

- planned sessions for the week;
- objective of each session;
- expected intensity;
- estimated duration;
- relevant zones or target ranges;
- short reasoning behind the recommendation.

The MVP will support both manual planned sessions and AI-assisted weekly proposals.

The baseline week may contain manually created planned sessions.

When the AI generates a weekly training proposal, the proposal remains separate from the official planned sessions until the user accepts it.

A weekly training proposal will not automatically modify the official planned sessions. The user must explicitly accept the proposal before it creates or updates planned sessions.

For the MVP, the user accepts or rejects the proposal as a whole. Accepting individual sessions may be added later.

---

### 10. Activity Report

After importing a completed activity with its Garmin file and subjective activity feedback, the system must generate an activity report including:

- summary of the activity;
- comparison with the planned session, if applicable;
- intensity analysis;
- relevant observations;
- impact on the current week;
- short recommendation for the next training decision.

The activity report will be generated automatically when the user adds a completed workout together with its Garmin file and subjective feedback.

The user may manually regenerate an activity report if relevant input data changes, such as subjective feedback or activity-session matching.

Previous versions of the activity report should be preserved.

---

### 11. Weekly Report

The system must generate a weekly report including:

- completed training summary;
- planned vs completed comparison;
- distribution by discipline;
- subjective status summary;
- key observations;
- risks or warning signs;
- recommendation for the following week.

Weekly reports will be generated manually by the user.

The MVP will not generate weekly reports automatically in the background because automatic notifications and scheduled processing are out of scope.

The user may generate a weekly report when they consider the week completed or when they want to review progress.

---

### 12. AI Report Storage

AI-generated reports will be stored.

This includes:

- weekly training proposals;
- activity reports;
- weekly reports.

AI-generated reports will store both:

- the full generated text;
- a minimal structured summary.

The full generated text preserves the complete AI output.

The structured summary allows basic querying, filtering, comparison, and future UI improvements.

For the MVP, the structured part may include fields such as:

- summary;
- observations;
- risks;
- recommendation;
- planned vs completed comparison;
- discipline distribution, when applicable.

The MVP will preserve generated report versions over time.

Keeping report versions preserves the recommendation context available at the time of generation and allows the athlete to review how decisions changed as new data was added.

---

### 13. Recommendation Safety Rules

AI recommendations must follow basic safety rules:

- do not provide medical diagnosis;
- treat pain, illness, abnormal fatigue, or unusually poor recovery as warning signs;
- recommend reducing, replacing, or skipping intensity when subjective status is poor;
- prioritize consistency, health, and long-term progression over aggressive load increases;
- avoid large sudden increases in training load;
- keep the athlete in control of final training decisions;
- advise professional medical support when symptoms suggest a possible health issue.

---

## Out of Scope

The MVP will not include:

- automatic integration with Garmin Connect;
- automatic integration with Strava;
- automatic synchronization with external calendars;
- mobile native application;
- multi-user support in the UI;
- athlete management screens;
- coach dashboard;
- payments or subscriptions;
- advanced performance modeling;
- CTL, ATL, TSB or similar advanced load metrics;
- full activity time-series persistence by default;
- full training plan generation from scratch;
- Markdown import for baseline training plans;
- social features;
- notifications;
- automatic background weekly report generation;
- race prediction models;
- nutrition planning;
- injury diagnosis;
- medical advice.

---

## System Inputs

The MVP will use the following inputs:

- target races classified as A, B, or C;
- baseline training plan;
- training phases;
- training weeks;
- planned sessions;
- performance metrics and structured training zones;
- Garmin activity files;
- completed activities;
- activity subjective feedback;
- athlete subjective status.

---

## System Outputs

The MVP will generate the following outputs:

- weekly training proposal;
- completed activity report;
- weekly progress and recommendation report;
- stored history of generated reports and recommendations;
- structured report summaries for basic querying and future UI improvements.

---

## Main User Flow

The first MVP vertical slice will be:

1. The user defines target races.
2. The user stores a baseline training plan.
3. The user defines a baseline training week.
4. The user creates planned sessions.
5. The user registers performance metrics and training zones.
6. The user uploads a completed Garmin activity.
7. The user enters subjective activity feedback.
8. The system analyzes the activity data, planned session, metrics, zones, and subjective feedback.
9. The system generates an activity report.
10. The user enters athlete subjective status when needed.
11. The user generates a weekly report manually.
12. The system compares planned and completed training and provides recommendations.

Weekly AI proposal generation may be added immediately after this first vertical slice, once the system can already store plans, activities, reports, and subjective feedback.

---

## Success Criteria

The MVP will be considered successful if it can:

- store a baseline training structure with target races, phases, weeks, and planned sessions;
- use performance metrics and structured training zones to prescribe useful training intensities;
- manually import Garmin activity files, prioritizing TCX first;
- analyze Garmin activity files with enough accuracy to summarize completed workouts;
- store laps or intervals when available;
- compare planned and completed training;
- support unplanned completed activities;
- include activity subjective feedback in activity reports;
- include athlete subjective status in weekly recommendations;
- actively adapt recommendations based on fatigue, sleep, stress, motivation, soreness, pain, and available time;
- produce clear and actionable activity reports;
- produce clear and actionable weekly reports;
- preserve generated reports and recommendation history;
- help the user make better training decisions without requiring excessive manual work.