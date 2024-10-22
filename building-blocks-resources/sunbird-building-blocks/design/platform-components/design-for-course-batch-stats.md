---
icon: elementor
---

# Design for course batch stats

**Approach 1**

Nested participant object in one documents

```
Create an index and add settings

curl -X PUT 
http://localhost:9200/cbatchstats/ 
-H 'Content-Type: application/json' 
-H 'Postman-Token: a39bca1e-1412-45f2-bf3a-814109bd31c3' 
-H 'cache-control: no-cache' 
-d '{
  "settings": {
    "index": {
      "number_of_shards": "5",
      "analysis": {
        "filter": {
          "mynGram": {
            "token_chars": [
              "letter",
              "digit",
              "whitespace",
              "punctuation",
              "symbol"
            ],
            "min_gram": "1",
            "type": "ngram",
            "max_gram": "20"
          }
        },
        "analyzer": {
          "cs_index_analyzer": {
            "filter": [
              "lowercase",
              "mynGram"
            ],
            "type": "custom",
            "tokenizer": "standard"
          },
          "keylower": {
            "filter": "lowercase",
            "type": "custom",
            "tokenizer": "keyword"
          },
          "cs_search_analyzer": {
            "filter": [
              "lowercase",
              "standard"
            ],
            "type": "custom",
            "tokenizer": "standard"
          }
        }
      },
      "number_of_replicas": "1"
    }
  }
}'

Creating mapping for the index

curl -X PUT 
http://localhost:9200/cbatchstats/_mapping/_doc 
-H 'Content-Type: application/json' 
-H 'Postman-Token: 5c2af6f7-8def-4122-b556-6c0a77d70675,56e956f8-f95b-4d7a-890f-2bf1da73db98,57d38de5-aa80-40b4-980b-52a1206a20c4' 
-H 'cache-control: no-cache,no-cache,no-cache' 
-d '{
  "dynamic": false,
  "properties": {
    "all_fields": {
      "type": "text",
      "fields": {
        "raw": {
          "type": "text",
          "analyzer": "keylower"
        }
      },
      "analyzer": "cs_index_analyzer",
      "search_analyzer": "cs_search_analyzer"
    },
    "batchId": {
      "type": "text",
      "fields": {
        "raw": {
          "type": "text",
          "analyzer": "keylower",
          "fielddata": true
        }
      },
      "copy_to": [
        "all_fields"
      ],
      "analyzer": "cs_index_analyzer",
      "search_analyzer": "cs_search_analyzer",
      "fielddata": true
    },
    "completedCount": {
      "type": "long",
      "fields": {
        "raw": {
          "type": "long"
        }
      }
    },
    "courseId": {
      "type": "text",
      "fields": {
        "raw": {
          "type": "text",
          "analyzer": "keylower",
          "fielddata": true
        }
      },
      "copy_to": [
        "all_fields"
      ],
      "analyzer": "cs_index_analyzer",
      "search_analyzer": "cs_search_analyzer",
      "fielddata": true
    },
    "endDate": {
      "type": "date",
      "fields": {
        "raw": {
          "type": "date"
        }
      }
    },
    "lastUpdatedOn": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "participantCount": {
      "type": "long",
      "fields": {
        "raw": {
          "type": "long"
        }
      }
    },
    "participants": {
      "properties": {
        "completedPercent": {
          "type": "long",
          "fields": {
            "raw": {
              "type": "long"
            }
          }
        },
        "districtName": {
          "type": "text",
          "fields": {
            "raw": {
              "type": "text",
              "analyzer": "keylower",
              "fielddata": true
            }
          },
          "copy_to": [
            "all_fields"
          ],
          "analyzer": "cs_index_analyzer",
          "search_analyzer": "cs_search_analyzer",
          "fielddata": true
        },
        "enrolledOn": {
          "type": "date",
          "fields": {
            "raw": {
              "type": "date"
            }
          }
        },
        "active": {
          "type": "boolean",
          "fields": {
            "raw": {
              "type": "boolean"
            }
          }
        },
        "maskedEmail": {
          "type": "text",
          "fields": {
            "raw": {
              "type": "text",
              "analyzer": "keylower",
              "fielddata": true
            }
          },
          "copy_to": [
            "all_fields"
          ],
          "analyzer": "cs_index_analyzer",
          "search_analyzer": "cs_search_analyzer",
          "fielddata": true
        },
        "maskedExternalId": {
          "type": "text",
          "fields": {
            "raw": {
              "type": "text",
              "analyzer": "keylower",
              "fielddata": true
            }
          },
          "copy_to": [
            "all_fields"
          ],
          "analyzer": "cs_index_analyzer",
          "search_analyzer": "cs_search_analyzer",
          "fielddata": true
        },
        "maskedPhone": {
          "type": "text",
          "fields": {
            "raw": {
              "type": "text",
              "analyzer": "keylower",
              "fielddata": true
            }
          },
          "copy_to": [
            "all_fields"
          ],
          "analyzer": "cs_index_analyzer",
          "search_analyzer": "cs_search_analyzer",
          "fielddata": true
        },
        "name": {
          "type": "text",
          "fields": {
            "keyword": {
              "type": "keyword",
              "ignore_above": 256
            }
          }
        },
        "rootOrgName": {
          "type": "text",
          "fields": {
            "raw": {
              "type": "text",
              "analyzer": "keylower",
              "fielddata": true
            }
          },
          "copy_to": [
            "all_fields"
          ],
          "analyzer": "cs_index_analyzer",
          "search_analyzer": "cs_search_analyzer",
          "fielddata": true
        },
        "subOrgName": {
          "type": "text",
          "fields": {
            "raw": {
              "type": "text",
              "analyzer": "keylower",
              "fielddata": true
            }
          },
          "copy_to": [
            "all_fields"
          ],
          "analyzer": "cs_index_analyzer",
          "search_analyzer": "cs_search_analyzer",
          "fielddata": true
        }
      }
    },
    "startDate": {
      "type": "date",
      "fields": {
        "raw": {
          "type": "date"
        }
      }
    }
  }
}'
```

\


**Approach 2**

Create separate document for each user in course batch

\


```
Create an index and add settings

curl -X PUT 
http://localhost:9200/cbatchstats/ 
-H 'Content-Type: application/json' 
-H 'Postman-Token: a39bca1e-1412-45f2-bf3a-814109bd31c3' 
-H 'cache-control: no-cache' 
-d '{	
"settings": {
"index": {
"number_of_shards": "5",
"analysis": {
"filter": {
"mynGram": {
"token_chars": ["letter", "digit", "whitespace", "punctuation", "symbol"],
"min_gram": "1",
"type": "ngram",
"max_gram": "20"
}
},
"analyzer": {
"cs_index_analyzer": {
"filter": ["lowercase", "mynGram"],
"type": "custom",
"tokenizer": "standard"
},
"keylower": {
"filter": "lowercase",
"type": "custom",
"tokenizer": "keyword"
},
"cs_search_analyzer": {
"filter": ["lowercase", "standard"],
"type": "custom",
"tokenizer": "standard"
}
}
},
"number_of_replicas": "1"
}
}
}'

Creating mapping for the index

curl -X PUT 
http://localhost:9200/cbatchstats/_mapping/_doc 
-H 'Content-Type: application/json' 
-H 'Postman-Token: 5c2af6f7-8def-4122-b556-6c0a77d70675,56e956f8-f95b-4d7a-890f-2bf1da73db98,57d38de5-aa80-40b4-980b-52a1206a20c4' 
-H 'cache-control: no-cache,no-cache,no-cache' 
-d '{
  "dynamic": false,
  "properties": {
    "all_fields": {
      "type": "text",
      "fields": {
        "raw": {
          "type": "text",
          "analyzer": "keylower"
        }
      },
      "analyzer": "cs_index_analyzer",
      "search_analyzer": "cs_search_analyzer"
    },
    "batchId": {
      "type": "text",
      "fields": {
        "raw": {
          "type": "text",
          "analyzer": "keylower",
          "fielddata": true
        }
      },
      "copy_to": [
        "all_fields"
      ],
      "analyzer": "cs_index_analyzer",
      "search_analyzer": "cs_search_analyzer",
      "fielddata": true
    },
    "completedCount": {
      "type": "long",
      "fields": {
        "raw": {
          "type": "long"
        }
      }
    },
    "courseId": {
      "type": "text",
      "fields": {
        "raw": {
          "type": "text",
          "analyzer": "keylower",
          "fielddata": true
        }
      },
      "copy_to": [
        "all_fields"
      ],
      "analyzer": "cs_index_analyzer",
      "search_analyzer": "cs_search_analyzer",
      "fielddata": true
    },
    "endDate": {
      "type": "date",
      "fields": {
        "raw": {
          "type": "date"
        }
      }
    },
    "lastUpdatedOn": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "participantCount": {
      "type": "long",
      "fields": {
        "raw": {
          "type": "long"
        }
      }
    },
    "completedPercent": {
      "type": "long",
      "fields": {
        "raw": {
          "type": "long"
        }
      }
    },
    "districtName": {
      "type": "text",
      "fields": {
        "raw": {
          "type": "text",
          "analyzer": "keylower",
          "fielddata": true
        }
      },
      "copy_to": [
        "all_fields"
      ],
      "analyzer": "cs_index_analyzer",
      "search_analyzer": "cs_search_analyzer",
      "fielddata": true
    },
    "enrolledOn": {
      "type": "date",
      "fields": {
        "raw": {
          "type": "date"
        }
      }
    },
    "maskedEmail": {
      "type": "text",
      "fields": {
        "raw": {
          "type": "text",
          "analyzer": "keylower",
          "fielddata": true
        }
      },
      "copy_to": [
        "all_fields"
      ],
      "analyzer": "cs_index_analyzer",
      "search_analyzer": "cs_search_analyzer",
      "fielddata": true
    },
    "maskedExternalId": {
      "type": "text",
      "fields": {
        "raw": {
          "type": "text",
          "analyzer": "keylower",
          "fielddata": true
        }
      },
      "copy_to": [
        "all_fields"
      ],
      "analyzer": "cs_index_analyzer",
      "search_analyzer": "cs_search_analyzer",
      "fielddata": true
    },
    "maskedPhone": {
      "type": "text",
      "fields": {
        "raw": {
          "type": "text",
          "analyzer": "keylower",
          "fielddata": true
        }
      },
      "copy_to": [
        "all_fields"
      ],
      "analyzer": "cs_index_analyzer",
      "search_analyzer": "cs_search_analyzer",
      "fielddata": true
    },
    "name": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "rootOrgName": {
      "type": "text",
      "fields": {
        "raw": {
          "type": "text",
          "analyzer": "keylower",
          "fielddata": true
        }
      },
      "copy_to": [
        "all_fields"
      ],
      "analyzer": "cs_index_analyzer",
      "search_analyzer": "cs_search_analyzer",
      "fielddata": true
    },
    "subOrgName": {
      "type": "text",
      "fields": {
        "raw": {
          "type": "text",
          "analyzer": "keylower",
          "fielddata": true
        }
      },
      "copy_to": [
        "all_fields"
      ],
      "analyzer": "cs_index_analyzer",
      "search_analyzer": "cs_search_analyzer",
      "fielddata": true
    },
    "startDate": {
      "type": "date",
      "fields": {
        "raw": {
          "type": "date"
        }
      }
    }
  }
}'
```

\


\


**Approach 3**

\
\


```
Create an index and add settings

curl -X PUT 
http://localhost:9200/cbatchstats/ 
-H 'Content-Type: application/json' 
-H 'Postman-Token: a39bca1e-1412-45f2-bf3a-814109bd31c3' 
-H 'cache-control: no-cache' 
-d '{	
"settings": {
"index": {
"number_of_shards": "5",
"analysis": {
"filter": {
"mynGram": {
"token_chars": ["letter", "digit", "whitespace", "punctuation", "symbol"],
"min_gram": "1",
"type": "ngram",
"max_gram": "20"
}
},
"analyzer": {
"cs_index_analyzer": {
"filter": ["lowercase", "mynGram"],
"type": "custom",
"tokenizer": "standard"
},
"keylower": {
"filter": "lowercase",
"type": "custom",
"tokenizer": "keyword"
},
"cs_search_analyzer": {
"filter": ["lowercase", "standard"],
"type": "custom",
"tokenizer": "standard"
}
}
},
"number_of_replicas": "1"
}
}
}'

Creating mapping for the index

curl -X PUT 
http://localhost:9200/cbatchstats/_mapping/_doc 
-H 'Content-Type: application/json' 
-H 'Postman-Token: 5c2af6f7-8def-4122-b556-6c0a77d70675,56e956f8-f95b-4d7a-890f-2bf1da73db98,57d38de5-aa80-40b4-980b-52a1206a20c4' 
-H 'cache-control: no-cache,no-cache,no-cache' 
-d '{
  "dynamic": false,
  "properties": {
    "all_fields": {
      "type": "text",
      "fields": {
        "raw": {
          "type": "text",
          "analyzer": "keylower"
        }
      },
      "analyzer": "cs_index_analyzer",
      "search_analyzer": "cs_search_analyzer"
    },
    "batchId": {
      "type": "text",
      "fields": {
        "raw": {
          "type": "text",
          "analyzer": "keylower",
          "fielddata": true
        }
      },
      "copy_to": [
        "all_fields"
      ],
      "analyzer": "cs_index_analyzer",
      "search_analyzer": "cs_search_analyzer",
      "fielddata": true
    }
    "courseId": {
      "type": "text",
      "fields": {
        "raw": {
          "type": "text",
          "analyzer": "keylower",
          "fielddata": true
        }
      },
      "copy_to": [
        "all_fields"
      ],
      "analyzer": "cs_index_analyzer",
      "search_analyzer": "cs_search_analyzer",
      "fielddata": true
    }
    "lastUpdatedOn": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    }
    "completedPercent": {
      "type": "long",
      "fields": {
        "raw": {
          "type": "long"
        }
      }
    },
    "districtName": {
      "type": "text",
      "fields": {
        "raw": {
          "type": "text",
          "analyzer": "keylower",
          "fielddata": true
        }
      },
      "copy_to": [
        "all_fields"
      ],
      "analyzer": "cs_index_analyzer",
      "search_analyzer": "cs_search_analyzer",
      "fielddata": true
    },
    "enrolledOn": {
      "type": "date",
      "fields": {
        "raw": {
          "type": "date"
        }
      }
    },
    "maskedEmail": {
      "type": "text",
      "fields": {
        "raw": {
          "type": "text",
          "analyzer": "keylower",
          "fielddata": true
        }
      },
      "copy_to": [
        "all_fields"
      ],
      "analyzer": "cs_index_analyzer",
      "search_analyzer": "cs_search_analyzer",
      "fielddata": true
    },
    "maskedPhone": {
      "type": "text",
      "fields": {
        "raw": {
          "type": "text",
          "analyzer": "keylower",
          "fielddata": true
        }
      },
      "copy_to": [
        "all_fields"
      ],
      "analyzer": "cs_index_analyzer",
      "search_analyzer": "cs_search_analyzer",
      "fielddata": true
    },
    "name": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "rootOrgName": {
      "type": "text",
      "fields": {
        "raw": {
          "type": "text",
          "analyzer": "keylower",
          "fielddata": true
        }
      },
      "copy_to": [
        "all_fields"
      ],
      "analyzer": "cs_index_analyzer",
      "search_analyzer": "cs_search_analyzer",
      "fielddata": true
    },
    "subOrgName": {
      "type": "text",
      "fields": {
        "raw": {
          "type": "text",
          "analyzer": "keylower",
          "fielddata": true
        }
      },
      "copy_to": [
        "all_fields"
      ],
      "analyzer": "cs_index_analyzer",
      "search_analyzer": "cs_search_analyzer",
      "fielddata": true
    }
  }
}'
```

\


\
