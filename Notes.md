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
