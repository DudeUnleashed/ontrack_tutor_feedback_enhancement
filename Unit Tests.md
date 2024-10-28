# Unit Tests required for Feedback Chips/Groups

- [] Test for orphaned feedback chips 
	- [] (no root parent to connect back to)

- [] Test for feedback chip loops 
	- [] (ensure that there is no duplicate parents in a tree resulting in an infinite loop)

- [] Test for tree completeness
	- [] (ensure that all nodes reach the root somehow)

- [] Test that the types of feedback chips stay connected to their appropriate sections of said trees
	- [] (ensure that each chips parent is of the same type in the chain, TLOs, CLOs, ect.)