# Use Cases

## Purpose

This document defines the main use cases for the Adaptive Triathlon Coach MVP.

The goal is to describe what the athlete can do with the system and how the system should respond, without defining technical architecture, API contracts, database schema, or UI details.

The MVP is centered around the following practical question:

> Based on what was planned, what I have actually done, and how I currently feel, what should I train next?

---

# Use Case List

## First MVP Vertical Slice

The first MVP vertical slice will include:

- UC-001 - Create Target Race
- UC-002 - Create Training Plan
- UC-003 - Create Training Phase
- UC-004 - Create Training Week
- UC-005 - Create Planned Session
- UC-006 - Register Performance Metric
- UC-007 - Define Training Zones
- UC-008 - Upload Completed Activity
- UC-009 - Add Activity Subjective Feedback
- UC-010 - Generate Activity Report
- UC-011 - Register Athlete Subjective Status
- UC-012 - Generate Weekly Report

## AI Weekly Proposal Flow

The AI weekly proposal flow will include:

- UC-013 - Generate Weekly Training Proposal
- UC-014 - Accept Weekly Training Proposal
- UC-015 - Reject Weekly Training Proposal
- UC-016 - Regenerate Activity Report

---

# UC-001 - Create Target Race

## Goal

Allow the athlete to define a target race that will guide training planning and recommendations.

## Primary Actor

Athlete.

## Preconditions

- The athlete exists in the system.

## Main Flow

1. The athlete opens the race creation flow.
2. The system asks for race information.
3. The athlete enters the race details.
4. The athlete assigns a race priority: A, B, or C.
5. The system validates the required information.
6. The system stores the race.
7. The system makes the race available for training plan context.

## Required Data

- race name;
- race date;
- race distance;
- priority classification: A, B, or C.

## Optional Data

- location;
- notes.

## Validation Rules

- Race name is required.
- Race date is required.
- Race distance is required.
- Race priority must be A, B, or C.
- Race date should not be empty or invalid.

## Output

- A new Race is created.

## Related Domain Concepts

- Athlete
- Race
- Race Priority

---

# UC-002 - Create Training Plan

## Goal

Allow the athlete to store a baseline training plan that will be adapted by the system.

## Primary Actor

Athlete.

## Preconditions

- The athlete exists in the system.
- At least one target race may exist, especially if the plan is linked to a main race.

## Main Flow

1. The athlete opens the training plan creation flow.
2. The system asks for the plan name, dates, and optional main race.
3. The athlete enters the plan details.
4. The athlete optionally links the plan to a main A race.
5. The system validates the information.
6. The system stores the training plan.

## Required Data

- plan name;
- start date;
- end date.

## Optional Data

- main race;
- notes.

## Validation Rules

- Plan name is required.
- Start date is required.
- End date is required.
- End date must be after start date.
- The MVP does not support Markdown import for baseline training plans.

## Output

- A new Training Plan is created.

## Related Domain Concepts

- Athlete
- Race
- Training Plan

---

# UC-003 - Create Training Phase

## Goal

Allow the athlete to divide a training plan into phases such as Prep, Base, Build, Peak, or Taper.

## Primary Actor

Athlete.

## Preconditions

- A Training Plan exists.

## Main Flow

1. The athlete opens the training phase creation flow.
2. The system asks for phase information.
3. The athlete enters the phase name, dates, and objective.
4. The system validates that the phase belongs to an existing training plan.
5. The system stores the training phase.

## Required Data

- training plan;
- phase name;
- start date;
- end date;
- objective.

## Optional Data

- notes.

## Validation Rules

- Training phase must belong to a training plan.
- Phase name is required.
- Start date is required.
- End date is required.
- End date must be after start date.
- Phase dates should fit within the training plan dates.

## Output

- A new Training Phase is created.

## Related Domain Concepts

- Training Plan
- Training Phase

---

# UC-004 - Create Training Week

## Goal

Allow the athlete to create the basic planning unit of the MVP: the training week.

## Primary Actor

Athlete.

## Preconditions

- A Training Plan exists.
- A Training Phase exists.

## Main Flow

1. The athlete opens the training week creation flow.
2. The system asks for week information.
3. The athlete selects the training phase.
4. The athlete enters the week number, dates, objective, and target training hours.
5. The system validates the information.
6. The system stores the training week.

## Required Data

- training phase;
- week number;
- start date;
- end date;
- objective;
- target training hours.

## Optional Data

- notes.

## Validation Rules

- Training week must belong to one training phase.
- Week number is required.
- Start date is required.
- End date is required.
- End date must be after start date.
- Target training hours must be greater than or equal to zero.
- Week dates should fit within the training phase dates.

## Output

- A new Training Week is created.

## Related Domain Concepts

- Training Phase
- Training Week

---

# UC-005 - Create Planned Session

## Goal

Allow the athlete to define what is expected to be trained during a specific training week.

## Primary Actor

Athlete.

## Preconditions

- A Training Week exists.

## Main Flow

1. The athlete opens the planned session creation flow.
2. The system asks for session information.
3. The athlete enters the discipline, planned date, duration, intensity, objective, and optional target zones.
4. The system sets the initial session status to `planned`.
5. The system validates the information.
6. The system stores the planned session.

## Required Data

- training week;
- discipline;
- planned date;
- estimated duration;
- expected intensity;
- objective.

## Optional Data

- session type;
- target zones;
- description;
- notes.

## Validation Rules

- Planned session must belong to one training week.
- Discipline is required.
- Planned date is required.
- Duration must be greater than zero, except for rest sessions.
- Initial status is `planned`.
- Status must be one of:
  - planned;
  - completed;
  - partially completed;
  - skipped;
  - replaced;
  - moved;
  - cancelled.

## Output

- A new Planned Session is created.

## Related Domain Concepts

- Training Week
- Planned Session
- Discipline
- Intensity
- Training Zone

---

# UC-006 - Register Performance Metric

## Goal

Allow the athlete to register a performance reference used to prescribe intensity and analyze completed activities.

## Primary Actor

Athlete.

## Preconditions

- The athlete exists in the system.

## Main Flow

1. The athlete opens the performance metric creation flow.
2. The system asks for metric information.
3. The athlete selects the discipline and metric type.
4. The athlete enters the metric value, unit, test date or estimation date, and optional notes.
5. The system validates the information.
6. The system stores the performance metric.

## Required Data

- discipline;
- metric type;
- value;
- unit;
- test date or estimation date.

## Optional Data

- estimation method;
- notes.

## Validation Rules

- Discipline is required.
- Metric type is required.
- Value is required.
- Unit is required.
- Test date or estimation date is required.
- Value must be valid for the selected metric type.

## Output

- A new Performance Metric is created.

## Related Domain Concepts

- Athlete
- Performance Metric
- Discipline

---

# UC-007 - Define Training Zones

## Goal

Allow the athlete to define structured training zones linked to a performance metric.

## Primary Actor

Athlete.

## Preconditions

- A Performance Metric exists.

## Main Flow

1. The athlete opens the training zone creation flow.
2. The system asks for zone information.
3. The athlete selects the related performance metric.
4. The athlete enters zone name, lower bound, upper bound, unit, and optional description.
5. The system validates the information.
6. The system stores the training zone.

## Required Data

- performance metric;
- discipline;
- zone name;
- lower bound;
- upper bound;
- unit.

## Optional Data

- description;
- notes.

## Validation Rules

- Training zone must belong to one performance metric.
- Lower bound and upper bound are required.
- Upper bound must be greater than or equal to lower bound.
- Unit must match the type of metric when applicable.
- Free text notes may complement structured ranges, but should not replace them.

## Output

- A new Training Zone is created.

## Related Domain Concepts

- Performance Metric
- Training Zone
- Discipline

---

# UC-008 - Upload Completed Activity

## Goal

Allow the athlete to manually upload a Garmin activity file and create a completed activity.

## Primary Actor

Athlete.

## Preconditions

- A Training Week exists.
- A Garmin activity file is available.
- A Planned Session may exist, but is not mandatory.

## Main Flow

1. The athlete opens the completed activity upload flow.
2. The system asks the athlete to select an activity file.
3. The athlete uploads a Garmin activity file.
4. The athlete optionally links the activity to a planned session.
5. The system validates the file format.
6. The system extracts available activity data.
7. The system creates the completed activity.
8. The system stores the activity file metadata.
9. The system stores laps or intervals when available.
10. The system includes the activity in the corresponding training week.

## Supported File Handling

- TCX files are prioritized first.
- ZIP files are supported as containers when they include TCX or FIT files.
- FIT files may be supported later.

## Data Extracted When Available

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

## Alternative Flows

### Invalid File Format

1. The athlete uploads an unsupported file.
2. The system rejects the file.
3. The system explains that the file format is not supported.

### ZIP Without Supported Activity File

1. The athlete uploads a ZIP file.
2. The system inspects the ZIP contents.
3. The system does not find a supported TCX or FIT file.
4. The system rejects the upload and explains the reason.

### Unplanned Activity

1. The athlete uploads an activity without linking it to a planned session.
2. The system stores the completed activity anyway.
3. The system includes it in weekly volume, discipline distribution, reports, and recommendations.

## Validation Rules

- Activity file is required.
- File format must be supported.
- Completed activity must belong to one training week.
- A completed activity may be linked to at most one planned session.
- A completed activity may exist without a planned session.
- Full time-series data points are not persisted by default in the MVP.

## Output

- A new Completed Activity is created.
- An Activity File record is created.
- Activity Laps are created when available.

## Related Domain Concepts

- Training Week
- Planned Session
- Completed Activity
- Activity File
- Activity Lap

---

# UC-009 - Add Activity Subjective Feedback

## Goal

Allow the athlete to register subjective feedback for a completed activity.

## Primary Actor

Athlete.

## Preconditions

- A Completed Activity exists.

## Main Flow

1. The athlete opens the activity feedback flow.
2. The system asks for perceived effort, perceived sensations, and comment.
3. The athlete enters the feedback.
4. The system validates the information.
5. The system stores the activity feedback.
6. The system uses this feedback as context for activity reports and future recommendations.

## Required Data

- completed activity;
- perceived effort from 1 to 10;
- perceived sensations.

## Optional Data

- free text comment.

## Validation Rules

- Feedback must belong to one completed activity.
- Perceived effort must be between 1 and 10.
- Perceived sensations must be one of:
  - very weak;
  - weak;
  - normal;
  - strong;
  - very strong.

## Output

- A new Athlete Activity Feedback entry is created.

## Related Domain Concepts

- Completed Activity
- Athlete Activity Feedback

---

# UC-010 - Generate Activity Report

## Goal

Generate an AI-assisted report for a completed activity.

## Primary Actor

Athlete.

## Preconditions

- A Completed Activity exists.
- An Activity File has been processed successfully.
- Athlete Activity Feedback exists.
- A linked Planned Session may exist, but is not mandatory.

## Main Flow

1. The system detects that a completed activity has been added with its Garmin file and subjective feedback.
2. The system gathers the completed activity data.
3. The system gathers activity laps when available.
4. The system gathers the linked planned session if available.
5. The system gathers relevant performance metrics and training zones.
6. The system gathers activity subjective feedback.
7. The system generates an activity report.
8. The system stores the full generated text.
9. The system stores a minimal structured summary.
10. The system stores the report version.
11. The athlete reviews the report.

## Report Content

The activity report should include:

- summary of the activity;
- comparison with the planned session, if applicable;
- intensity analysis;
- relevant observations;
- impact on the current week;
- risks or warning signs, if any;
- short recommendation for the next training decision.

## Alternative Flows

### No Linked Planned Session

1. The completed activity is not linked to a planned session.
2. The system generates the report without planned vs completed comparison.
3. The system still includes the activity in weekly context and recommendations.

### Missing Activity Feedback

1. The completed activity exists but subjective feedback has not been entered.
2. The system should request subjective feedback before generating the activity report.

### Poor Subjective Feedback or Pain

1. The athlete feedback indicates pain, abnormal fatigue, or unusually poor sensations.
2. The system treats this as a warning sign.
3. The system avoids aggressive recommendations.
4. The system may recommend reducing, replacing, or skipping intensity.
5. The system may advise professional medical support if symptoms suggest a possible health issue.

## Validation Rules

- Activity report must belong to one completed activity.
- Activity report must preserve full generated text.
- Activity report must include a minimal structured summary.
- Report versions must be preserved over time.
- The report must not provide medical diagnosis.

## Output

- A new Activity Report version is created.

## Related Domain Concepts

- Completed Activity
- Planned Session
- Activity Lap
- Athlete Activity Feedback
- Performance Metric
- Training Zone
- Activity Report

---

# UC-011 - Register Athlete Subjective Status

## Goal

Allow the athlete to register general subjective status that can influence weekly recommendations.

## Primary Actor

Athlete.

## Preconditions

- A Training Week exists.

## Main Flow

1. The athlete opens the subjective status flow.
2. The system asks for current status information.
3. The athlete enters fatigue, sleep quality, stress, motivation, soreness, pain notes, available time, and optional notes.
4. The system validates the information.
5. The system stores the subjective status entry.
6. The system makes the entry available for weekly proposals and weekly reports.

## Required Data

- training week;
- date.

## Optional Data

- fatigue;
- sleep quality;
- stress;
- motivation;
- muscle soreness;
- pain notes;
- available time;
- free text notes.

## Validation Rules

- Subjective status belongs to one training week.
- Subjective status is registered flexibly by date.
- The MVP does not require mandatory daily check-ins.
- Subjective status must actively influence recommendations when available.

## Output

- A new Athlete Subjective Status entry is created.

## Related Domain Concepts

- Training Week
- Athlete Subjective Status

---

# UC-012 - Generate Weekly Report

## Goal

Generate an AI-assisted weekly report that compares planned and completed training and recommends what to consider next.

## Primary Actor

Athlete.

## Preconditions

- A Training Week exists.
- The training week may contain planned sessions.
- The training week may contain completed activities.
- Athlete subjective status may exist.

## Main Flow

1. The athlete opens the weekly report generation flow.
2. The athlete manually requests a weekly report.
3. The system gathers the training week objective and target hours.
4. The system gathers planned sessions.
5. The system gathers completed activities.
6. The system gathers activity reports when available.
7. The system gathers athlete subjective status entries for the week.
8. The system gathers relevant performance metrics and training zones.
9. The system compares planned and completed training.
10. The system analyzes distribution by discipline.
11. The system identifies key observations, risks, and warning signs.
12. The system generates a weekly report.
13. The system stores the full generated text.
14. The system stores a minimal structured summary.
15. The system stores the report version.
16. The athlete reviews the report.

## Report Content

The weekly report should include:

- completed training summary;
- planned vs completed comparison;
- distribution by discipline;
- subjective status summary;
- key observations;
- risks or warning signs;
- recommendation for the following week.

## Alternative Flows

### No Completed Activities

1. The training week has planned sessions but no completed activities.
2. The system generates a report focused on non-compliance, missing data, or planned-only review.
3. The system recommends next steps conservatively.

### Unplanned Activities Exist

1. The week contains completed activities not linked to planned sessions.
2. The system includes them in weekly volume, discipline distribution, and recommendations.
3. The system may indicate that the activity was unplanned.

### Poor Subjective Status

1. The athlete subjective status indicates fatigue, poor sleep, high stress, pain, or low motivation.
2. The system treats this as a relevant input, not just context.
3. The system may recommend maintaining, reducing, simplifying, or adjusting the following week.

## Validation Rules

- Weekly report must belong to one training week.
- Weekly report generation is manual in the MVP.
- The MVP does not generate weekly reports automatically in the background.
- Weekly report must preserve full generated text.
- Weekly report must include a minimal structured summary.
- Report versions must be preserved over time.
- The report must not provide medical diagnosis.

## Output

- A new Weekly Report version is created.

## Related Domain Concepts

- Training Week
- Planned Session
- Completed Activity
- Activity Report
- Athlete Subjective Status
- Performance Metric
- Training Zone
- Weekly Report

---

# UC-013 - Generate Weekly Training Proposal

## Goal

Generate an AI-assisted training proposal for a training week.

## Primary Actor

Athlete.

## Preconditions

- A Training Week exists.
- The current training phase is defined.
- Target races are defined.
- Performance metrics and training zones may exist.
- Completed activities and subjective status may exist.

## Main Flow

1. The athlete opens the weekly training proposal flow.
2. The athlete requests a weekly training proposal.
3. The system gathers target races and race priorities.
4. The system gathers the current training phase.
5. The system gathers the baseline training week.
6. The system gathers existing planned sessions, if any.
7. The system gathers recent completed activities.
8. The system gathers performance metrics and training zones.
9. The system gathers athlete subjective status.
10. The system generates a weekly training proposal.
11. The system stores the full generated text.
12. The system stores a minimal structured summary.
13. The system stores the proposal version.
14. The proposal remains separate from the official planned sessions.
15. The athlete reviews the proposal.

## Proposal Content

The weekly training proposal should include:

- planned sessions for the week;
- objective of each session;
- expected intensity;
- estimated duration;
- relevant zones or target ranges;
- short reasoning behind the recommendation.

## Validation Rules

- Weekly training proposal must belong to one training week.
- Proposal must not automatically modify official planned sessions.
- Subjective athlete status must actively influence recommendations.
- The proposal must follow recommendation safety rules.
- Proposal versions must be preserved over time.

## Output

- A new Weekly Training Proposal version is created with status `draft`.

## Related Domain Concepts

- Race
- Training Phase
- Training Week
- Planned Session
- Completed Activity
- Performance Metric
- Training Zone
- Athlete Subjective Status
- Weekly Training Proposal

---

# UC-014 - Accept Weekly Training Proposal

## Goal

Allow the athlete to accept an AI-generated weekly training proposal and convert it into official planned sessions.

## Primary Actor

Athlete.

## Preconditions

- A Weekly Training Proposal exists.
- The proposal status is `draft`.

## Main Flow

1. The athlete reviews the weekly training proposal.
2. The athlete accepts the proposal.
3. The system changes the proposal status to `accepted`.
4. The system creates or updates planned sessions based on the accepted proposal.
5. The system marks the created or updated planned sessions as official for the training week.

## Validation Rules

- Only draft proposals can be accepted.
- A weekly proposal must be explicitly accepted before it creates or updates planned sessions.
- For the MVP, the proposal is accepted as a whole.
- Accepting individual sessions may be added later.

## Output

- Weekly Training Proposal status changes to `accepted`.
- Planned Sessions are created or updated.

## Related Domain Concepts

- Weekly Training Proposal
- Training Week
- Planned Session

---

# UC-015 - Reject Weekly Training Proposal

## Goal

Allow the athlete to reject an AI-generated weekly training proposal without modifying official planned sessions.

## Primary Actor

Athlete.

## Preconditions

- A Weekly Training Proposal exists.
- The proposal status is `draft`.

## Main Flow

1. The athlete reviews the weekly training proposal.
2. The athlete rejects the proposal.
3. The system changes the proposal status to `rejected`.
4. The system does not create or update planned sessions.

## Validation Rules

- Only draft proposals can be rejected.
- Rejected proposals must not modify official planned sessions.
- Rejected proposal versions should remain stored for historical context.

## Output

- Weekly Training Proposal status changes to `rejected`.
- Official planned sessions remain unchanged.

## Related Domain Concepts

- Weekly Training Proposal
- Training Week
- Planned Session

---

# UC-016 - Regenerate Activity Report

## Goal

Allow the athlete to regenerate an activity report when relevant input data changes.

## Primary Actor

Athlete.

## Preconditions

- A Completed Activity exists.
- At least one Activity Report may already exist.
- Relevant input data has changed or the athlete wants a new analysis.

## Main Flow

1. The athlete opens the completed activity detail.
2. The athlete requests report regeneration.
3. The system gathers the latest completed activity data.
4. The system gathers the latest activity feedback.
5. The system gathers the latest planned session matching, if available.
6. The system gathers relevant performance metrics and training zones.
7. The system generates a new activity report.
8. The system stores the full generated text.
9. The system stores a minimal structured summary.
10. The system stores the new report version.
11. The athlete reviews the new report.

## Alternative Flows

### No Relevant Changes

1. The athlete requests regeneration without changing inputs.
2. The system may still generate a new version.
3. The system preserves the previous report version.

## Validation Rules

- Regenerated reports must not overwrite previous report versions.
- The new report must become a new version.
- The report must not provide medical diagnosis.

## Output

- A new Activity Report version is created.

## Related Domain Concepts

- Completed Activity
- Planned Session
- Athlete Activity Feedback
- Performance Metric
- Training Zone
- Activity Report

---

# Recommendation Safety Rules

All AI-assisted use cases must follow these rules:

- Do not provide medical diagnosis.
- Treat pain, illness, abnormal fatigue, or unusually poor recovery as warning signs.
- Recommend reducing, replacing, or skipping intensity when subjective status is poor.
- Prioritize consistency, health, and long-term progression over aggressive load increases.
- Avoid large sudden increases in training load.
- Keep the athlete in control of final training decisions.
- Advise professional medical support when symptoms suggest a possible health issue.

---

# Notes

These use cases define functional behavior for the MVP.

They do not define:

- technical architecture;
- database schema;
- API contracts;
- frontend screen design;
- AI prompt design;
- infrastructure;
- deployment strategy.