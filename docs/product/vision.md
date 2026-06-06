# Product Vision

## Product Name

Adaptive Triathlon Coach

## Problem

Preparing for a middle-distance or long-distance triathlon requires constantly adjusting training to the athlete’s real situation: target races, baseline plan, availability, performance metrics, completed workouts, fatigue, and personal context.

The problem is that many training plans are static. They may work well on paper, but they are not always easy to adapt to what actually happens week by week.

## Target User

The main user is an amateur triathlete preparing for a target race who wants to train in a structured but flexible way.

The product is especially intended for athletes who do not simply want to complete workouts, but want to make better training decisions based on their real condition, progress, and personal priorities.

## Product Idea

Adaptive Triathlon Coach is an AI-powered application focused on triathlon training.

The application uses a baseline training plan, target races, performance metrics, subjective athlete status, and real activities imported from Garmin files to generate recommendations, reports, and adjustments adapted to the athlete’s context.

The product does not aim to replace the athlete’s judgment. AI recommendations are proposed as decision support, and the athlete remains in control of accepting, modifying, or rejecting training adjustments.

## Value Proposition

The application helps the athlete answer practical questions such as:

- What should I train this week?
- How does this activity fit into my training plan?
- Am I accumulating too much training load?
- Should I keep, reduce, or modify the planned workout?
- How should I adjust the week based on what I have actually done?
- How should fatigue, stress, sleep, soreness, or available time affect my next training decision?

The main value is not to create generic training plans, but to adapt an existing plan to the athlete’s real situation.

## MVP Focus

The MVP will focus on three main capabilities:

1. Store a baseline training structure with target races, training weeks, and planned sessions.
2. Analyze completed activities from Garmin files and compare them with planned sessions.
3. Generate activity and weekly reports with summaries, compliance, observations, risks, and recommendations.

Weekly AI training proposals will also be supported, but they will remain separate from the official planned sessions until the user accepts them.

## Main System Inputs

- List of races classified as A, B, or C targets.
- Baseline training plan including phases, goals, weekly hours, availability, and planned sessions.
- Performance metrics and structured training zones by discipline.
- Garmin activity files.
- Athlete subjective status.
- Activity subjective feedback.

For the MVP, TCX files will be prioritized first. ZIP files may be supported as containers when they include TCX or FIT files. FIT support may be added later.

## Main System Outputs

- Weekly training proposal.
- Completed activity report.
- Weekly progress and recommendation report.
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