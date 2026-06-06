# Domain Model

## Purpose

This document defines the initial domain model for the Adaptive Triathlon Coach MVP.

The goal is to identify the main business concepts, their responsibilities, and their relationships before defining detailed use cases, database models, or technical architecture.

The MVP is centered around one main idea:

> Adapt a baseline triathlon training plan based on planned sessions, completed activities, athlete feedback, performance metrics, subjective status, and current context.

---

# Core Domain Concepts

## Athlete

The athlete is the user of the system.

In the MVP, the system supports only one athlete. However, Athlete is explicitly modeled as an internal domain entity because most other entities belong to the athlete.

The MVP does not require athlete management screens in the UI.

### Responsibilities

- Own target races.
- Own the baseline training plan.
- Register performance metrics.
- Define training zones.
- Upload completed activities.
- Provide subjective activity feedback.
- Provide subjective status.
- Review AI-generated recommendations and reports.

### Key Attributes

- id
- name
- birth year or age group
- optional notes

---

## Race

A race represents a target event for the athlete.

Races guide the training plan and influence the importance of each training phase, weekly proposal, and recommendation.

### Responsibilities

- Define the athlete's target events.
- Classify race priority.
- Provide context for training recommendations.

### Key Attributes

- id
- athlete id
- name
- date
- distance
- priority: A, B, or C
- location
- notes

### Examples

- IRONMAN 70.3 Málaga 2026
- Olympic triathlon
- Sprint triathlon
- Marathon

---

## Race Priority

Race priority defines how important a race is within the season.

### Values

- A: Main target race.
- B: Secondary race used as preparation or performance checkpoint.
- C: Low-priority race, usually social, training-based, or activation-focused.

### Responsibilities

- Help the system understand how much training should be adapted around the race.
- Help decide tapering, recovery, and risk tolerance.

---

## Training Plan

A training plan represents the baseline structure used to guide training.

The MVP does not generate a complete training plan from scratch. Instead, it stores and adapts an existing baseline plan.

The baseline training plan is entered manually through forms. Markdown import is not part of the first MVP version.

### Responsibilities

- Group the training phases.
- Provide the overall structure of the preparation.
- Serve as the reference for weekly proposals and reports.

### Key Attributes

- id
- athlete id
- name
- start date
- end date
- main race id
- notes

### Relationships

- A training plan belongs to one athlete.
- A training plan has many training phases.
- A training plan is usually linked to one main A race.

---

## Training Phase

A training phase represents a period within the training plan.

Examples: Prep, Base, Build, Peak, Taper.

### Responsibilities

- Define the objective of a specific period.
- Group training weeks.
- Provide context for weekly recommendations.

### Key Attributes

- id
- training plan id
- name
- start date
- end date
- objective
- notes

### Examples

- Prep
- Base
- Build
- Peak
- Taper

### Relationships

- A training phase belongs to one training plan.
- A training phase has many training weeks.

---

## Training Week

A training week is the basic planning unit of the MVP.

Each week belongs to a training phase and contains weekly objectives, target hours, planned sessions, completed activities, subjective status entries, weekly proposals, and weekly reports.

### Responsibilities

- Define the weekly objective.
- Define target training volume.
- Group planned sessions.
- Group completed activities.
- Provide the main context for weekly recommendations.
- Act as the main unit for planned vs completed comparison.

### Key Attributes

- id
- training phase id
- week number
- start date
- end date
- objective
- target training hours
- notes

### Relationships

- A training week belongs to one training phase.
- A training week has many planned sessions.
- A training week has many completed activities.
- A training week may have many athlete subjective status entries.
- A training week may have many weekly training proposals.
- A training week may have many weekly reports.

---

## Planned Session

A planned session represents a workout that is expected to be completed by the athlete.

It is part of a training week and provides the reference against which completed activities may be compared.

A planned session is different from a completed activity.

### Responsibilities

- Define what the athlete is expected to train.
- Provide intended duration, intensity, and objective.
- Reference target training zones or ranges when applicable.
- Serve as reference for activity comparison.
- Track whether the planned session was completed, modified, skipped, moved, replaced, or cancelled.

### Key Attributes

- id
- training week id
- discipline
- session type
- planned date
- duration
- intensity
- objective
- target zones
- description
- status
- notes

### Status Values

- planned
- completed
- partially completed
- skipped
- replaced
- moved
- cancelled

### Disciplines

- swim
- bike
- run
- strength
- mobility
- yoga
- rest
- other

### Session Types

Examples:

- endurance
- recovery
- technique
- intervals
- tempo
- long session
- brick
- strength
- mobility
- race
- rest

### Relationships

- A planned session belongs to one training week.
- A planned session may be linked to zero, one, or many completed activities.
- A planned session may reference one or more training zones.

### Notes

A planned session may be linked to more than one completed activity when needed, for example in brick sessions or split workouts.

---

## Completed Activity

A completed activity represents an actual workout performed by the athlete.

It may come from a Garmin file and may include subjective feedback provided manually by the athlete.

A completed activity is different from a planned session.

### Responsibilities

- Store what the athlete actually did.
- Provide objective activity data.
- Provide the basis for activity analysis.
- Support comparison with a planned session when applicable.
- Influence future recommendations.

### Key Attributes

- id
- training week id
- planned session id, optional
- discipline
- activity date
- duration
- distance
- average pace or speed
- average heart rate
- maximum heart rate
- average power
- normalized power, optional
- cadence
- elevation gain
- source
- notes

### Relationships

- A completed activity belongs to one training week.
- A completed activity may be linked to one planned session.
- A completed activity may have one uploaded activity file.
- A completed activity may have many activity laps.
- A completed activity may have one athlete activity feedback entry.
- A completed activity may have one or more activity report versions.

### Notes

A completed activity may exist without being linked to any planned session.

Unplanned activities are included in weekly volume, discipline distribution, reports, and recommendations.

For the MVP, one completed activity should be linked to at most one planned session.

The system may suggest a possible match between a completed activity and a planned session, but the user remains responsible for confirming the link.

---

## Activity File

An activity file represents the original uploaded file used to import objective training data.

For the MVP, TCX files are prioritized first. ZIP files are supported as containers when they include TCX or FIT files. FIT files may be supported later.

### Responsibilities

- Store metadata about the uploaded file.
- Keep traceability between imported data and original source.
- Allow reprocessing if needed.

### Key Attributes

- id
- completed activity id
- file name
- file format
- upload date
- processing status
- processing error, optional

### File Formats

- TCX
- ZIP
- FIT

### Processing Status

- pending
- processed
- failed

### Relationships

- An activity file belongs to one completed activity.

---

## Activity Lap

An activity lap represents a segment, lap, or interval extracted from the activity file.

This is especially useful for swimming sets, running intervals, bike segments, and structured workouts.

Activity laps are stored as structured data when they are available in the uploaded activity file.

### Responsibilities

- Store interval-level activity data.
- Help analyze pacing, intensity, and execution.
- Support more detailed activity reports.

### Key Attributes

- id
- completed activity id
- lap number
- duration
- distance
- average pace or speed
- average heart rate
- maximum heart rate
- average power
- cadence
- elevation gain
- notes

### Relationships

- An activity lap belongs to one completed activity.

---

## Activity Data Point

An activity data point represents detailed time-series data extracted from an activity file.

This may include heart rate, pace, power, cadence, altitude, or GPS data.

For the MVP, full activity time-series data points will not be persisted by default.

The system may parse detailed data temporarily during activity processing, but the first persisted version focuses on activity summary data and laps or intervals when available.

### Possible Future Attributes

- id
- completed activity id
- timestamp
- distance
- heart rate
- power
- pace or speed
- cadence
- altitude
- latitude
- longitude

### MVP Status

Activity Data Point is a future capability, not a persisted MVP entity by default.

---

## Athlete Activity Feedback

Athlete activity feedback represents the athlete's subjective evaluation after a completed activity.

This is different from objective Garmin data and different from general athlete subjective status.

### Responsibilities

- Capture perceived effort.
- Capture subjective sensations.
- Capture free text observations.
- Add context to the activity report and future recommendations.

### Key Attributes

- id
- completed activity id
- perceived effort
- perceived sensations
- comment
- created at

### Perceived Effort

Scale from 1 to 10.

### Perceived Sensations

- very weak
- weak
- normal
- strong
- very strong

### Relationships

- Athlete activity feedback belongs to one completed activity.

---

## Athlete Subjective Status

Athlete subjective status represents the athlete's general current state.

Unlike activity feedback, this is not tied to a single completed workout. It provides context when generating or adjusting a weekly proposal and when generating weekly reports.

Subjective status is registered flexibly by date. The MVP does not require mandatory daily check-ins.

### Responsibilities

- Capture current fatigue.
- Capture sleep quality.
- Capture stress.
- Capture motivation.
- Capture soreness or pain.
- Capture available time.
- Provide context for recommendations.
- Actively influence training adaptation.

### Key Attributes

- id
- training week id
- date
- fatigue
- sleep quality
- stress
- motivation
- muscle soreness
- pain notes
- available time
- free text notes

### Relationships

- Athlete subjective status usually belongs to one training week.
- A training week may have multiple subjective status entries.

### Notes

Subjective status is not only displayed as context. It must actively influence whether the system recommends maintaining, reducing, simplifying, or adjusting training.

---

## Performance Metric

A performance metric represents a tested or estimated value used to define training intensity.

Examples include swimming CSS, cycling FTP, or running threshold pace.

### Responsibilities

- Store current performance references.
- Support training intensity prescription.
- Provide context for activity analysis.

### Key Attributes

- id
- athlete id
- discipline
- metric type
- value
- unit
- test date
- estimation method
- notes

### Metric Types

Examples:

- swimming CSS
- cycling FTP
- running threshold pace
- running threshold heart rate
- maximum heart rate
- pace zone reference
- power zone reference

### Relationships

- A performance metric belongs to one athlete.
- A performance metric may define one or more training zones.

---

## Training Zone

A training zone defines a structured range of intensity for a specific discipline.

Training zones are used in planned sessions, activity analysis, and recommendations.

Training zones should be stored as structured ranges whenever possible. Free text notes may complement structured ranges, but they should not replace them.

### Responsibilities

- Translate performance metrics into usable intensity ranges.
- Help prescribe workouts.
- Help analyze completed activities.

### Key Attributes

- id
- performance metric id
- discipline
- zone name
- lower bound
- upper bound
- unit
- description
- notes

### Examples

Swimming pace zones:

- easy / technical
- aerobic comfortable
- controlled
- strong intervals

Cycling power zones:

- Z1 recovery
- Z2 endurance
- Z3 tempo
- Z4 threshold
- Z5 VO2

Running zones:

- easy
- steady
- tempo
- threshold
- interval

### Relationships

- A training zone belongs to one performance metric.
- A planned session may reference one or more training zones.
- A completed activity may be analyzed against training zones.

---

## Weekly Training Proposal

A weekly training proposal is an AI-generated recommendation for a training week.

It is based on the baseline plan, target races, current phase, planned sessions, completed activities, performance metrics, training zones, and subjective status.

The proposal remains separate from the official planned sessions until the user accepts it.

### Responsibilities

- Propose planned sessions for a week.
- Explain the reasoning behind the proposal.
- Adapt the baseline plan to the athlete's current context.
- Preserve the user as the final decision-maker.

### Key Attributes

- id
- training week id
- generated at
- proposal summary
- full generated text
- structured summary
- recommendation status
- reasoning
- notes
- version

### Recommendation Status

- draft
- accepted
- modified
- rejected

### Relationships

- A weekly training proposal belongs to one training week.
- A weekly training proposal may create or update planned sessions only after user acceptance.
- A training week may have multiple weekly training proposal versions over time.

### Notes

For the MVP, the user accepts or rejects a weekly training proposal as a whole. Accepting individual sessions may be added later.

---

## Activity Report

An activity report is an AI-generated analysis of a completed activity.

It is generated automatically after importing an activity file and entering subjective activity feedback.

The user may manually regenerate an activity report if relevant input data changes, such as subjective feedback or activity-session matching.

### Responsibilities

- Summarize the completed activity.
- Compare the activity with the planned session if available.
- Analyze intensity and execution.
- Identify relevant observations.
- Describe impact on the current week.
- Recommend the next training decision.

### Key Attributes

- id
- completed activity id
- generated at
- full generated text
- structured summary
- summary
- planned vs completed analysis
- intensity analysis
- observations
- impact on current week
- risks
- recommendation
- version

### Relationships

- An activity report belongs to one completed activity.
- A completed activity may have multiple activity report versions over time.

---

## Weekly Report

A weekly report is an AI-generated analysis of a training week.

It summarizes what was planned, what was completed, how the athlete felt, and what should be considered next.

Weekly reports are generated manually by the user.

### Responsibilities

- Summarize completed training.
- Compare planned vs completed training.
- Analyze distribution by discipline.
- Include subjective status.
- Identify risks or warning signs.
- Recommend adjustments for the following week.

### Key Attributes

- id
- training week id
- generated at
- full generated text
- structured summary
- completed summary
- planned vs completed comparison
- discipline distribution
- subjective status summary
- key observations
- risks
- recommendation
- version

### Relationships

- A weekly report belongs to one training week.
- A training week may have multiple weekly report versions over time.

---

# Supporting Concepts

## Discipline

A discipline represents the type of training or activity.

### Values

- swim
- bike
- run
- strength
- mobility
- yoga
- rest
- other

---

## Intensity

Intensity represents the expected or observed effort level of a session.

In the MVP, intensity can be expressed in a simple way and connected to specific training zones when available.

### Possible Values

- recovery
- easy
- moderate
- controlled
- hard
- very hard

---

## Recommendation

A recommendation is an AI-generated suggestion that helps the athlete make a training decision.

Recommendations may appear inside:

- weekly training proposals;
- activity reports;
- weekly reports.

For the MVP, recommendations are stored as part of the generated reports rather than as a separate standalone entity.

---

# Main Relationships Summary

## Training Structure

- One athlete has one or more races.
- One athlete has one training plan for the MVP.
- One training plan has many training phases.
- One training phase has many training weeks.
- One training week has many planned sessions.

## Activity Structure

- One training week has many completed activities.
- One completed activity may be linked to one planned session.
- One planned session may be linked to zero, one, or many completed activities.
- One completed activity may have one activity file.
- One completed activity may have many activity laps.
- One completed activity has one athlete activity feedback entry.
- One completed activity may have many activity report versions.
- Activity data points are not persisted by default in the MVP.

## Context and Recommendation Structure

- One training week may have many athlete subjective status entries.
- One training week may have many weekly training proposal versions.
- One training week may have many weekly report versions.
- Performance metrics define training zones.
- Planned sessions may reference training zones.
- Completed activities may be analyzed against training zones.

---

# Important Domain Decisions

## Training Week as the Basic Planning Unit

The training week is the basic unit of planning and adaptation.

This means that the system mainly adapts training week by week, rather than generating or modifying a full season plan automatically.

---

## Planned Session vs Completed Activity

A planned session and a completed activity are different concepts.

A planned session represents what was expected.

A completed activity represents what actually happened.

They may be linked, but the relationship is optional because:

- the athlete may complete an unplanned activity;
- the athlete may skip a planned session;
- one planned session may result in more than one completed activity;
- one completed activity may partially match a planned session.

For the MVP:

- one planned session may be linked to multiple completed activities;
- one completed activity should be linked to at most one planned session.

---

## Activity Feedback vs Subjective Status

The MVP separates two types of subjective information.

### Activity Feedback

Activity feedback is linked to a completed activity.

It answers:

> How did this specific workout feel?

### Athlete Subjective Status

Athlete subjective status is linked to a week or date.

It answers:

> How am I feeling now, and how should that affect the next training decision?

---

## AI Reports Are Stored and Versioned

AI-generated outputs are stored as reports.

This includes:

- weekly training proposals;
- activity reports;
- weekly reports.

Reports store both:

- the full generated text;
- a minimal structured summary.

Generated report versions are preserved over time.

This allows the athlete to review historical recommendations and preserves the reasoning available at the time of generation.

---

## Activity File Traceability

The uploaded Garmin file should remain traceable.

Even if the system extracts summary data, the original uploaded file metadata should be preserved so the activity can be reviewed or reprocessed later.

---

## Recommendation Safety

AI recommendations must follow basic safety rules:

- do not provide medical diagnosis;
- treat pain, illness, abnormal fatigue, or unusually poor recovery as warning signs;
- recommend reducing, replacing, or skipping intensity when subjective status is poor;
- prioritize consistency, health, and long-term progression over aggressive load increases;
- avoid large sudden increases in training load;
- keep the athlete in control of final training decisions;
- advise professional medical support when symptoms suggest a possible health issue.

---

# Initial Aggregate Candidates

This section identifies possible domain aggregates for future backend design.

## Training Plan Aggregate

Possible root:

- Training Plan

Contains:

- Training Phases
- Training Weeks
- Planned Sessions

## Completed Activity Aggregate

Possible root:

- Completed Activity

Contains:

- Activity File
- Activity Laps
- Athlete Activity Feedback
- Activity Report versions

Activity Data Points are not included in the persisted MVP aggregate by default.

## Performance Metric Aggregate

Possible root:

- Performance Metric

Contains:

- Training Zones

## Weekly Analysis Aggregate

Possible root:

- Training Week

Contains or references:

- Weekly Training Proposal versions
- Weekly Report versions
- Athlete Subjective Status

These aggregates are provisional and should be refined during technical design.