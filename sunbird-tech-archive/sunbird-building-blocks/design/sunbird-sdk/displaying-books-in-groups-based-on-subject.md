---
icon: elementor
---

# Displaying Books In Groups Based On Subject

### Introduction <a href="#displayingbooksingroupsbasedonsubject-introduction" id="displayingbooksingroupsbasedonsubject-introduction"></a>

This wiki explains that how to display search result based on subject. [SB-10221](https://project-sunbird.atlassian.net/browse/SB-10221)

### Problem Statement <a href="#displayingbooksingroupsbasedonsubject-problemstatement" id="displayingbooksingroupsbasedonsubject-problemstatement"></a>

Display the books in groups based on subject by using content search API.

### Proposed Design <a href="#displayingbooksingroupsbasedonsubject-proposeddesign" id="displayingbooksingroupsbasedonsubject-proposeddesign"></a>

**Solution 1:**

* Fetch the list of available TextBook for a selected board, medium and grade.

```
"request": {
		"mode": "hard",
		"filters": {
			"objectType": "Content",
			"board: ["Karnataka"],
			"gradeLevel": ["Class 5"],
			"medium": ["English"]
		},
		"limit": 0,
		"facets": ["subject"]
	}
```

\


* For each subject returned in the above API response (facets), use the below search API to fetch the content.

```
"request": {
		"filters": {
			"mode": "hard",
			"objectType": "Content",
			"contentType": ["TextBook"],
			"board: ["Karnataka"],
			"gradeLevel": ["Class 5"],
			"medium": ["English"],
			"subject": "evs"
		},
		"limit": 100,
		"fields": ["name", "appIcon"]
	}
```

\


* In this approach **n+1** API call will be there. Here **n** is number of facets returned for subject.

\


**Solution 2:**

* Fetch the list of available TextBook for a selected board, medium and grade.
* ```
  "request": {
  		"mode": "hard",
  		"filters": {
  			"objectType": "Content",
  			"contentType": ["TextBook"],
  			"board: ["Karnataka"],
  			"gradeLevel": ["Class 5"],
  			"medium": ["English"]
  		},
  		"limit": 0,
  		"facets": ["subject"]
  	}
  ```
* Group the subject locally in GenieSDK.

**Solution 2:**

* Fetch the list of available TextBook for a selected board, medium and grade by using some wrapper API on the top of search API.
* ```
  "request": {
  		"mode": "hard",
  		"filters": {
  			"objectType": "Content",
  			"contentType": ["TextBook"],
  			"board: ["Karnataka"],
  			"gradeLevel": ["Class 5"],
  			"medium": ["English"]
  		},
  		"limit": 0,
  		"facets": ["subject"]
  	}
  ```
* This API will return the response groups based on subject.

\


[Swayangjit Parida](https://project-sunbird.atlassian.net/wiki/people/557058:69780b52-eed2-43e4-b273-6473bac18bac?ref=confluence) [Rayulu Villa](https://project-sunbird.atlassian.net/wiki/people/557058:cee0b254-59ea-4cde-9b36-aa4d8d417643?ref=confluence) [Santhosh Vasabhaktula](https://project-sunbird.atlassian.net/wiki/people/557058:6be72d49-04d0-4cce-aaec-cb8ccf26e787?ref=confluence) [Mathew Pallan](https://project-sunbird.atlassian.net/wiki/people/5a0147f1c24efb3c4ed42ac8?ref=confluence)

\


\
