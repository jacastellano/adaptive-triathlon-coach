# MVP Decisions

## Purpose

This document records the main product and functional decisions for the Adaptive Triathlon Coach MVP.

Decisions are used to avoid reopening the same questions repeatedly and to keep the MVP scope clear.

---

## DEC-001 - Baseline Training Plan Input

The baseline training plan will be entered manually through a form.

The basic planning unit will be the training week. Each training week must belong to a training phase and include:

- training phase;
- week objective;
- target training hours.

Planned sessions may be defined as part of the weekly planning structure.

---

## DEC-002 - Activity Subjective Feedback

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

## DEC-003 - Activity Report Generation

The activity report will be generated automatically when the user adds a completed workout together with its Garmin file.

Once generated, the report will be stored and can be consulted later at any time.

---

## DEC-004 - Weekly Training Proposal Detail

The weekly training proposal will include, at minimum:

- planned sessions;
- session duration;
- session intensity;
- session objective;
- short reasoning behind the recommendation.

The level of detail may be expanded later when defining the use cases.

---

## DEC-005 - AI Report Persistence

Generated AI reports will be stored.

This includes:

- activity reports;
- weekly reports;
- weekly training proposals.

Storing generated reports will preserve historical context and allow the user to review previous recommendations and analyses.

---

## DEC-006 - Garmin File Import Priority

The MVP will prioritize TCX files first because they are XML-based, easier to inspect, easier to parse, and enough to validate the first activity analysis flow.

ZIP files will be supported as containers when they include TCX or FIT files.

FIT files will be supported later because they are more complete but require specific parsing libraries.

---

## DEC-007 - Minimum Viable Garmin Analysis

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

The MVP does not require advanced performance modeling. The first goal is to generate a clear activity summary and compare it against the planned session.

---

## DEC-008 - Activity Data Point Storage

The MVP will not persist full activity time-series data points by default.

The system may parse detailed data temporarily during activity processing, but the first persisted version will focus on activity summary data and laps or intervals when available.

---

## DEC-009 - Activity Lap Storage

The MVP will store laps or intervals as structured data when they are available in the uploaded activity file.

Lap data is useful for swimming sets, running intervals, bike segments, and activity report generation.

---

## DEC-010 - Weekly Training Proposal Creation

The MVP will support both manual planned sessions and AI-assisted weekly proposals.

The baseline week may contain manually created planned sessions.

When the AI generates a weekly training proposal, the proposal remains separate from the official planned sessions until the user accepts it.

---

## DEC-011 - Weekly Training Proposal Acceptance

A weekly training proposal will not automatically modify the official planned sessions.

The user must explicitly accept the proposal before it creates or updates planned sessions.

For the MVP, the user accepts or rejects the proposal as a whole. Accepting individual sessions may be added later.

---

## DEC-012 - Planned Session Status

Planned sessions may have the following status:

- planned;
- completed;
- partially completed;
- skipped;
- replaced;
- moved;
- cancelled.

A planned session status helps the system compare planned training against completed training and understand whether the athlete followed, modified, skipped, or replaced the original plan.

---

## DEC-013 - Unplanned Activities

The MVP will allow completed activities without linking them to a planned session.

Unplanned activities will still be included in weekly volume, discipline distribution, reports, and recommendations.

The system may suggest a possible match with a planned session, but the user remains responsible for confirming the link.

---

## DEC-014 - Training Zone Structure

The MVP will store training zones as structured ranges whenever possible.

Each zone should include:

- discipline;
- zone name;
- lower bound;
- upper bound;
- unit;
- optional description;
- optional notes.

Free text notes may be used to complement structured ranges, but they should not replace them.

---

## DEC-015 - Athlete Subjective Status Frequency

Athlete subjective status will be registered flexibly by date.

The user may add subjective status entries when needed, especially before generating or adjusting a weekly training proposal.

The MVP will not require mandatory daily check-ins.

Weekly reports may summarize all subjective status entries registered during the week.

---

## DEC-016 - Subjective Status in Weekly Recommendations

Subjective athlete status will actively influence weekly recommendations.

The system should use fatigue, sleep quality, stress, motivation, soreness, pain, available time, and free text notes to decide whether to maintain, reduce, simplify, or adjust planned training.

Poor subjective status should not be treated as simple context. It should be considered a relevant input for recommendation safety and training adaptation.

---

## DEC-017 - Recommendation Safety Rules

AI recommendations must follow basic safety rules:

- do not provide medical diagnosis;
- treat pain, illness, abnormal fatigue, or unusually poor recovery as warning signs;
- recommend reducing, replacing, or skipping intensity when subjective status is poor;
- prioritize consistency, health, and long-term progression over aggressive load increases;
- avoid large sudden increases in training load;
- keep the athlete in control of final training decisions;
- advise professional medical support when symptoms suggest a possible health issue.

---

## DEC-018 - AI Report Storage Structure

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

---

## DEC-019 - Activity Report Regeneration

Activity reports will be generated automatically when the user adds a completed workout with its Garmin file and subjective activity feedback.

The user may manually regenerate an activity report if relevant input data changes, such as subjective feedback or activity-session matching.

Previous versions of the activity report should be preserved.

---

## DEC-020 - Weekly Report Trigger

Weekly reports will be generated manually by the user.

The MVP will not generate weekly reports automatically in the background because automatic notifications and scheduled processing are out of scope.

The user may generate a weekly report when they consider the week completed or when they want to review progress.

---

## DEC-021 - Report Versioning

The MVP will preserve generated report versions over time.

This applies to:

- weekly training proposals;
- activity reports;
- weekly reports.

Keeping report versions preserves the recommendation context available at the time of generation and allows the athlete to review how decisions changed as new data was added.

---

## DEC-022 - Athlete Modeling in Single-User MVP

The MVP will explicitly model Athlete as an internal domain entity, even though the first version supports only one user.

The UI does not need athlete management screens in the MVP.

This keeps the domain model clean and makes future multi-user support easier without adding unnecessary frontend complexity now.

---

## DEC-023 - Baseline Plan Markdown Import

The MVP will not support Markdown import for baseline training plans in the first version.

The baseline plan will be entered manually through forms, as defined in DEC-001.

Markdown import may be considered later if manual plan entry becomes too slow or repetitive.

---

## DEC-024 - MVP First End-to-End Flow

The first MVP vertical slice will be:

Race setup → baseline training week → planned sessions → completed activity upload → activity report → weekly report.

This flow validates the core product idea: comparing planned training against completed training and generating useful recommendations.

Weekly AI proposal generation may be added immediately after this first vertical slice, once the system can already store plans, activities, reports, and subjective feedback.

---

## DEC-025 - Planned Sessions and Completed Activities Data Model

The MVP will model planned sessions and completed activities as separate domain entities.

A planned session represents what the athlete expected to do.

A completed activity represents what the athlete actually did.

A completed activity may optionally be linked to one planned session, but this link is not mandatory.

The MVP must support:

- planned sessions that are completed;
- planned sessions that are partially completed;
- planned sessions that are skipped;
- planned sessions that are replaced;
- planned sessions that are moved;
- planned sessions that are cancelled;
- completed activities without a planned session;
- completed activities imported from Garmin files;
- completed activities with subjective athlete feedback.

A planned session may be linked to more than one completed activity when needed, for example in brick sessions or split workouts.

For the MVP, one completed activity should be linked to at most one planned session.