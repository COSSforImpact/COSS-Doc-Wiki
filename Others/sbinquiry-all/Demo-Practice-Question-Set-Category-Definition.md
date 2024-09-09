
### Demo Practice Question Set (without Sections)
Curl command to run




```
curl -L -X PATCH '{{host}}/object/category/definition/v4/update/obj-cat:demo-practice-question-set_questionset_all' \
-H 'Content-Type: application/json' \
--data-raw '{
  "request": {
    
  }
}'
```
Pass the below body into the request in the above curl command


```json
{
    "objectMetadata": {
      "config": {
        "sourcingSettings": {
          "collection": {
            "objectType": "QuestionSet",
            "primaryCategory": "Demo Practice Question Set",
            "maxDepth": 0,
            "isRoot": true,
            "iconClass": "",
            "children": {
              "Question": []
            },
            "hierarchy": {}
          }
        }
      },
      "schema": {
        "properties": {
          "mimeType": {
            "type": "string",
            "enum": [
              "application/vnd.sunbird.questionset"
            ]
          }
        }
      }
    },
    "languageCode": [],
    "forms": {
      "create": {
        "templateName": "",
        "required": [],
        "properties": [
          {
            "name": "Basic details",
            "fields": [
              
              {
                "code": "appIcon",
                "name": "Icon",
                "label": "Icon",
                "placeholder": "Icon",
                "description": "Icon for the question set",
                "dataType": "text",
                "inputType": "appIcon",
                "editable": true,
                "required": true,
                "visible": true,
                "renderingHints": {
                  "class": "sb-g-col-lg-1 required"
                }
              },
              {
                "code": "name",
                "name": "Name",
                "label": "Name",
                "placeholder": "Enter Name",
                "description": "Name of the Question Set",
                "dataType": "text",
                "inputType": "text",
                "editable": true,
                "required": true,
                "visible": true,
                "renderingHints": {
                  "class": "sb-g-col-lg-1 required"
                },
                "validations": [
                  {
                    "type": "maxLength",
                    "value": "120",
                    "message": "Entered name is too long"
                  },
                  {
                    "type": "required",
                    "message": "Name is required"
                  }
                ]
              },
              {
                "code": "description",
                "name": "Description",
                "label": "Description",
                "placeholder": "Enter Description",
                "description": "Description of the Question Set",
                "dataType": "text",
                "inputType": "textarea",
                "editable": true,
                "required": true,
                "visible": true,
                "renderingHints": {
                  "class": "sb-g-col-lg-1 required"
                },
                "validations": [
                  {
                    "type": "required",
                    "message": "Description is required"
                  }
                ]
              },
              {
                "code": "keywords",
                "name": "Keywords",
                "label": "Keywords",
                "placeholder": "Enter Keywords",
                "description": "Keywords for the Question Set",
                "dataType": "list",
                "inputType": "keywords",
                "editable": true,
                "required": false,
                "visible": true,
                "renderingHints": {
                  "class": "sb-g-col-lg-1"
                },
                "validations": []
              },
              {
                "code": "instructions",
                "name": "Instructions",
                "label": "Instructions",
                "placeholder": "Enter Instructions",
                "description": "Instructions for the question set",
                "dataType": "text",
                "inputType": "textarea",
                "editable": true,
                "required": false,
                "visible": true,
                "renderingHints": {
                  "class": "sb-g-col-lg-2"
                },
                "validations": [
                    {
                        "type": "maxLength",
                        "value": "500",
                        "message": "Input is Exceeded"
                    }
                ]
              },
              {
                "code": "primaryCategory",
                "name": "Type",
                "label": "Type",
                "placeholder": "",
                "description": "Type or Category of the Question Set",
                "dataType": "text",
                "inputType": "text",
                "editable": false,
                "required": true,
                "visible": true,
                "renderingHints": {
                  "class": "sb-g-col-lg-1 required"
                }
              },
              {
                "code": "additionalCategories",
                "name": "Additional Category",
                "label": "Additional Category",
                "placeholder": "Select Additional Category",
                "description": "Additonal Category of the Question Set",
                "default": "",
                "dataType": "list",
                "inputType": "nestedselect",
                "editable": true,
                "required": false,
                "visible": true,
                "renderingHints": {
                  "class": "sb-g-col-lg-1"
                }
              }
            ]
          },
          {
            "name": "",
            "fields": [
              {
                "code": "board",
                "name": "Board/Syllabus",
                "label": "Board/Syllabus",
                "placeholder": "Select Board/Syllabus",
                "description": "Board or Syallbus of the Question Set",
                "default": "",
                "dataType": "text",
                "inputType": "select",
                "editable": true,
                "required": true,
                "visible": true,
                "depends": [],
                "renderingHints": {
                  "class": "sb-g-col-lg-1 required"
                },
                "validations": [
                  {
                    "type": "required",
                    "message": "Board is required"
                  }
                ]
              },
              {
                "code": "medium",
                "name": "Medium",
                "label": "Medium",
                "placeholder": "Select Medium",
                "description": "Medium of Instruction for the Question Set",
                "default": "",
                "dataType": "list",
                "inputType": "select",
                "editable": true,
                "required": true,
                "visible": true,
                "depends": [
                  "board"
                ],
                "renderingHints": {
                  "class": "sb-g-col-lg-1 required"
                },
                "validations": [
                  {
                    "type": "required",
                    "message": "Medium is required"
                  }
                ]
              },
              {
                "code": "gradeLevel",
                "name": "Class",
                "label": "Class",
                "placeholder": "Select Class",
                "description": "Class of the Question Set",
                "default": "",
                "dataType": "list",
                "inputType": "select",
                "editable": true,
                "required": true,
                "visible": true,
                "depends": [
                  "board",
                  "medium"
                ],
                "renderingHints": {
                  "class": "sb-g-col-lg-1 required"
                },
                "validations": [
                  {
                    "type": "required",
                    "message": "Class is required"
                  }
                ]
              },
              {
                "code": "subject",
                "name": "Subject",
                "label": "Subject",
                "placeholder": "Select Subject",
                "description": "Subject of the Question Set",
                "default": "",
                "dataType": "list",
                "inputType": "select",
                "editable": true,
                "required": true,
                "visible": true,
                "depends": [
                  "board",
                  "medium",
                  "gradeLevel"
                ],
                "renderingHints": {
                  "class": "sb-g-col-lg-1 required"
                },
                "validations": [
                  {
                    "type": "required",
                    "message": "Subject is required"
                  }
                ]
              },
              {
                "code": "topic",
                "name": "Topics",
                "label": "Topics",
                "placeholder": "Choose Topics",
                "description": "Choose Topics covered in the Question Set",
                "default": "",
                "dataType": "list",
                "inputType": "topicselector",
                "editable": true,
                "required": false,
                "visible": true,
                "depends": [
                  "board",
                  "medium",
                  "gradeLevel",
                  "subject"
                ],
                "renderingHints": {
                  "class": "sb-g-col-lg-1"
                }
              },
              {
                "code": "audience",
                "name": "Audience",
                "label": "Audience",
                "placeholder": "Select Audience",
                "description": "Audience of the Question Set",
                "dataType": "list",
                "inputType": "select",
                "editable": true,
                "required": true,
                "visible": true,
                "range": [
                  "Student",
                  "Teacher",
                  "Administrator"
                ],
                "renderingHints": {
                  "class": "sb-g-col-lg-1 required"
                },
                "validations": [
                  {
                    "type": "required",
                    "message": "Audience is required"
                  }
                ]
              }
            ]
          },
          {
            "name": "Question set behaviour",
            "fields": [
              {
                "code": "shuffle",
                "name": "Shuffle Questions",
                "label": "Shuffle Questions",
                "placeholder": "Shuffle Questions",
                "description": "Questions will be Shuffled while playing",
                "default": "false",
                "dataType": "boolean",
                "inputType": "checkbox",
                "editable": true,
                "required": false,
                "visible": true,
                "renderingHints": {
                  "class": "sb-g-col-lg-1"
                }
              },
              {
                "code": "maxQuestions",
                "name": "Show Questions",
                "label": "Show Questions",
                "placeholder": "Number of questions to be shown",
                "description": "Number of questions to be shown",
                "default": "",
                "dataType": "number",
                "inputType": "select",
                "editable": true,
                "required": false,
                "visible": true,
                "renderingHints": {
                  "class": "sb-g-col-lg-1"
                }
              },
              {
                "code": "showFeedback",
                "name": "Show Feedback",
                "label": "Show Feedback",
                "placeholder": "Show Correct/Incorrect Feedback",
                "description": "Show Correct/Incorrect Feedback",
                "default": "Yes",
                "dataType": "text",
                "inputType": "checkbox",
                "editable": true,
                "required": false,
                "visible": true,
                "renderingHints": {
                  "class": "sb-g-col-lg-1"
                }
              },
              {
                "code": "showSolutions",
                "name": "Show Solution",
                "label": "Show Solution",
                "placeholder": "Show Solution",
                "description": "Show Solution",
                "default": "Yes",
                "dataType": "text",
                "inputType": "checkbox",
                "editable": true,
                "required": false,
                "visible": true,
                "renderingHints": {
                  "class": "sb-g-col-lg-1"
                }
              },
              {
                "code": "maxTime",
                "name": "Maximum Time",
                "label": "Maximum time",
                "placeholder": "hh:mm:ss",
                "description": "Maximum Time for the question set",
                "default": "300",
                "dataType": "text",
                "inputType": "timer",
                "editable": true,
                "visible": true,
                "required": false,
                "renderingHints": {
                  "class": "sb-g-col-lg-1"
                },
                "validations": [
                  {
                    "type": "time",
                    "message": "Please enter in hh:mm:ss",
                    "value": "HH:mm:ss"
                  },
                  {
                    "type": "maxLength",
                    "value": "05:59:59",
                    "message": "Maximum time should be less than 05:59:59"
                  }
                ]
              },
              {
                "code": "warningTime",
                "name": "Warning Time",
                "label": "Warning Time",
                "placeholder": "hh:mm:ss",
                "description": "Warning time for the question set",
                "dataType": "list",
                "inputType": "timer",
                "editable": true,
                "required": false,
                "visible": true,
                "depends": [
                  "maxTime"
                ],
                "renderingHints": {
                  "class": "sb-g-col-lg-1"
                },
                "validations": [
                  {
                    "type": "time",
                    "message": "Please enter hh:mm:ss",
                    "value": "HH:mm:ss"
                  },
                  {
                    "type": "compare",
                    "criteria": {
                      "<=": [
                        "maxTime"
                      ]
                    },
                    "message": "Warning time should be less than Max time"
                  }
                ]
              },
              {
                "code": "showTimer",
                "visible": false,
                "editable": false,
                "dataType": "text",
                "default": "Yes",
                "depends": [
                  "maxTime"
                ],
                "name": "Show Timer",
                "renderingHints": {
                  "class": "sb-g-col-lg-1"
                },
                "description": "Show Timer",
                "inputType": "checkbox",
                "label": "Show Timer",
                "placeholder": "Show Timer",
                "required": false
              },
              {
               "code": "summaryType",
               "dataType": "text",
               "description": "summaryType",
               "editable": true,
               "inputType": "select",
               "label": "Summary Type",
               "name": "summaryType",
               "placeholder": "Select Summary Type",
               "renderingHints": {
                   "class": "sb-g-col-lg-1"
               },
               "required": false,
               "visible": true,
               "range": [
                   "Complete",
                   "Score",
                   "Duration",
                   "Score & Duration"
                 ]
               }
            ]
          },
          {
            "name": "Ownership & Legal",
            "fields": [
              {
                "code": "author",
                "name": "Author",
                "label": "Author",
                "placeholder": "Enter Author",
                "description": "Author of the question set",
                "default": "",
                "dataType": "text",
                "inputType": "text",
                "editable": true,
                "required": true,
                "visible": true,
                "renderingHints": {
                  "class": "sb-g-col-lg-1 required"
                },
                "validations": [
                  {
                    "type": "required",
                    "message": "Author is required"
                  }
                ]
              },
              {
                "code": "attributions",
                "name": "Attributions",
                "label": "Attributions",
                "placeholder": "Enter Attributions",
                "description": "Attributions of the question set",
                "dataType": "text",
                "inputType": "text",
                "editable": true,
                "required": false,
                "visible": true,
                "renderingHints": {
                  "class": "sb-g-col-lg-1"
                }
              },
              {
                "code": "copyright",
                "name": "Copyright",
                "label": "Copyright",
                "placeholder": "Copyright",
                "description": "Copyright",
                "dataType": "text",
                "inputType": "text",
                "editable": true,
                "required": true,
                "visible": true,
                "renderingHints": {
                  "class": "sb-g-col-lg-1 required"
                },
                "validations": [
                  {
                    "type": "required",
                    "message": "Copyright is required"
                  }
                ]
              },
              {
                "code": "copyrightYear",
                "name": "Copyright Year",
                "label": "Copyright Year",
                "placeholder": "Copyright Year",
                "description": "Year of the Copyright",
                "dataType": "number",
                "inputType": "text",
                "editable": true,
                "required": true,
                "visible": true,
                "renderingHints": {
                  "class": "sb-g-col-lg-1 required"
                },
                "validations": [
                  {
                    "type": "required",
                    "message": "Copyright Year is required"
                  }
                ]
              },
              {
                "code": "license",
                "name": "License",
                "label": "License",
                "placeholder": "Select license",
                "description": "License",
                "defaultValue": "CC BY 4.0",
                "dataType": "text",
                "inputType": "select",
                "editable": true,
                "required": true,
                "visible": true,
                "range": "",
                "renderingHints": {
                  "class": "sb-g-col-lg-1 required"
                }
              }
            ]
          }
        ]
      },
      "childMetadata": {
        "templateName": "",
        "required": [],
        "properties": [
          {
            "code": "name",
            "name": "Name",
            "label": "Name",
            "placeholder": "Name of the Question. E.g. Practice MCQ",
            "description": "Name helps you find it easily",
            "default": "",
            "dataType": "text",
            "inputType": "text",
            "editable": true,
            "required": true,
            "visible": true,
            "renderingHints": {
              "class": "sb-g-col-lg-1 required"
            },
            "validations": [
              {
                "type": "maxLength",
                "value": "100",
                "message": "Entered name is too long"
              },
              {
                "type": "required",
                "message": "Name is required"
              }
            ]
          },
          {
            "code": "bloomsLevel",
            "name": "Learning level",
            "label": "Learning level",
            "placeholder": "Select Learning level",
            "description": "Learning level of the question",
            "dataType": "text",
            "inputType": "select",
            "editable": true,
            "required": false,
            "visible": true,
            "range": [
              "remember",
              "understand",
              "apply",
              "analyse",
              "evaluate",
              "create"
            ],
            "renderingHints": {
              "class": "sb-g-col-lg-1"
            },
            "validations": []
          },
          {
            "code": "board",
            "name": "Board/Syllabus",
            "label": "Board/Syllabus",
            "placeholder": "Select Board/Syllabus",
            "description": "Board or Syallbus of the Question Set",
            "default": "",
            "dataType": "text",
            "inputType": "select",
            "editable": true,
            "required": true,
            "visible": true,
            "depends": [],
            "renderingHints": {
              "class": "sb-g-col-lg-1 required"
            },
            "validations": [
              {
                "type": "required",
                "message": "Board is required"
              }
            ]
          },
          {
            "code": "medium",
            "name": "Medium",
            "label": "Medium",
            "placeholder": "Select Medium",
            "description": "Medium of Instruction for the Question Set",
            "default": "",
            "dataType": "list",
            "inputType": "select",
            "editable": true,
            "required": true,
            "visible": true,
            "depends": [
              "board"
            ],
            "renderingHints": {
              "class": "sb-g-col-lg-1 required"
            },
            "validations": [
              {
                "type": "required",
                "message": "Medium is required"
              }
            ]
          },
          {
            "code": "gradeLevel",
            "name": "Class",
            "label": "Class",
            "placeholder": "Select Class",
            "description": "Class of the Question Set",
            "default": "",
            "dataType": "list",
            "inputType": "select",
            "editable": true,
            "required": true,
            "visible": true,
            "depends": [
              "board",
              "medium"
            ],
            "renderingHints": {
              "class": "sb-g-col-lg-1 required"
            },
            "validations": [
              {
                "type": "required",
                "message": "Class is required"
              }
            ]
          },
          {
            "code": "subject",
            "name": "Subject",
            "label": "Subject",
            "placeholder": "Select Subject",
            "description": "Subject of the Question Set",
            "default": "",
            "dataType": "list",
            "inputType": "select",
            "editable": true,
            "required": true,
            "visible": true,
            "depends": [
              "board",
              "medium",
              "gradeLevel"
            ],
            "renderingHints": {
              "class": "sb-g-col-lg-1 required"
            },
            "validations": [
              {
                "type": "required",
                "message": "Subject is required"
              }
            ]
          },
          {
            "code": "topic",
            "name": "Topics",
            "label": "Topics",
            "placeholder": "Choose Topics",
            "description": "Choose Topics covered in the Question Set",
            "default": "",
            "dataType": "list",
            "inputType": "topicselector",
            "editable": true,
            "required": false,
            "visible": true,
            "depends": [
              "board",
              "medium",
              "gradeLevel",
              "subject"
            ],
            "renderingHints": {
              "class": "sb-g-col-lg-1"
            }
          },
          {
                "code": "additionalCategories",
                "name": "Additional Category",
                "label": "Additional Category",
                "placeholder": "Select Additional Category",
                "description": "Additonal Category of the Question Set",
                "default": "Practice",
                "dataType": "list",
                "inputType": "nestedselect",
                "editable": true,
                "required": false,
                "visible": false,
                "renderingHints": {
                  "class": "sb-g-col-lg-1"
                }
              }
        ]
      }
    }
  }
```


 **Rich text instruction** 


```
{
                "code": "instructions",
                "name": "Instructions",
                "label": "Instructions",
                "placeholder": "Enter Instructions",
                "description": "Instructions for the question set",
                "dataType": "text",
                "inputType": "richtext",
                "editable": true,
                "required": false,
                "visible": true,
                "renderingHints": {
                  "class": "sb-g-col-lg-2"
                },
                "validations": [
                    {
                        "type": "maxLength",
                        "value": "500",
                        "message": "Input is Exceeded"
                    }
                ]
              }
```


*****

[[category.storage-team]] 
[[category.confluence]] 
