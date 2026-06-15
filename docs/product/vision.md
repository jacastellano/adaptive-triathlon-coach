# Product Vision

## Product Name

Adaptive Triathlon Coach

## Problem

Preparing for a middle-distance or long-distance triathlon requires constant adaptation.

A training plan may look good when it is created, but real preparation changes week by week: availability, fatigue, sleep, stress, soreness, missed sessions, unexpected events, completed workouts, performance metrics, and personal priorities all affect what the athlete should do next.

Many training plans are too static. They define what should happen, but they do not help enough when reality differs from the plan.

## Target User

The main user is an amateur triathlete preparing for a target race who wants to train in a structured but flexible way.

The product is especially intended for athletes who do not simply want to complete workouts, but want to make better training decisions based on their real condition, progress, and personal context.

## Product Idea

Adaptive Triathlon Coach is an AI-powered application focused on triathlon training.

The application uses a baseline training plan, target races, training phases, weekly goals, performance metrics, training zones, completed activities, subjective feedback, and daily athlete status to generate recommendations, reports, and planning adjustments adapted to the athlete’s context.

The product does not aim to replace the athlete’s judgment. AI recommendations are proposed as decision support, and the athlete remains in control of reviewing, adjusting, and consolidating training decisions.

## Value Proposition

The application helps the athlete answer practical questions such as:

- What should I train this week?
- How should this week be adapted to my current situation?
- How does this completed activity fit into my training plan?
- Did I complete what was planned?
- Am I accumulating too much training load?
- Should upcoming training be kept, reduced, or modified?
- How should fatigue, stress, sleep, soreness, or available time affect my next training decision?
- How is the overall plan progressing so far?
- Should next week be adjusted based on recent compliance, missed sessions, or unexpected events?

The main value is not to create generic training plans, but to adapt an existing plan to the athlete’s real situation.

## MVP Focus

The MVP will focus on four main flows:

1. Define the training context: target races, training plan, phases, weeks, performance metrics, and training zones.
2. Generate, adjust, and consolidate weekly training proposals before they become official planned sessions.
3. Log completed training days by importing activities, linking them to planned sessions, adding subjective feedback, and registering daily athlete status.
4. Generate daily and weekly reports, including compliance, observations, risks, recommendations, and an overall plan progress snapshot.

Weekly AI training proposals will be generated as drafts. The athlete can review, adjust, and consolidate them before they become official planned sessions.

## Main System Inputs

- List of races classified as A, B, or C targets.
- Baseline training plan including phases, goals and weekly hours.
- Performance metrics and structured training zones by discipline.
- Garmin activity files.
- Link between completed activities and planned sessions.
- Athlete subjective status.
- Activity subjective feedback.
- Daily comments or relevant context provided by the athlete.

For the MVP, TCX files will be prioritized first. ZIP files may be supported as containers when they include TCX or FIT files. FIT support may be added later.

## Main System Outputs

- Weekly training proposal.
- Consolidated weekly plan.
- Daily training report based on all completed activities for the day, subjective feedback, athlete status, and relevant daily context.
- Weekly training report.
- Plan progress snapshot showing compliance, deviations, unexpected events, injuries, and relevant context for future planning.
- Stored history of generated reports and recommendations.

## Out of Scope for the MVP

The MVP will not initially include:

- Automatic integration with Garmin, Strava, or other platforms.
- Full training plan generation from scratch.
- Advanced training load metrics such as CTL, ATL, or TSB.
- Full activity time-series persistence by default.
- Multi-user support.
- Payments or subscriptions.
- Native mobile application.
- Automatic notifications.
- External calendar integration.
- Medical diagnosis or medical advice.