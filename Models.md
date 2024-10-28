# Models

These are the models I am expecting that will be used for the feedback enhancement features for OnTrack

# Task Learning Outcome

| Field        | Type   | Null | Key     | Default | Extra          |
|--------------|--------|------|---------|---------|----------------|
| id           | int    | no   | Primary |         | auto_increment |
| name         | string | no   |         |         |                |
| tlo_number   | int    | no   |         |         |                |
| abbreviation | string | no   |         |         |                |
| description  | string | no   |         |         |                |

Need to clarify if task learning outcome is different to what happens in learning outcome task link. Otherwise the model is similar and will be used similarly to learning outcome for this purpose, except instead of being a learning outcome for the unit, its different for each task and will be grouped that way. The routes will mirror that of learning outcome and be the following.

# Possible routes

- [] add an outcome to a task
	/tasks/:task_id/outcomes

	requires
	task_id, name, desc, abbr

- [] update tlo
	/tasks/:task_id/outcomes/:id

	requires
	task_id, name, desc, abbr, tlo_number

- [] delete an outcome from a task
	/tasks/:task_id/outcomes/:id

	requires
	task_id, id

- [] download the outcomes for a unit to a csv
- [] upload the outcomes for a unit from a csv

# Questions
- why is ilo used for learning outcome and not lo? does the i stand for something else

 - should task learning outcome share the same table as learning outcomes, keeping separate would be easier to manage, however it does share a lot of functionality with learning outcome, so we could reuse some of the existing functions if they would still even work.



# Feedback Chip

| Field        | Type            | Null | Key     | Default | Extra          |
|--------------|-----------------|------|---------|---------|----------------|
| id           | int             | no   | Primary |         | auto_increment |
| title        | string          | no   |         |         |                |
| parentChipId | feedbackChip    | yes  |         |         |                |
| childChipId  | feedbackChip    | yes  |         |         |                |
| belongsTo    | learningOutcome | no   |         |         |                |

Feedback Chips are generic versions of the following group and template chips. A group chip can either be the root chip of the whole tree, or act as each node heads, where template chips are the leaves that populate the text when clicked. The group chips should be stored in the same table as the base chips and be linked within the same table to save space.

# Feedback Group Chip

| Field        | Type            | Null | Key     | Default | Extra          |
|--------------|-----------------|------|---------|---------|----------------|
| id           | int             | no   | Primary |         | auto_increment |
| title        | string          | no   |         |         |                |
| parentChipId | feedbackChip    | yes  |         |         |                |
| childChipId  | feedbackChip    | yes  |         |         |                |
| belongsTo    | learningOutcome | no   |         |         |                |

A feedback chip can belong to either a task learning outcome, global learning outcome, course learning outcome, ect. These act as broader categories that you will be able to filter by within the interface and will provide context.

# Feedback Template Chip

| Field        | Type       | Null | Key     | Default | Extra          |
|--------------|------------|------|---------|---------|----------------|
| id           | int        | no   | Primary |         | auto_increment |
| abbreviation | string     | no   |         |         |                |
| order        | number     | no   |         |         |                |
| chipText     | char[20]   | no   |         |         |                |
| description  | string     | no   |         |         |                |
| commentText  | string     | no   |         |         |                |
| summaryText  | string     | no   |         |         |                |
| taskStatus   | taskStatus | no   |         |         |                |

The feedback template chip will store the relevant information that when clicked, will populate the response box in the UI with the appropriate feedback. These are the final leaves in the chip tree and will be disabled when clicked while remaining in that level of the tree. 

# Feedback Chip Audit

| Field              | Type         | Null | Key     | Default | Extra          |
|--------------------|--------------|------|---------|---------|----------------|
| id                 | int          | no   | Primary |         | auto_increment |
| taskId             | task         | no   |         |         |                |
| userId             | user         | no   |         |         |                |
| feedbackTemplateId | feedbackChip | no   |         |         |                |

We will track usage data using these template chips, taking the task id, user id, and feedback template id. This will be used to gauge how often certain chips are being used, as well as the types of feedback commonly given for a certain task.


# Changes that need to be made to existing tables/relationships

learning outcome will gain to establish the relationship
has_many :feedback_chips