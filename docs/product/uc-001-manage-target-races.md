# UC-001: Manage Target Races

## Summary

The athlete manages target races in the race calendar.

A target race is a relevant race with priority A, B, or C. Target races are stored in the race calendar and may be considered later by the training planning process.

This use case covers viewing, creating, updating, and deleting target races.

## Primary Actor

- Athlete

For the MVP, the user acts as both athlete and coach.

## Trigger

The athlete wants to add, review, update, or remove a relevant race in the race calendar so it can be considered later by the training planning process.

## Preconditions

- The athlete is using the application.
- The athlete has access to the target race management option.

## Covered Actions

- View the target race list.
- Create a target race.
- Update an existing target race.
- Delete an existing target race.

## Target Race List

The athlete can view the list of target races already created in the race calendar.

The list shows the following information for each target race:

- Race name
- Race date
- Race type
- Race distance in kilometers
- Priority

Target races are shown ordered by race date in ascending order.

The athlete cannot change the ordering in the MVP.

Each target race in the list provides actions to update or delete it.

If there are no target races, the system shows an empty state and offers the athlete the option to create a new target race.

## Required Data

To create or update a target race, the following data is required:

- Race name
- Race date
- Race type
- Race distance in kilometers
- Priority

## Optional Data

- Notes

Notes is a free text field and must not exceed 500 characters.

## Race Type Catalog

The initial race type catalog for the MVP is:

- Triathlon
- Duathlon
- Aquathlon
- Running
- Trail running
- Open water swim
- Cycling
- Other

If the athlete selects `Other`, no additional custom race type is required in the MVP.

## Main Flow: View Target Races

1. The athlete opens the target race management option.
2. The system shows the target race list.
3. The system displays existing target races ordered by race date in ascending order.
4. For each target race, the system shows race name, race date, race type, race distance in kilometers, and priority.
5. For each target race, the system provides actions to update or delete it.

## Main Flow: Create Target Race

1. The athlete opens the target race creation option.
2. The system shows the target race creation form.
3. The athlete enters the race name.
4. The athlete enters the race date.
5. The athlete selects the race type.
6. The athlete enters the race distance in kilometers.
7. The athlete selects the priority.
8. Optionally, the athlete enters notes.
9. The athlete submits the form.
10. The system validates the data.
11. The system creates the target race.
12. The system confirms the creation or shows the new race in the target race list.

## Main Flow: Update Target Race

1. The athlete chooses to update an existing target race from the target race list.
2. The system shows the update form pre-filled with the current target race data.
3. The athlete updates one or more fields.
4. The athlete submits the form.
5. The system validates the data using the same validation rules used during target race creation.
6. The system updates the target race.
7. The system confirms the update or shows the updated race in the target race list.

## Main Flow: Delete Target Race

1. The athlete chooses to delete an existing target race from the target race list.
2. The system asks the athlete to confirm the deletion.
3. The athlete confirms the deletion.
4. The system deletes the target race from the race calendar.
5. The system confirms the deletion or removes the race from the target race list.

## Alternative Flows

### A1. Empty Target Race List

1. The athlete opens the target race management option.
2. There are no target races created yet.
3. The system shows an empty state.
4. The system offers the athlete the option to create a new target race.

### A2. Missing Required Data

1. The athlete submits the create or update form with one or more required fields empty.
2. The system does not create or update the target race.
3. The system shows validation feedback.
4. The athlete can correct the data and try again.

### A3. Invalid Race Distance

1. The athlete submits the create or update form with a race distance that is not greater than 0.
2. The system does not create or update the target race.
3. The system shows validation feedback.
4. The athlete can correct the data and try again.

### A4. Invalid Race Type or Priority

1. The athlete submits the create or update form with an invalid race type or priority.
2. The system does not create or update the target race.
3. The system shows validation feedback.
4. The athlete can correct the data and try again.

### A5. Duplicated Target Race

1. The athlete submits the create or update form with a race name and race date that already exist in another target race.
2. The system does not create or update the target race.
3. The system shows validation feedback.
4. The athlete can correct the data and try again.

### A6. Notes Exceed Maximum Length

1. The athlete submits the create or update form with notes longer than 500 characters.
2. The system does not create or update the target race.
3. The system shows validation feedback.
4. The athlete can shorten the notes and try again.

### A7. Delete Target Race Cancelled

1. The athlete chooses to delete an existing target race.
2. The system asks the athlete to confirm the deletion.
3. The athlete cancels the deletion.
4. The system does not delete the target race.
5. The athlete returns to the target race list.

### A8. Target Race Referenced by a Training Plan

1. The athlete chooses to update or delete a target race that is already referenced by a training plan.
2. The system warns the athlete that the target race is already referenced by a training plan.
3. If the athlete continues with the update, the system saves the change in the race calendar.
4. If the athlete continues with the deletion, the system removes the target race from the race calendar.
5. Updating or deleting a target race does not automatically modify, recalculate, or delete existing training plans, periods, weeks, sessions, or activity reports.

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
- Target races are shown ordered by race date in ascending order.
- The athlete cannot change the target race ordering in the MVP.
- All target race fields can be updated.
- When a target race is updated, the system applies the same validations used during creation.
- Before deleting a target race, the system asks the athlete to confirm the deletion.
- Updating or deleting a target race does not automatically modify, recalculate, or delete existing training plans, periods, weeks, sessions, or activity reports.

## Success Postconditions

- The target race list is available to the athlete.
- Created target races are stored in the race calendar.
- Updated target races are stored with their latest data.
- Deleted target races are removed from the race calendar.
- Existing training plans, periods, weeks, sessions, and activity reports are not automatically modified.

## Failure Postconditions

- No target race is created, updated, or deleted when validation fails or when deletion is cancelled.
- The athlete can correct the data and try again.

## Out of Scope

- Creating training periods.
- Creating a training plan.
- Assigning a target race to a training period.
- Automatically recalculating a plan after creating, updating, or deleting a target race.
- Generating weekly training proposals.
- Creating activity reports.
- Target race detail view.
- Search and filters for target races.
- User-controlled ordering of target races.
