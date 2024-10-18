---
icon: elementor
---

# Course Infra - AUDIT Telemetry

#### **Common AUDIT Event Structure:** <a href="#courseinfra-audittelemetry-commonauditeventstructure" id="courseinfra-audittelemetry-commonauditeventstructure"></a>

```
{
  "eid": , "AUDIT",
  "ets": , 1592803822,
  "ver": "3.0", 
  "mid": , "LP.AUDIT.1592803822"
  "actor": { 
    "id": "<userid>", 
    "type":  "User"
  },

  // Context of the event
  "context": { 
    "channel": "<default_value>", 
    "pdata": { 
      "id": "org.sunbird.learning.platform", 
      "pid": "course-progress-updater", 
      "ver": 1.0
    },
    "env": "Course",
    "cdata": [{ 
      "type":"CourseBatch", 
      "id": "<batchId>" 
    }]
  },
  "object": {}, // Required.
  "edata": {} // Required.
}
```

#### Scenarios: <a href="#courseinfra-audittelemetry-scenarios" id="courseinfra-audittelemetry-scenarios"></a>

**1. Course - Start:**

```
{
  "eid": "AUDIT",
  "object": {
    "id": "<course_id>",
    "type": "Course",
    "rollup": {
      "l1": "<courseId>"
    }
  },
  "edata": {
    "props": ["identifier","enrolledDate","courseId", "active"],
    "type": "course-enroll"
  }
}
```

**2. Course - Complete:**

```
{
  "eid": "AUDIT",
  "object": {
    "id": "<course_id>",
    "type": "Course",
    "rollup": {
      "l1": "<courseId>"
    }
  },
  "edata": {
    "props": ["completedDate"],
    "type": "course-complete"
  }
}
```

**3. CourseUnit - Start:**

```
{
  "eid": "AUDIT",
  "object": {
    "id": "<courseunit_id>",
    "type": "CourseUnit",
    "rollup": {
      "l1": "<courseId>"
    }
  },
  "edata": {
    "props": ["identifer"],
    "type": "start"
  }
}
```

**4. CourseUnit - Complete:**

```
{
  "eid": "AUDIT",
  "object": {
    "id": "<courseunit_id>",
    "type": "CourseUnit",
    "rollup": {
      "l1": "<courseId>"
    }
  },
  "edata": {
    "props": ["lastCompletedOn"],
    "type": "complete"
  }
}
```

**5. Content - Start:**

```
{
  "eid": "AUDIT",
  "object": {
    "id": "<content_id>",
    "type": "Content",
    "rollup": {
      "l1": "<courseId>",
      "l2": "<courseunit_id>"
    }
  },
  "edata": {
    "props": ["identifer"],
    "type": "start"
  }
}
```

**6. Content - Complete:**

```
{
  "eid": "AUDIT",
  "object": {
    "id": "<content_id>",
    "type": "Content",
    "rollup": {
      "l1": "<courseId>",
      "l2": "<courseunit_id>"
    }
  },
  "edata": {
    "props": ["lastCompletedOn"],
    "type": "complete"
  }
}
```
