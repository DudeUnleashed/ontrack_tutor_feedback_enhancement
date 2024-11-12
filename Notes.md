# Notes

This document will store my notes as I work on outlining the plans for this feature.

# Things to mention
The chips have no direct connection to the task definition or unit directly. The chips will interact with the learning outcome types as a layer of abstraction. The front end can then just grab all chips relating to either type of learning outcome.

# Things to flesh out more
Add all the necessary endpoints that frontend requires, not sure how specific the backend needs to be as a lot of the work is done by frontend for this component.
Develop front end UI for the creation of these feedback chips and have them correctly created and tested in the backend.

# Week 1 Notes

The learning outcomes table is going to handle all types of learning outcomes.
Polymorphic association between tlo and tasks, ulo to units, ect.
Check task comments for examples of polymorphic

Unit_id becomes context_id or something, this is generic for each type of learning outcome.
Inject new context type string, no default
Update all after to unit

Remove task links table, ratings are no longer needed, as a complete task now indicates that all tlo are completed.

Learning outcomes should be able to link to other learning outcomes, so task relating to unit, unit relating to course, ect.

# Week 2 Notes

Looked over the learning outcomes api and modified the endpoints to accept the new context_id and context_string to consolidate the endpoints so they can create learning outcomes for any type.
Started creating the api for feedback_chip and feedback_template_chip with the basic CRUD endpoints for each.
Need to discuss how specific the endpoints want to be, and see what other endpoints for these would be useful for the frontend implementation.

Will look into the table changes required for these changes to work, and all the problems that could occur throughout the system due to this change.

# Week 3 Notes

Created diagrams for the db changes, including the shift from unit_id to context_type and context_id for learning outcomes and the removal of the learning outcome task link

Need to question and identify exactly what the belongsTo field of the feedback chip entails, if its not acting as a context definer we should include one for easy sorting.
In the original document belongsTo was a taskDefinition, since we are now using all sorts of types, should this change to context_type, or maybe learning_outcome_id instead.
Need a way to easily grab the chips that fall under the same category, if belongsTo is now just learning outcome we can grab all the same type eg, unit, course, task, ect.

A feedback chip now also is linked to both learningoutcomes and taskdefinitions, a new field is added for this
context_id and context_type can be null as there can be outcomes with no link to a type, eg clo. There needs to be validation so both are null, or both are full, cant have a type null and id true.
Feedback group and templates are stored in the same table, use polymorphism to achieve this, and have groups linked to templates within the same table.

Use feedback chip as a core, and group/template as types of chips for a nicer model.
Maybe store some info 
Sort feedback files into folders for better sorting
learning_outcomes becomes recursive.
Go over josh's additions previously and see what needs to be changed, ect.
