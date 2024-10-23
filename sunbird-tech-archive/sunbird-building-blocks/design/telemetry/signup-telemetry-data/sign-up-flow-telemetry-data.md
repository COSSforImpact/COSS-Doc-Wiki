---
icon: elementor
---

# Sign Up flow telemetry data

**Use cases for signup flow :**\
**1.when signup form is loading**

![](../../../../../.gitbook/assets/grey\_arrow\_down.png)when signup form is loading

```
 {
      "eid": "START",
      "ets": 1589873004306,
      "ver": "3.0",
      "mid": "START:cd239af7f09bbf692b93e0bcd88a1dbf",
      "actor": {
        "id": "db707c34785f86f30979eef0993e5991",
        "type": "User"
      },
      "context": {
        "channel": "505c7c48ac6dc1edc9b08f21db5a571d",
        "pdata": {
          "id": "prod.diksha.portal",
          "ver": "2.8.12",
          "pid": "sunbird-portal"
        },
        "env": "signup",
        "sid": "7a33c191-8086-e016-72a1-d82fac1ad545",
        "did": "db707c34785f86f30979eef0993e5991",
        "cdata": [
          
        ],
        "rollup": {
          "l1": "505c7c48ac6dc1edc9b08f21db5a571d"
        }
      },
      "object": {
        
      },
      "tags": [
        "505c7c48ac6dc1edc9b08f21db5a571d"
      ],
      "edata": {
        "type": "view",
        "pageid": "signup",
        "mode": "self",
        "uaspec": {
          "agent": "Chrome",
          "ver": "79.0.3945.130",
          "system": "unknown",
          "platform": "Linux",
          "raw": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.130 Safari/537.36"
        },
        "duration": 1589873004.436
      }
    }
```

**2. Impression event for sign up page load**

![](../../../../../.gitbook/assets/grey\_arrow\_down.png)Impression event for sign up page load

```
{
      "eid": "IMPRESSION",
      "ets": 1589873004351,
      "ver": "3.0",
      "mid": "IMPRESSION:c3e106b4506ab38789f9ca2681a31cd1",
      "actor": {
        "id": "db707c34785f86f30979eef0993e5991",
        "type": "User"
      },
      "context": {
        "channel": "505c7c48ac6dc1edc9b08f21db5a571d",
        "pdata": {
          "id": "prod.diksha.portal",
          "ver": "2.8.12",
          "pid": "sunbird-portal"
        },
        "env": "signup",
        "sid": "7a33c191-8086-e016-72a1-d82fac1ad545",
        "did": "db707c34785f86f30979eef0993e5991",
        "cdata": [
          {
            "type": "signup",
            "id": "639363e3-de50-5edb-5e2c-bf68ce10a457"
          }
        ],
        "rollup": {
          "l1": "505c7c48ac6dc1edc9b08f21db5a571d"
        }
      },
      "object": {
        
      },
      "tags": [
        "505c7c48ac6dc1edc9b08f21db5a571d"
      ],
      "edata": {
        "type": "view",
        "pageid": "signup",
        "uri": "/signup",
        "duration": 0.44
      }
    }
```

**3. Fetching of terms and conditions log event .**

![](../../../../../.gitbook/assets/grey\_arrow\_down.png)If successfully fetched TNC data.

```
 {
      "eid": "LOG",
      "ets": 1589873004377,
      "ver": "3.0",
      "mid": "LOG:98831c8fc68acdc2d96ab87044435d3a",
      "actor": {
        "id": "db707c34785f86f30979eef0993e5991",
        "type": "User"
      },
      "context": {
        "channel": "505c7c48ac6dc1edc9b08f21db5a571d",
        "pdata": {
          "id": "prod.diksha.portal",
          "ver": "2.8.12",
          "pid": "sunbird-portal"
        },
        "env": "self-signup",
        "sid": "7a33c191-8086-e016-72a1-d82fac1ad545",
        "did": "db707c34785f86f30979eef0993e5991",
        "cdata": [
          
        ],
        "rollup": {
          "l1": "505c7c48ac6dc1edc9b08f21db5a571d"
        }
      },
      "object": {
        
      },
      "tags": [
        "505c7c48ac6dc1edc9b08f21db5a571d"
      ],
      "edata": {
        "type": "fetch-terms-condition",
        "level": "SUCCESS",
        "message": "fetch-terms-condition success"
      }
    },
```

![](../../../../../.gitbook/assets/grey\_arrow\_down.png)Error in fetching term and condition data

```
    {
      "eid": "LOG",
      "ets": 1589873004377,
      "ver": "3.0",
      "mid": "LOG:98831c8fc68acdc2d96ab87044435d3a",
      "actor": {
        "id": "db707c34785f86f30979eef0993e5991",
        "type": "User"
      },
      "context": {
        "channel": "505c7c48ac6dc1edc9b08f21db5a571d",
        "pdata": {
          "id": "prod.diksha.portal",
          "ver": "2.8.12",
          "pid": "sunbird-portal"
        },
        "env": "self-signup",
        "sid": "7a33c191-8086-e016-72a1-d82fac1ad545",
        "did": "db707c34785f86f30979eef0993e5991",
        "cdata": [
          
        ],
        "rollup": {
          "l1": "505c7c48ac6dc1edc9b08f21db5a571d"
        }
      },
      "object": {
        
      },
      "tags": [
        "505c7c48ac6dc1edc9b08f21db5a571d"
      ],
      "edata": {
        "type": "fetch-terms-condition",
        "level": "ERROR",
        "message": "fetch-terms-condition failed"
      }
    },
```

**4. User Selects terms and condition check box-**

![](../../../../../.gitbook/assets/grey\_arrow\_down.png) If user selects terms and condition check box

```
    {
      "eid": "INTERACT",
      "ets": 1589873019509,
      "ver": "3.0",
      "mid": "INTERACT:e441999f571e12943227883f8379e115",
      "actor": {
        "id": "db707c34785f86f30979eef0993e5991",
        "type": "User"
      },
      "context": {
        "channel": "505c7c48ac6dc1edc9b08f21db5a571d",
        "pdata": {
          "id": "prod.diksha.portal",
          "ver": "2.8.12",
          "pid": "sunbird-portal"
        },
        "env": "self-signup",
        "sid": "7a33c191-8086-e016-72a1-d82fac1ad545",
        "did": "db707c34785f86f30979eef0993e5991",
        "cdata": [
          {
            "id": "user:tnc:accept",
            "type": "Feature"
          },
          {
            "id": "SB-16663",
            "type": "Task"
          }
        ],
        "rollup": {
          "l1": "505c7c48ac6dc1edc9b08f21db5a571d"
        }
      },
      "object": {
        
      },
      "tags": [
        "505c7c48ac6dc1edc9b08f21db5a571d"
      ],
      "edata": {
        "id": "user:tnc:accept",
        "type": "click",
        "subtype": "selected",
        "pageid": "self-signup"
      }
    },
```

![](../../../../../.gitbook/assets/grey\_arrow\_down.png)If user has not selects terms and condition check box.

```
{
      "eid": "INTERACT",
      "ets": 1589873019509,
      "ver": "3.0",
      "mid": "INTERACT:e441999f571e12943227883f8379e115",
      "actor": {
        "id": "db707c34785f86f30979eef0993e5991",
        "type": "User"
      },
      "context": {
        "channel": "505c7c48ac6dc1edc9b08f21db5a571d",
        "pdata": {
          "id": "prod.diksha.portal",
          "ver": "2.8.12",
          "pid": "sunbird-portal"
        },
        "env": "self-signup",
        "sid": "7a33c191-8086-e016-72a1-d82fac1ad545",
        "did": "db707c34785f86f30979eef0993e5991",
        "cdata": [
          {
            "id": "user:tnc:accept",
            "type": "Feature"
          },
          {
            "id": "SB-16663",
            "type": "Task"
          }
        ],
        "rollup": {
          "l1": "505c7c48ac6dc1edc9b08f21db5a571d"
        }
      },
      "object": {
        
      },
      "tags": [
        "505c7c48ac6dc1edc9b08f21db5a571d"
      ],
      "edata": {
        "id": "user:tnc:accept",
        "type": "click",
        "subtype": "unselected",
        "pageid": "self-signup"
      }
    }
```

**5. User clicks on register button**

![](../../../../../.gitbook/assets/grey\_arrow\_down.png) User clicks on register button interact event

```
 {
      "eid": "INTERACT",
      "ets": 1589873024419,
      "ver": "3.0",
      "mid": "INTERACT:78f4edc9ed9cb58c65cb4e22311ef95c",
      "actor": {
        "id": "db707c34785f86f30979eef0993e5991",
        "type": "User"
      },
      "context": {
        "channel": "505c7c48ac6dc1edc9b08f21db5a571d",
        "pdata": {
          "id": "prod.diksha.portal",
          "ver": "2.8.12",
          "pid": "sunbird-portal"
        },
        "env": "signup",
        "sid": "7a33c191-8086-e016-72a1-d82fac1ad545",
        "did": "db707c34785f86f30979eef0993e5991",
        "cdata": [
          {
            "type": "signup",
            "id": "639363e3-de50-5edb-5e2c-bf68ce10a457"
          }
        ],
        "rollup": {
          "l1": "505c7c48ac6dc1edc9b08f21db5a571d"
        }
      },
      "object": {
        
      },
      "tags": [
        "505c7c48ac6dc1edc9b08f21db5a571d"
      ],
      "edata": {
        "id": "submit-signup",
        "type": "click",
        "pageid": "signup",
        "extra": {
          "contactType": "email"
        }
      }
    },
```

**6. User clicks on submit otp button**

![](../../../../../.gitbook/assets/grey\_arrow\_down.png)User clicks on submit otp button interact event

```
{
      "eid": "INTERACT",
      "ets": 1589873035386,
      "ver": "3.0",
      "mid": "INTERACT:571cf5b83dfbc2e10950d5693d34ac95",
      "actor": {
        "id": "db707c34785f86f30979eef0993e5991",
        "type": "User"
      },
      "context": {
        "channel": "505c7c48ac6dc1edc9b08f21db5a571d",
        "pdata": {
          "id": "prod.diksha.portal",
          "ver": "2.8.12",
          "pid": "sunbird-portal"
        },
        "env": "signup",
        "sid": "7a33c191-8086-e016-72a1-d82fac1ad545",
        "did": "db707c34785f86f30979eef0993e5991",
        "cdata": [
          {
            "type": "otp",
            "id": "639363e3-de50-5edb-5e2c-bf68ce10a457"
          }
        ],
        "rollup": {
          "l1": "505c7c48ac6dc1edc9b08f21db5a571d"
        }
      },
      "object": {
        
      },
      "tags": [
        "505c7c48ac6dc1edc9b08f21db5a571d"
      ],
      "edata": {
        "id": "submit-otp",
        "type": "click",
        "pageid": "otp",
        "extra": {
          "values": "/sign-up"
        }
      }
    },
```

**7.Invalid otp entered error**

![](../../../../../.gitbook/assets/grey\_arrow\_down.png)Invalid otp entered error interact event

```
{
      "eid": "INTERACT",
      "ets": 1589873035506,
      "ver": "3.0",
      "mid": "INTERACT:2b1af9055bbaf82658f25fabfa3eee0c",
      "actor": {
        "id": "db707c34785f86f30979eef0993e5991",
        "type": "User"
      },
      "context": {
        "channel": "505c7c48ac6dc1edc9b08f21db5a571d",
        "pdata": {
          "id": "prod.diksha.portal",
          "ver": "2.8.12",
          "pid": "sunbird-portal"
        },
        "env": "signup",
        "sid": "7a33c191-8086-e016-72a1-d82fac1ad545",
        "did": "db707c34785f86f30979eef0993e5991",
        "cdata": [
          {
            "type": "otp",
            "id": "639363e3-de50-5edb-5e2c-bf68ce10a457"
          }
        ],
        "rollup": {
          "l1": "505c7c48ac6dc1edc9b08f21db5a571d"
        }
      },
      "object": {
        
      },
      "tags": [
        "505c7c48ac6dc1edc9b08f21db5a571d"
      ],
      "edata": {
        "id": "invalid-otp-error",
        "type": "click",
        "pageid": "otp",
        "extra": {
          "isError": "true"
        }
      }
    }
```

**8.Create user Flow**

![](../../../../../.gitbook/assets/grey\_arrow\_down.png)If create user API success Log event

```
{
      "eid": "LOG",
      "ets": 1589875003461,
      "ver": "3.0",
      "mid": "LOG:18a009ff521ecfda52209cff4be38fed",
      "actor": {
        "id": "db707c34785f86f30979eef0993e5991",
        "type": "User"
      },
      "context": {
        "channel": "505c7c48ac6dc1edc9b08f21db5a571d",
        "pdata": {
          "id": "prod.diksha.portal",
          "ver": "2.8.12",
          "pid": "sunbird-portal"
        },
        "env": "self-signup",
        "sid": "abd0af50-6a4a-decf-901f-fc07290cbee4",
        "did": "db707c34785f86f30979eef0993e5991",
        "cdata": [
          
        ],
        "rollup": {
          "l1": "505c7c48ac6dc1edc9b08f21db5a571d"
        }
      },
      "object": {
        
      },
      "tags": [
        "505c7c48ac6dc1edc9b08f21db5a571d"
      ],
      "edata": {
        "type": "sign-up",
        "level": "SUCCESS",
        "message": "sign-up success"
      }
    },
```

![](../../../../../.gitbook/assets/grey\_arrow\_down.png)If create user API fails

```
{
      "eid": "LOG",
      "ets": 1589875003461,
      "ver": "3.0",
      "mid": "LOG:18a009ff521ecfda52209cff4be38fed",
      "actor": {
        "id": "db707c34785f86f30979eef0993e5991",
        "type": "User"
      },
      "context": {
        "channel": "505c7c48ac6dc1edc9b08f21db5a571d",
        "pdata": {
          "id": "prod.diksha.portal",
          "ver": "2.8.12",
          "pid": "sunbird-portal"
        },
        "env": "self-signup",
        "sid": "abd0af50-6a4a-decf-901f-fc07290cbee4",
        "did": "db707c34785f86f30979eef0993e5991",
        "cdata": [
          
        ],
        "rollup": {
          "l1": "505c7c48ac6dc1edc9b08f21db5a571d"
        }
      },
      "object": {
        
      },
      "tags": [
        "505c7c48ac6dc1edc9b08f21db5a571d"
      ],
      "edata": {
        "type": "sign-up",
        "level": "ERROR",
        "message": "sign-up failed"
      }
    },
```

**9. Accept TNC success**

![](../../../../../.gitbook/assets/grey\_arrow\_down.png)Accept TNC success

```
  {
      "eid": "LOG",
      "ets": 1589875006685,
      "ver": "3.0",
      "mid": "LOG:3e16cff169b3227ec4c53456a2c9d933",
      "actor": {
        "id": "db707c34785f86f30979eef0993e5991",
        "type": "User"
      },
      "context": {
        "channel": "505c7c48ac6dc1edc9b08f21db5a571d",
        "pdata": {
          "id": "prod.diksha.portal",
          "ver": "2.8.12",
          "pid": "sunbird-portal"
        },
        "env": "self-signup",
        "sid": "abd0af50-6a4a-decf-901f-fc07290cbee4",
        "did": "db707c34785f86f30979eef0993e5991",
        "cdata": [
          
        ],
        "rollup": {
          "l1": "505c7c48ac6dc1edc9b08f21db5a571d"
        }
      },
      "object": {
        
      },
      "tags": [
        "505c7c48ac6dc1edc9b08f21db5a571d"
      ],
      "edata": {
        "type": "accept-tnc",
        "level": "SUCCESS",
        "message": "accept-tnc success"
      }
    },
```

**10. Accept TNC API error**

![](../../../../../.gitbook/assets/grey\_arrow\_down.png)Accept TNC API error

```
  {
      "eid": "LOG",
      "ets": 1589875006685,
      "ver": "3.0",
      "mid": "LOG:3e16cff169b3227ec4c53456a2c9d933",
      "actor": {
        "id": "db707c34785f86f30979eef0993e5991",
        "type": "User"
      },
      "context": {
        "channel": "505c7c48ac6dc1edc9b08f21db5a571d",
        "pdata": {
          "id": "prod.diksha.portal",
          "ver": "2.8.12",
          "pid": "sunbird-portal"
        },
        "env": "self-signup",
        "sid": "abd0af50-6a4a-decf-901f-fc07290cbee4",
        "did": "db707c34785f86f30979eef0993e5991",
        "cdata": [
          
        ],
        "rollup": {
          "l1": "505c7c48ac6dc1edc9b08f21db5a571d"
        }
      },
      "object": {
        
      },
      "tags": [
        "505c7c48ac6dc1edc9b08f21db5a571d"
      ],
      "edata": {
        "type": "accept-tnc",
        "level": "ERRORED",
        "message": "accept-tnc failed"
      }
    },
```
