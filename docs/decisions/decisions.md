# MVP Decisions

## DEC-001 - Baseline Training Plan Input

The baseline training plan will be entered manually through a form.

The basic planning unit will be the training week. Each training week must belong to a training phase and include:

- training phase;
- week objective;
- target training hours.

Planned sessions may be defined as part of the weekly planning structure.

## DEC-002 - Garmin File Import Priority

Pending decision.

The MVP has not yet defined which Garmin file format should be prioritized first.

Possible formats:

- FIT;
- TCX;
- ZIP.

ZIP files may be supported as containers if they include FIT or TCX activity files.

## DEC-003 - Activity Subjective Feedback

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

## DEC-004 - Activity Report Generation

The activity report will be generated automatically when the user adds a completed workout together with its Garmin file.

Once generated, the report will be stored and can be consulted later at any time.

## DEC-005 - Weekly Training Proposal Detail

The weekly training proposal will include, at minimum:

- planned sessions;
- session duration;
- session intensity;
- session objective;
- short reasoning behind the recommendation.

The level of detail may be expanded later when defining the use cases.

## DEC-006 - Planned Sessions and Completed Activities Data Model

Pending decision.

The detailed data model for planned sessions and completed activities will be defined later in the domain model document.

## DEC-007 - AI Report Persistence

Generated AI reports will be stored.

This includes:

- activity reports;
- weekly reports;
- weekly training proposals.

Storing generated reports will preserve historical context and allow the user to review previous recommendations and analyses.