# UC-002: Manage Training Program

## 1. Use Case Summary

Create and manage a Training Program as the high-level weekly structure of an athlete's preparation.

A Training Program is composed of a fixed list of Training Weeks. Each week defines its dates, period classification, weekly goal and target training hours.

This use case does not generate daily training sessions. It only defines the program structure at weekly level.

## 2. Goal

Allow the user to create, review, edit, change status and delete a Training Program.

The program must provide a complete weekly planning framework that can later be used by other use cases to generate or manage detailed weekly training plans.

## 3. Scope

### In Scope

- List Training Programs.
- Create a new Training Program.
- Generate Training Weeks from a first Monday and a number of weeks.
- Complete all generated Training Weeks before saving the program.
- View Training Program detail.
- Edit an active Training Program.
- Change Training Program status.
- Delete a Training Program.

### Out of Scope

- Creating planned training sessions.
- Generating daily workouts.
- Distributing training by sport.
- Managing athlete availability.
- Managing fatigue, sleep, stress or readiness inputs.
- Associating Training Programs with Target Races.
- Adding or removing weeks after the program has been created.
- Editing individual week dates.
- Creating or managing a standalone Training Period entity.

## 4. Primary Actor

- Athlete user.

In the MVP, the athlete user is also considered the user managing their own training program.

## 5. Preconditions

- The user is authenticated.
- The user has access to the Training Programs area.

## 6. Main Concepts

### Training Program

A Training Program is the high-level structure of a training plan.

It contains:

- Name.
- Description / notes.
- Status.
- A list of Training Weeks.

The program start date and end date are derived from its weeks:

- Program start date = start date of the first Training Week.
- Program end date = end date of the last Training Week.

### Training Week

A Training Week represents one week within a Training Program.

It contains:

- Week number.
- Start date.
- End date.
- Period.
- Weekly goal.
- Target hours.

Training Weeks are always generated from Monday to Sunday.

### Period

There is no standalone Training Period entity in the MVP.

The period is a classification field inside each Training Week.

Initial allowed values:

- Prep.
- Base.
- Build.
- Peak.
- Taper.
- Race Week.
- Recovery.
- Transition.

## 7. Statuses

A Training Program can have one of the following statuses:

- Active.
- Completed.
- Suspended.

### Status Rules

- A newly created Training Program is created as Active.
- A user can only have one Active Training Program at a time.
- If the user already has an Active Training Program, the system must not allow creating another one.
- To create a new Training Program, the current Active Training Program must first be completed, suspended or deleted.

### Allowed Status Transitions

| From      | To        | Allowed | Notes                                                          |
| --------- | --------- | ------: | -------------------------------------------------------------- |
| Active    | Completed |     Yes | The program is finished and becomes read-only.                 |
| Active    | Suspended |     Yes | The program is paused and becomes read-only.                   |
| Suspended | Active    |     Yes | Allowed only if the user has no other Active Training Program. |
| Completed | Active    |      No | Reactivating completed programs is not supported in the MVP.   |
| Completed | Suspended |      No | Not supported in the MVP.                                      |
| Suspended | Completed |      No | Not supported in the MVP.                                      |

## 8. Data Fields

### Training Program Fields

| Field               |         Required |                    Editable | Description                                               |
| ------------------- | ---------------: | --------------------------: | --------------------------------------------------------- |
| Name                |              Yes |       Yes, only when Active | Name of the training program.                             |
| Description / notes |               No |       Yes, only when Active | Free-text description or general notes about the program. |
| Status              |              Yes | Through allowed transitions | Active, Completed or Suspended.                           |
| Start date          |          Derived |                          No | Start date of the first Training Week.                    |
| End date            |          Derived |                          No | End date of the last Training Week.                       |
| Number of weeks     | Yes, at creation |           No after creation | Total number of weeks generated for the program.          |

### Training Week Fields

| Field        |  Required |                         Editable | Description                                                 |
| ------------ | --------: | -------------------------------: | ----------------------------------------------------------- |
| Week number  | Generated |                               No | Global week number inside the program.                      |
| Start date   | Generated |                               No | Monday of the week.                                         |
| End date     | Generated |                               No | Sunday of the week.                                         |
| Period       |       Yes | Yes, only when program is Active | Period classification of the week.                          |
| Weekly goal  |       Yes | Yes, only when program is Active | Free-text goal for the week.                                |
| Target hours |       Yes | Yes, only when program is Active | Positive integer representing target weekly training hours. |

## 9. Main Flow — Create Training Program

1. The user opens the Training Programs area.
2. The system shows the list of existing Training Programs.
3. The user chooses to create a new Training Program.
4. The system checks whether the user already has an Active Training Program.
5. If no Active Training Program exists, the system displays the creation form.
6. The user enters:
   - Program name.
   - Optional description / notes.
   - First week start date.
   - Number of weeks.
7. The system validates that the first week start date is a Monday.
8. The system validates that the number of weeks is greater than zero.
9. The user generates the Training Weeks.
10. The system creates a table of weeks with:
    - Week number.
    - Start date.
    - End date.
11. The user completes every generated Training Week with:
    - Period.
    - Weekly goal.
    - Target hours.
12. The system validates that all Training Weeks are complete.
13. The user saves the Training Program.
14. The system creates the Training Program with status Active.
15. The system stores all generated Training Weeks.
16. The system shows the Training Program detail or confirms that the program has been created successfully.

## 10. Alternative Flows

### AF-001 — User already has an Active Training Program

1. The user tries to create a new Training Program.
2. The system detects that the user already has an Active Training Program.
3. The system does not allow creating a new Training Program.
4. The system informs the user that they must first complete, suspend or delete the current Active Training Program.

### AF-002 — First week start date is not Monday

1. The user enters a first week start date that is not a Monday.
2. The system shows a validation error.
3. The system does not generate the Training Weeks until the date is corrected.

### AF-003 — Number of weeks is invalid

1. The user enters an invalid number of weeks.
2. The system shows a validation error.
3. The system does not generate the Training Weeks until the value is corrected.

Invalid values include:

- Empty value.
- Zero.
- Negative values.
- Decimal values.

### AF-004 — Generated weeks are incomplete

1. The user generates the Training Weeks.
2. The user tries to save the Training Program without completing all week fields.
3. The system shows validation errors.
4. The system does not save the Training Program until every week has:
   - Period.
   - Weekly goal.
   - Target hours.

### AF-005 — Target hours is invalid

1. The user enters an invalid target hours value for a Training Week.
2. The system shows a validation error.
3. The system does not allow saving until the value is corrected.

Invalid values include:

- Empty value.
- Zero.
- Negative values.
- Decimal values.

Valid values are positive integers, for example:

- 6.
- 8.
- 10.
- 12.

## 11. View Training Program Detail

The user can open the detail of a Training Program from the list.

The detail screen shows:

- Program name.
- Description / notes.
- Derived start date.
- Derived end date.
- Total number of weeks.
- Status.
- Training Weeks table.

The Training Weeks table shows:

| Field        |
| ------------ |
| Week number  |
| Start date   |
| End date     |
| Period       |
| Weekly goal  |
| Target hours |

Available actions depend on the Training Program status.

## 12. Edit Training Program

Only Active Training Programs can be edited.

The user can edit:

- Program name.
- Description / notes.
- Week period.
- Week weekly goal.
- Week target hours.

The user cannot edit:

- Program start date.
- Program end date.
- Number of weeks.
- Week number.
- Week start date.
- Week end date.

Adding or removing weeks after creation is not supported in the MVP.

## 13. Change Training Program Status

### Complete Active Program

1. The user opens an Active Training Program.
2. The user chooses to mark it as Completed.
3. The system asks for confirmation.
4. The user confirms.
5. The system changes the status to Completed.
6. The program becomes read-only.

### Suspend Active Program

1. The user opens an Active Training Program.
2. The user chooses to suspend it.
3. The system asks for confirmation.
4. The user confirms.
5. The system changes the status to Suspended.
6. The program becomes read-only.

### Reactivate Suspended Program

1. The user opens a Suspended Training Program.
2. The user chooses to reactivate it.
3. The system checks whether the user already has another Active Training Program.
4. If no Active Training Program exists, the system changes the status to Active.
5. If another Active Training Program exists, the system does not reactivate the suspended program and informs the user.

## 14. Delete Training Program

A Training Program can be deleted in any status:

- Active.
- Suspended.
- Completed.

Deletion rules:

- The system must ask for confirmation before deleting.
- Deleting a Training Program also deletes all its Training Weeks.
- Target Races are not affected because UC-002 does not manage any relationship between Training Programs and Target Races.

## 15. List Training Programs

The Training Programs list shows:

| Field      | Description                           |
| ---------- | ------------------------------------- |
| Name       | Program name.                         |
| Start date | Derived from the first Training Week. |
| End date   | Derived from the last Training Week.  |
| Weeks      | Total number of Training Weeks.       |
| Status     | Active, Suspended or Completed.       |

Default ordering:

1. Active programs first.
2. Suspended programs second.
3. Completed programs last.

Within each status group, programs are ordered by descending start date.

The user cannot change the ordering in the MVP.

## 16. Business Rules

- BR-001: A Training Program is composed of Training Weeks.
- BR-002: There is no standalone Training Period entity in the MVP.
- BR-003: The period is a field of each Training Week.
- BR-004: A Training Program start date is derived from the first Training Week.
- BR-005: A Training Program end date is derived from the last Training Week.
- BR-006: Training Weeks are always generated from Monday to Sunday.
- BR-007: The first week start date must be a Monday.
- BR-008: The number of weeks must be a positive integer.
- BR-009: Week dates are generated by the system and cannot be manually edited.
- BR-010: Every generated Training Week must be completed before saving the Training Program.
- BR-011: Every Training Week must have a period.
- BR-012: Every Training Week must have a weekly goal.
- BR-013: Every Training Week must have target hours.
- BR-014: Target hours must be a positive integer.
- BR-015: Decimal target hours are not allowed.
- BR-016: A newly created Training Program is created as Active.
- BR-017: A user can only have one Active Training Program at a time.
- BR-018: If the user already has an Active Training Program, they cannot create another one.
- BR-019: Only Active Training Programs can be edited.
- BR-020: Suspended Training Programs are read-only, except for reactivation.
- BR-021: Completed Training Programs are read-only and cannot be reactivated in the MVP.
- BR-022: The number of weeks cannot be changed after creation.
- BR-023: Weeks cannot be added or removed after creation in the MVP.
- BR-024: A Training Program can be deleted in any status.
- BR-025: Deleting a Training Program deletes its Training Weeks.
- BR-026: UC-002 does not create planned training sessions.
- BR-027: UC-002 does not associate Training Programs with Target Races.

## 17. Acceptance Criteria

### AC-001 — Create Training Program successfully

Given the user has no Active Training Program  
When the user creates a Training Program with valid data and completes all generated Training Weeks  
Then the system creates the Training Program  
And the Training Program status is Active  
And the Training Weeks are stored with their generated dates and completed planning fields.

### AC-002 — Prevent creating a second Active Training Program

Given the user already has an Active Training Program  
When the user tries to create another Training Program  
Then the system prevents the creation  
And informs the user that they must complete, suspend or delete the current Active Training Program first.

### AC-003 — Generate weeks from Monday start date

Given the user enters a valid Monday as the first week start date  
And enters a valid number of weeks  
When the user generates the weeks  
Then the system creates consecutive weeks from Monday to Sunday  
And assigns a global week number to each week.

### AC-004 — Reject non-Monday start date

Given the user enters a first week start date that is not Monday  
When the user tries to generate the weeks  
Then the system shows a validation error  
And does not generate the weeks.

### AC-005 — Require all weekly fields before saving

Given the system has generated the Training Weeks  
When the user tries to save the Training Program with incomplete weeks  
Then the system shows validation errors  
And does not save the Training Program.

### AC-006 — Reject invalid target hours

Given the user is completing a Training Week  
When the user enters empty, zero, negative or decimal target hours  
Then the system shows a validation error  
And does not allow saving until the value is corrected.

### AC-007 — Edit Active Training Program

Given the Training Program is Active  
When the user edits the program name, description or weekly planning fields  
Then the system saves the changes.

### AC-008 — Prevent editing Suspended Training Program

Given the Training Program is Suspended  
When the user opens the program detail  
Then the program is displayed as read-only  
And the user cannot edit weekly planning fields.

### AC-009 — Prevent editing Completed Training Program

Given the Training Program is Completed  
When the user opens the program detail  
Then the program is displayed as read-only  
And the user cannot edit or reactivate it.

### AC-010 — Suspend Active Training Program

Given the Training Program is Active  
When the user suspends it and confirms the action  
Then the system changes the status to Suspended.

### AC-011 — Complete Active Training Program

Given the Training Program is Active  
When the user completes it and confirms the action  
Then the system changes the status to Completed.

### AC-012 — Reactivate Suspended Training Program

Given the Training Program is Suspended  
And the user has no other Active Training Program  
When the user reactivates it  
Then the system changes the status to Active.

### AC-013 — Prevent reactivating Suspended Training Program when another Active exists

Given the Training Program is Suspended  
And the user already has another Active Training Program  
When the user tries to reactivate the Suspended Training Program  
Then the system prevents the reactivation  
And informs the user that only one Active Training Program is allowed.

### AC-014 — Delete Training Program

Given the user opens a Training Program in any status  
When the user deletes it and confirms the action  
Then the system deletes the Training Program  
And deletes all its Training Weeks.

### AC-015 — List Training Programs

Given the user has Training Programs  
When the user opens the Training Programs list  
Then the system shows name, start date, end date, number of weeks and status  
And orders them by Active, Suspended and Completed  
And within each status group by descending start date.

## 18. Open Questions

No open questions for the MVP version of this use case.
