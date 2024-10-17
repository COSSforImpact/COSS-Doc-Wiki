---
icon: folder-open
---

# Object-Types

true

### Common Attributes

Attributes provided by User, or configured at global/tenant/category level:

| **Attribute** | **Definition**                                                          | **Details**                                                                                                        | **Applicable Object Types** | **Behaviour** |
| ------------- | ----------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ | --------------------------- | ------------- |
| name          | type: “string”, required: true                                          | Name (or title) of the object.                                                                                     | All                         |               |
| description   | type: “string”, required: false                                         | Description of the object.                                                                                         | All                         |               |
| mimeType      | type: “string”, required: true, enum: \[“list of supported mime types“] | <p>Technical mime type of the object.</p><ul><li>List of supported mime types vary for each object type.</li></ul> |                             |               |

* These are generally configured for each category or derived from the file uploaded by the user.

\| All | | | instructions | type: “string” or “json”, required: false, json format: {“key”: “value”} | Instructions on how to understand, attempt or how the object will be evaluated.

* supports instructions in multiple languages: key is the language code and value is instructions in HTML format in the specified language
* will be in “string” format (instead of a map) when the instructions are in only one language

\| Question, QuestionSet, Content, Collection |

* Shown as the first slide of the content
* Users should be able to view instructions anytime during the play session

\| | keywords | type: “list”, required: false | | All | | | Organisation Framework | frameworkId board, medium, gradeLevel, subject, topic, learningOutcomes | Every object can be tagged with one organisation framework and with one or more terms of the selected framework categories. Framework tagging is optional. | Question, QuestionSet, Content, Collection |

* Selection of organisation framework during creation

\| | Target Frameworks | List of framework Ids and framework terms | Every object can additionally be tagged with zero or more target frameworks and their terms. - Planned for R3.4C1: Org FW: subject: ICT, medium: English Target FW: board: MH, medium: Marathi/English, Grade: 6C2: Org FW: board: MH, medium: Marathi/English, Grade: 6, subject: EnglishWhen searched for “board: MH, medium: Marathi/English, Grade: 6“, C2 should be shown before C1 | Question, QuestionSet, Content, Collection |

* Selection of target framework during creation
* Platform should expand the search to use both org and target framework tags
* Configurable weightage to org framework & target framework tags
* Search & Filter - should use weightages

\| | Audience | type: “list”, required: false, enum: \\\[“student”, “teacher”, “admin”] | Target audience of the object. | Question, QuestionSet, Content, Collection |

* Categories and Filters vary based on the audience

\| | Visibility | type: “string”, required: true, enum: \\\[“public”, “protected“, “private“, “parent”] |

* public - visible to everyone in consumption and creation (currently, this value is “default”).
* protected - visible only for all creators during creation. consumption users cannot discover these objects.
* private - visible only for creators in the same organisation as the creator. Not visible for consumption users and creators of other organisations.
* parent - visible only within the context of the parent object, e.g.: a question very specific to a survey question set or a content within a course

\| All |

* Only “public” visibility objects should be searchable
* parent, private and protected can be consumed as part of the collection/question set
  * accesible via URL & DIAL codes?
  * guest user access allowed?

\| | License | type: “license”, required: true | One of the configured licenses in the platform. Value will be defaulted to the default license configured for the tenant and/or category. | All | | | Copyright Information | copyright, author, owner, attributions credits: objectCredits (previously contentCredits), voiceCredits, soundCredits, imageCredits | Additional copyright information provided by the creator. | All | | | Icons | appIcon, grayScaleAppIcon, thumbnail, posterImage, screenshots, stageIcons | | Question, QuestionSet, Content, Collection | | | PublishCheckList | type: “list” | List of items verified by publisher before publishing the object. Checklist items vary for each object type and configurable at global, tenant or category level. | Question, QuestionSet, Content, Collection | | | PublishComment | type: “string” | Comment given by publisher while approving the object. | Question, QuestionSet, Content, Collection | | | RejectReasons | type: “list” | List of reasons for rejecting the object. Checklist items vary for each object type and configurable at global, tenant or category level. | Question, QuestionSet, Content, Collection | | | RejectComment | type: “string” | Comment given by publisher while rejecting the object. | Question, QuestionSet, Content, Collection | | | DialCodeRequired | type: “boolean”, defaultValue: “false“ | To specify if a dial code has to be mandatorily linked to the object before publishing the object. | All |

* Editor should dial code field if this attribute is set to true
* Publish pipeline should check for dial code before publishing

\| | CompatibilityLevel | type: “number”, required: true, defaultValue: 1 | Compatibility level of the object, i.e. the minimum app version on which the content can be consumed. | Question, QuestionSet, Content, Collection |

* Mobile & desktop apps download/search/play content based on the compatibility level
* Platform to set the value using primary category definition or mime type config

\| | PrimaryCategory | type: “string”, required: true | Object category like “Survey”, “Quiz”, “Course”, etc - used for search & discovery purposes. Every object is created with one primary category. | All |

* Editors should show metadata form using the primary category config (default values, fixed values, range, required)
* Platform use the definition to set the valid values and validate the metadata
* How to handle changes to primary category definition?
* Primary categories configured at global level, tenant can override the list and/or definition

\| | AdditionalCategories | type: “list”, required: false | Additional (& optional) list of categories - used only for search & discovery. | All |

* TBD - Category Display on the consumption card??

\| | Trackable | type: “string”, required: true, enum: \\\[“yes”, “no”], defaultValue: “no” | If the object is trackable or not. If set as “yes”, user has to login to access the question set, user progress of the question set is tracked and can be monitored by the user & creator/admin of the question set. | QuestionSet, Content, Collection |

* Collection:
  * Consumption State of each content is stored - In Progress (with percentage of completion) or Complete
  * Collection level progress
    * Total count, completed count, In Progress count
    *
  *
* Logged in User’s state is stored in the server
* Completion

\| | RequiresEnrolment | | | |

* Batch creation and management will be enabled
*

\| | AutoCreateBatch | type: “boolean”, required: false | Should be set to true if a batch has to be auto created for an object on publish if the object is marked as trackable. The batch is created only if a live/upcoming batch doesn't exist for the object. The start date of the batch will be set to date of publish and no end date. Start and end dates can be modified for the auto-created batch by the creator or mentor. | QuestionSet, Content, Collection | | | DailySummaryReportEnabled | type: “boolean”, required: false | Should be set to true if daily summary aggregates have to be computed for an object that is marked as trackable. | | | | CredentialsAllowed | type: “string”, required: true, enum: \\\[“yes”, “no”], defaultValue: “no” | If credentials can be linked to object or not. This is applicable only for trackable objects. | QuestionSet, Content, Collection | | | CertTemplate | template: “certificate template details“, criteria: “based on completion or score or both“ | If object has any configured credentials to be issued to the users. | QuestionSet, Content, Collection | | | AllowAnonymousAccess | type: “boolean”, defaultValue: true | If the object is allowed to be consumed without login. \\\[TBD: behaviour when both trackable and allowAnonymousAccess are set as true. one option is that trackable becomes optional in this case, i.e. progress gets tracked only for logged in users] | Question, QuestionSet, Content, Collection | | | Terms\&Conditions | type: “string”, required”: false | URL of the terms & conditions page. If configured, user has to agree the “terms & conditions” before consuming the question set. The acceptance is captured as a telemetry event. | Question, QuestionSet, Content, Collection | | | ExpectedDuration | type: “float”, required: false | Expected time for consuming the object. It is a metadata set by the creator. | Question, QuestionSet, Content, Collection | | | CompletionCriteria | type: “json”, required: false | Criteria to consider the object as completed by user. The structure of critieria will be different for each object type. Example: { ”contentCount”: “minimum number of content to be completed“, ”questionCount”: “minimum number of questions to be answered“, ”score”: “minimum score to be achieved“ } | Question, QuestionSet, Content, Collection | | | MaxScore | type: “float”, required: false |

* Maximum score that can be awarded in this object, or,
* Marks in case of non-interactive question set use cases.

\| Question, QuestionSet, Content, Collection | | | Collaborators | type: “list”, required: false | List of collaborators for creating the object | All | | | SemanticVersion | type: “string”, required: false | Semantic version of the object. This is different from the published version. Semantic version is used to maintain same version number even though there are changes and object is re-published. | All | | | Code | type: “string”, required: true | Auto-generated, if not provided by the user. | All | | | FlagReasons | type: “list”, required: false | List of configured reasons like “copyright violation”, “inappropriate content”, etc. | All | | | Flags | type: “list”, required: false | List of comments given by the user while flagging the object. | All | | | Batch Information | type: “json”, required: true, format: { “identifier”: ““, “name”: “”, “startDate”: “”, “endDate”: ““, “enrolmentEndDate”: “, “status”: “Active/InActive“, “mentors“: \\\[“list of users who have access to batch data“] } | If object is trackable, a batch gets created for tracking enrolment and progress. Only one active batch is allowed at one time. | QuestionSet, Content, Collection | |

Attributes set/computed/derived by System:

| **Attribute** | **Definition**                                                                        | **Details**                                                                                    | **Applicable Object Types** |
| ------------- | ------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | --------------------------- |
| Status        | type: “list”, required: true, enum: \[“list of status values”], defaultValue: “Draft” | <p>Status of the object.</p><ul><li>List of status values vary for each object type.</li></ul> |                             |

\| All | | SchemaVersion | type: “string”, required: true | Version of the schema used for creating this object. | All | | EditorState | type: “json”, required: false | Editor state to restore objects from last saved state in editor. | Question, QuestionSet, Content, Collection | | PkgVersion | type: “number” | Package version is incremented on every publish of the object. | All | | DownloadUrl | type: “string” | ECAR file URL of the object. | QuestionSet, Content, Collection | | Size | type: “number” | Size in bytes of the ECAR file. | QuestionSet, Content, Collection | | Checksum | type: “number” | Checksum of the generated ECAR file | QuestionSet, Content, Collection | | ArtifactUrl | type: “string” | URL of the actual artifact file, i.e. the actual PDF, mp4 or zip file. | All | | PreviewUrl | type: “string” | Preview URL of the object for consumption in online mode. | All | | StreamingUrl | type: “string” | Streaming URL for mime types that support streaming play | All | | ContentEncoding | type: “list”, required: true, enum: \\\[“gzip”, “identity”] |

* gzip - if the artifact has to be extracted for consumption in the app, like epub, html zip, etc
* identity - if the artifact can be consumed directly without extraction, like mp4, webm, etc.

\| All | | ContentDisposition | type: “list”, required: false, enum: \\\["inline", "online", "online-only"] |

* inline - if the artifact is available in the ECAR file and can be consumed completely offline.
* online - if the ECAR has only artifactUrl and has to be downloaded (be online) for consumption. Post download, consumption can happen offline.
* online-only - the object cannot be consumed offline - like youtube videos and large videos.

\| All | | VersionKey | type: “string”, required: true | Unique version key verified and computed on every update to prevent stale updates. | All | | LockKey | type: “string” | Lock key used for locking an object for updates when multiple collaborators are working on the same object. | All | | DialCodes | type: “list” | List of DIAL codes linked to the object. | All | | ReservedDialCodes | type: “list” | List of DIAL codes reserved to be linked to this object. | All | | Assets | type: “list”, format: \\\[{“identifier“: “string“, “mimeType”: “string”, “src”: “string”, “baseUrl”: “string”}] | List of assets used in the object. | Question, QuestionSet, Content, Collection | | Error Details | uploadError, publishError, reviewError | Errors that occurred in various stages of the object lifecycle | All | | Ownership Information | channel, createdBy (creator), createdFor (organisation) | Ownership information for the object. | All | | Audit Information | createdBy, createdOn, lastUpdatedOn, lastUpdatedBy, lastSubmittedBy, lastSubmittedOn lastPublishedBy, lastPublishedOn, lastStatusChangedOn, prevState, flaggedBy, lastFlaggedOn | Audit Information. | All | | Source Information |

* origin - URI of the source object
* originData - basic metadata of the source object
* copyType - shallow OR deep

\| Details of the source from which the object is created. | All | | Analytics Data | me\_totalSessionsCount, me\_creationSessions, me\_creationTimespent, me\_totalTimespent, me\_totalInteractions, me\_averageInteractionsPerMin, me\_averageSessionsPerDevice, me\_totalDevices, me\_averageTimespentPerSession, me\_averageRating, me\_totalDownloads, me\_totalSideloads, me\_totalRatings, me\_totalComments, me\_totalUsage, me\_totalLiveContentUsage, me\_usageLastWeek, me\_deletionsLastWeek, me\_lastUsedOn, me\_lastRemovedOn | Statistical data about the object. These values are set by analytics systems based on the telemetry. | All |

***

\[\[category.storage-team]] \[\[category.confluence]]
