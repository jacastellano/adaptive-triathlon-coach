# UC-001: Create Target Race

## Summary

Create a target race in the race calendar.

A target race is a relevant race or event that the athlete wants to track and potentially use later in the training planning process.

For the MVP, a target race is any race in the calendar with priority A, B, or C. Multiple races can share the same priority.

## Primary Actor

Athlete.

For the MVP, the user acts as both athlete and coach.

## Trigger

The athlete wants to add a relevant race to the race calendar so it can be considered later by the training planning process.

## Preconditions

- The athlete is using the application.
- The athlete has access to the target race creation option.

## Required Data

- Race name
- Race date
- Race type
- Race distance in kilometers
- Priority

## Optional Data

- Notes

## Main Flow

1. The athlete opens the target race creation option.
2. The system shows the target race creation form.
3. The athlete enters the race name.
4. The athlete enters the race date.
5. The athlete selects the race type.
6. The athlete enters the race distance in kilometers.
7. The athlete selects the priority.
8. The athlete optionally enters notes.
9. The athlete submits the form.
10. The system validates the data.
11. The system creates the target race.
12. The system confirms the creation or shows the new race in the target race list.

## Alternative Flows

### A1. Missing Required Data

1. Some required field is empty.
2. The system does not create the target race.
3. The system shows validation feedback.
4. The athlete can correct the data and try again.

### A2. Invalid Race Distance

1. The race distance is not greater than 0.
2. The system does not create the target race.
3. The system shows validation feedback.
4. The athlete can correct the data and try again.

### A3. Invalid Race Type or Priority

1. The race type or priority is not one of the allowed values.
2. The system does not create the target race.
3. The system shows validation feedback.
4. The athlete can correct the data and try again.

### A4. Duplicated Target Race

1. A target race with the same race name and race date already exists.
2. The system does not create the target race.
3. The system shows validation feedback.
4. The athlete can correct the data and try again.

## Business Rules

- A target race must have priority A, B, or C.
- Multiple target races can share the same priority.
- Race type must be selected from the initial catalog.
- Race distance is stored as a numeric value in kilometers.
- Discipline split is not required.
- Race date is required.
- Race date can be in the past, present, or future.
- Duplicated target races are not allowed.
- Two target races are considered duplicated when they have the same race name and race date.
- Notes are optional.
- Notes must not exceed 500 characters.

## Initial Race Type Catalog

- Triathlon
- Duathlon
- Aquathlon
- Running
- Trail running
- Open water swim
- Cycling
- Other

## Success Postconditions

- The target race is stored in the race calendar.
- The target race is available for future planning use cases.

## Failure Postconditions

- No target race is created.
- The athlete can correct the data and try again.

## Out of Scope

This use case does not cover:

- Creating a training period.
- Creating a training plan.
- Assigning the target race to a training period.
- Generating training weeks.
- Updating or deleting an existing target race.
- Importing races from external calendars or race platforms.
- Calculating discipline-specific distances for multisport races.
