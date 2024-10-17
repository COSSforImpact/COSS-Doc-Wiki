---
icon: elementor
---

# Sequencing of a question paper

Question paper needs to be sequenced. Have a Go-live/ Start date and a Live-Until/ End date. These are required to ensure that the Question paper can be prepared and published beforehand and will only be shown to students only after the start date and until the end date.

&#x20;

Approach 1:

1. This is configured as a property for the collection/ question set
2. The API sends all the Question papers in the search API
3. It will be the job of the frontend to identify the active/live question papers and show it to the users

&#x20;

Approach 2:

1. This is configured as a property for the collection/ question set
2. The API sends only a filtered list of question papers (Filtered for active; the date of request lies between the dates of Start and end date of question paper) relevant Question papers in the search API
