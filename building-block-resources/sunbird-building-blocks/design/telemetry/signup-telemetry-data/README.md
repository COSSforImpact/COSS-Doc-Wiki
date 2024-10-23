---
icon: folder-open
---

# Signup Telemetry data

### Background <a href="#signuptelemetrydata-background" id="signuptelemetrydata-background"></a>

For Signup and google signin flow telemetry events need to be generated and this documentation consists all the telemetry events for signup and google sigin flow.

Assumptions :&#x20;

1. As all the below telemetry events are pre login events ,actor is not specified in the events and values of actor will be of below object value\
   actor: {\
   "id": "anonymous",\
   "type": "User"\
   }
2. sid , did inside context will be same in all the events so they haven't mentioned in the all the events.

#### **Proposed Solution**  **Use cases for signup flow :**  **1.when user clicks on signup button once it is landed to signup form** <a href="#signuptelemetrydata-proposedsolutionusecasesforsignupflow-1.whenuserclicksonsignupbuttononceitisland" id="signuptelemetrydata-proposedsolutionusecasesforsignupflow-1.whenuserclicksonsignupbuttononceitisland"></a>

\


start event : Sample example

```
{
  "eid": "START",
  "context": {
    "channel": "b00bc992ef25f1a9a8d63291e20efc8d",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.13.0",
      "pid": "sunbird-portal"
    },
    "env": "signup",
    "cdata": [ {"type": "signup", "id": "<uuid>" }],
  },
  "edata": {
    "type":"signup",
    "uaspec":UASPEC,
    "pageid":"signup",
    "mode":"self"
  }
}
```

\


#### **2. After landing on signup form in portal**   <a href="#signuptelemetrydata-2.afterlandingonsignupforminportal" id="signuptelemetrydata-2.afterlandingonsignupforminportal"></a>

Impression event : sample example

```
{
  "eid": "IMPRESSION",
  "context": {
    "channel": "0123166367624478721",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.13.0",
      "pid": "sunbird-portal"
    },
    "env": "signup",
    "cdata": [
      {
        "type": "signup",
        "id": "<uuid>"
      }
    ]
  },
  "edata": {
    "type": "view",
    "pageid": "signup",
    "uri": "/signup"
  }
}
```

#### 3. on click of signup button in the form   <a href="#signuptelemetrydata-3.onclickofsignupbuttonintheform" id="signuptelemetrydata-3.onclickofsignupbuttonintheform"></a>

interact event : sample example

```
{
  "eid": "INTERACT",
  "ver": "3.0",
  "context": {
    "channel": "b00bc992ef25f1a9a8d63291e20efc8d",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.13.0",
      "pid": "sunbird-portal"
    },
    "env": "signup",
    "cdata": [ {"type": "signup", "id": "<uuid>" }]
  },
  "edata": {
    "id": "submit-signup",
    "type": "click",
    "pageid": "signup",
	"extra": {
      "contactType":"<radio option selected value (email / phone)>"
    }
  }
}
```

#### 4. After landing to otp page on clicking of signup submit <a href="#signuptelemetrydata-4.afterlandingtootppageonclickingofsignupsubmit" id="signuptelemetrydata-4.afterlandingtootppageonclickingofsignupsubmit"></a>

\


impression event : sample example

```
{
  "eid": "IMPRESSION",
  "context": {
    "channel": "0123166367624478721",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.13.0",
      "pid": "sunbird-portal"
    },
    "env": "signup",
    "cdata": [ {"type": "signup", "id": "<uuid>" }],
  },
  "edata": {
    "type": "view",
    "pageid": "otp",
    "uri": "/sign-up"
  }
}
```

\


#### 5. On clicking of submit otp in otp page <a href="#signuptelemetrydata-5.onclickingofsubmitotpinotppage" id="signuptelemetrydata-5.onclickingofsubmitotpinotppage"></a>

\


Interact event : sample example

```
{
  "eid": "INTERACT",
  "ver": "3.0",
  "context": {
    "channel": "b00bc992ef25f1a9a8d63291e20efc8d",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.13.0",
      "pid": "sunbird-portal"
    },
    "env": "signup",
    "cdata": [ {"type": "otp", "id": "<uuid>" }]
  },
  "edata": {
    "id": "submit-otp",
    "type": "click",
    "pageid": "otp",
    "extra": {
      "values":"/sign-up"
    }
  }
}
```

\


#### 6. On clicking of resend otp in otp page <a href="#signuptelemetrydata-6.onclickingofresendotpinotppage" id="signuptelemetrydata-6.onclickingofresendotpinotppage"></a>

\


interact event : sample example

```
{
  "eid": "INTERACT",
  "ver": "3.0",
  "context": {
    "channel": "b00bc992ef25f1a9a8d63291e20efc8d",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.13.0",
      "pid": "sunbird-portal"
    },
    "env": "signup",
    "cdata": [ {"type": "otp", "id": "<uuid>" }]
  },
  "edata": {
    "id": "resend-otp",
    "type": "click",
    "pageid": "otp",
  }
}
```

#### 7. on send otp fail after clicking on signup submit form <a href="#signuptelemetrydata-7.onsendotpfailafterclickingonsignupsubmitform" id="signuptelemetrydata-7.onsendotpfailafterclickingonsignupsubmitform"></a>

\


Interact Event : sample example

```
{
  "eid": "INTERACT",
  "context": {
    "channel": "b00bc992ef25f1a9a8d63291e20efc8d",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.13.0",
      "pid": "sunbird-portal"
    },
    "env": "otp",
    "cdata": [ {"type": "otp", "id": "<uuid>" }],
  },
  "edata": {
  	  "pageid": "otp",
	  "type": "click",
	  "id": "send-otp",
	  "extra": {
	    "isError":"true"
	  }	
  }
}
```

#### 8. on resend otp api error  <a href="#signuptelemetrydata-8.onresendotpapierror" id="signuptelemetrydata-8.onresendotpapierror"></a>

\


Interact Event : sample example

```
{
  "eid": "INTERACT",
  "context": {
    "channel": "b00bc992ef25f1a9a8d63291e20efc8d",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.13.0",
      "pid": "sunbird-portal"
    },
    "env": "otp",
    "cdata": [ {"type": "otp", "id": "<uuid>" }],
  },
  "edata": {
  	  "pageid": "otp",
	  "type": "click",
	  "id": "resend-otp",
	  "extra": {
	    "isError":"true"
	  }	
  }
}
```

\


#### **9. End event for : Signup submit api error / Error of submit otp (on api failure, not on invalid otp) / success of submit otp in signup flow** <a href="#signuptelemetrydata-9.endeventfor-signupsubmitapierror-errorofsubmitotp-onapifailure-notoninvalidotp" id="signuptelemetrydata-9.endeventfor-signupsubmitapierror-errorofsubmitotp-onapifailure-notoninvalidotp"></a>

\


End event : sample example

```
{
  "eid": "END",
  "context": {
    "channel": "b00bc992ef25f1a9a8d63291e20efc8d",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.13.0",
      "pid": "sunbird-portal"
    },
    "env": "signup",
    "cdata": [ {"type": "signup", "id": "<uuid>" }],
  },
  "edata": {
    "type":"signup",
    "pageid": "signup",
    "mode": "self"
  }
}
```

\


### **Log events for signup flow :**  <a href="#signuptelemetrydata-logeventsforsignupflow" id="signuptelemetrydata-logeventsforsignupflow"></a>

\


#### 1. On google invisble captcha suspicious event on signup submit <a href="#signuptelemetrydata-1.ongoogleinvisblecaptchasuspiciouseventonsignupsubmit" id="signuptelemetrydata-1.ongoogleinvisblecaptchasuspiciouseventonsignupsubmit"></a>

Log Event : sample example

```
{
  "eid": "LOG",
  "context": {
    "channel": "b00bc992ef25f1a9a8d63291e20efc8d",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.13.0",
      "pid": "sunbird-portal"
    },
    "env": "signup",
    "cdata": [ {"type": "signup", "id": "<uuid>" }],
  },
  "edata": {
  	  "pageid": "signup",
	  "type": "api_access", 
	  "level": "ERROR", 
	  "message": "google captcha found suspicious"
  }
}
```

#### 2. on otp verification fail after user has submitted otp <a href="#signuptelemetrydata-2.onotpverificationfailafteruserhassubmittedotp" id="signuptelemetrydata-2.onotpverificationfailafteruserhassubmittedotp"></a>

\


Log Event : sample example

```
{
  "eid": "LOG",
  "context": {
    "channel": "b00bc992ef25f1a9a8d63291e20efc8d",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.13.0",
      "pid": "sunbird-portal"
    },
    "env": "otp",
    "cdata": [ {"type": "otp", "id": "<uuid>" }],
  },
  "edata": {
  	  "pageid": "otp",
	  "type": "api_call", 
	  "level": "ERROR", 
	  "message": "otp verification failed"
  }
}
```

#### 3. create user error after otp verified in signup flow <a href="#signuptelemetrydata-3.createusererrorafterotpverifiedinsignupflow" id="signuptelemetrydata-3.createusererrorafterotpverifiedinsignupflow"></a>

\


Log Event : sample example

```
{
  "eid": "LOG",
  "context": {
    "channel": "b00bc992ef25f1a9a8d63291e20efc8d",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.13.0",
      "pid": "sunbird-portal"
    },
    "env": "otp",
    "cdata": [ {"type": "signup", "id": "<uuid>" }],
  },
  "edata": {
  	  "pageid": "signup",
	  "type": "api_call", 
	  "level": "ERROR", 
	  "message": "user creation failed"
  }
}
```

#### **Google signIn flow** <a href="#signuptelemetrydata-googlesigninflow" id="signuptelemetrydata-googlesigninflow"></a>

#### &#x20;1.after landing to google page on click of signin with google from keycloak page  (is this really needed ?, as all the google signin flow events are been done in backend, and frontend have only google redirect pages)   <a href="#signuptelemetrydata-1.afterlandingtogooglepageonclickofsigninwithgooglefromkeycloakpage-isthisreally" id="signuptelemetrydata-1.afterlandingtogooglepageonclickofsigninwithgooglefromkeycloakpage-isthisreally"></a>

Start event : sample example

```
{
  "eid": "START",
  "context": {
    "channel": "b00bc992ef25f1a9a8d63291e20efc8d",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.13.0",
      "pid": "sunbird-portal"
    },
    "env": "signin",
    "cdata": [ {"type": "signin", "id": "<uuid>" }],
  },
  "edata": {
    "type": "signup",
    "pageid": "signin",
    "uaspec": UASPEC,
	"mode":"google"
  }
}
```

#### 2. After landing to google page after clicking of signin with google from keycloak page (this is a google page, impression can be created from backend when google gives the redirect url) <a href="#signuptelemetrydata-2.afterlandingtogooglepageafterclickingofsigninwithgooglefromkeycloakpage-thisis" id="signuptelemetrydata-2.afterlandingtogooglepageafterclickingofsigninwithgooglefromkeycloakpage-thisis"></a>

\


Impression event : sample example

```
{
  "eid": "IMPRESSION",
  "context": {
    "channel": "0123166367624478721",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.13.0",
      "pid": "sunbird-portal"
    },
    "env": "otp",
    "cdata": [ {"type": "signin", "id": "<uuid>" }],
  },
  "edata": {
    "type": "view",
    "pageid": "signin",
    "uri": "/google/auth"
  }
}
```

#### &#x20;3. After user action done on google sigin approved and google has given user details or denied <a href="#signuptelemetrydata-3.afteruseractiondoneongooglesiginapprovedandgooglehasgivenuserdetailsordenied" id="signuptelemetrydata-3.afteruseractiondoneongooglesiginapprovedandgooglehasgivenuserdetailsordenied"></a>

\


End event : sample example

```
{
  "eid": "END",
  "context": {
    "channel": "b00bc992ef25f1a9a8d63291e20efc8d",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.13.0",
      "pid": "sunbird-portal"
    },
    "env": "sigin",
    "cdata": [ {"type": "sigin", "id": "<uuid>" }],
  },
  "edata": {
    "type": "signin",
    "subtype": "google_signin",
    "pageid": "sigin",
    "mode":"google"
  }
}
```

\


### **Log events of google signIn** <a href="#signuptelemetrydata-logeventsofgooglesignin" id="signuptelemetrydata-logeventsofgooglesignin"></a>

\


#### **1. on success full response of user details from google sigin**  <a href="#signuptelemetrydata-1.onsuccessfullresponseofuserdetailsfromgooglesigin" id="signuptelemetrydata-1.onsuccessfullresponseofuserdetailsfromgooglesigin"></a>

Log Event : sample example

```
{
  "eid": "LOG",
  "context": {
    "channel": "b00bc992ef25f1a9a8d63291e20efc8d",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.13.0",
      "pid": "sunbird-portal"
    },
    "env": "signin",
    "cdata": [ {"type": "signin", "id": "<uuid>" }],
  },
  "edata": {
  	  "pageid": "signin",
	  "type": "api_access", 
	  "level": "INFO", 
	  "message": "successfull recieved user details from google"
  }
}
```

#### **2. on api error of google sigin to get redirect url** <a href="#signuptelemetrydata-2.onapierrorofgooglesigintogetredirecturl" id="signuptelemetrydata-2.onapierrorofgooglesigintogetredirecturl"></a>

Log Event : sample example

```
{
  "eid": "LOG",
  "context": {
    "channel": "b00bc992ef25f1a9a8d63291e20efc8d",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.13.0",
      "pid": "sunbird-portal"
    },
    "env": "signin",
    "cdata": [ {"type": "signin", "id": "<uuid>" }],
  },
  "edata": {
  	  "pageid": "signin",
	  "type": "api_access", 
	  "level": "ERROR", 
	  "message": "unable to get redirect url from google after user clicked on google signin button"
  }
}
```

#### **3. on api error of google sigin to get user details from token** <a href="#signuptelemetrydata-3.onapierrorofgooglesigintogetuserdetailsfromtoken" id="signuptelemetrydata-3.onapierrorofgooglesigintogetuserdetailsfromtoken"></a>

Log Event : sample example

```
{
  "eid": "LOG",
  "context": {
    "channel": "b00bc992ef25f1a9a8d63291e20efc8d",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.13.0",
      "pid": "sunbird-portal"
    },
    "env": "signin",
    "cdata": [ {"type": "signin", "id": "<uuid>" }],
  },
  "edata": {
  	  "pageid": "signin",
	  "type": "api_access", 
	  "level": "ERROR", 
	  "message": "unable to get user details from auth token or <error response from google can be dumped here>"
  }
}
```

#### **4. google signIn user already exists event** <a href="#signuptelemetrydata-4.googlesigninuseralreadyexistsevent" id="signuptelemetrydata-4.googlesigninuseralreadyexistsevent"></a>

Log Event: sample example

```
{
  "eid": "LOG",
  "context": {
    "channel": "b00bc992ef25f1a9a8d63291e20efc8d",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.13.0",
      "pid": "sunbird-portal"
    },
    "env": "signin",
    "cdata": [ {"type": "signin", "id": "<uuid>" }],
  },
  "edata": {
  	  "pageid": "signin",
	  "type": "process", 
	  "level": "INFO", 
	  "message": "user exists"
  }
}
```

#### **5. google sigin user not exists event**  <a href="#signuptelemetrydata-5.googlesiginusernotexistsevent" id="signuptelemetrydata-5.googlesiginusernotexistsevent"></a>

\


Log Event : Sample example

```
{
  "eid": "LOG",
  "context": {
    "channel": "b00bc992ef25f1a9a8d63291e20efc8d",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.13.0",
      "pid": "sunbird-portal"
    },
    "env": "signin",
    "cdata": [ {"type": "signin", "id": "<uuid>" }],
  },
  "edata": {
  	  "pageid": "signin",
	  "type": "process", 
	  "level": "INFO", 
	  "message": "user not exists"
  }
}

```

\


#### 6. create user error during signup using google <a href="#signuptelemetrydata-6.createusererrorduringsignupusinggoogle" id="signuptelemetrydata-6.createusererrorduringsignupusinggoogle"></a>

\


Log Event : sample example

```
{
  "eid": "LOG",
  "context": {
    "channel": "b00bc992ef25f1a9a8d63291e20efc8d",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.13.0",
      "pid": "sunbird-portal"
    },
    "env": "otp",
    "cdata": [ {"type": "signin", "id": "<uuid>" }],
  },
  "edata": {
  	  "pageid": "signin",
	  "type": "api_call", 
	  "level": "ERROR", 
	  "message": "user creation failed"
  }
}
```

### **Audit Events : (what should be the values for edata audit events)** <a href="#signuptelemetrydata-auditevents-whatshouldbethevaluesforedataauditevents" id="signuptelemetrydata-auditevents-whatshouldbethevaluesforedataauditevents"></a>

\


#### 1.after user is created from self signup :  <a href="#signuptelemetrydata-1.afteruseriscreatedfromselfsignup" id="signuptelemetrydata-1.afteruseriscreatedfromselfsignup"></a>

\


audit event : sample example

```
{
  "eid": "AUDIT",
  "context": {
    "channel": "b00bc992ef25f1a9a8d63291e20efc8d",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.13.0",
      "pid": "sunbird-portal"
    },
    "env": "signin",
    "cdata": [ {"type": "signup","id":"self"}],
  },
  "edata": {
	  "props": "",
	  "state": "", 
	  "prevstate": ""
  }
}
```

\


#### 2. After user is created from google login :  <a href="#signuptelemetrydata-2.afteruseriscreatedfromgooglelogin" id="signuptelemetrydata-2.afteruseriscreatedfromgooglelogin"></a>

\


audit event : sample example

```
{
  "eid": "AUDIT",
  "context": {
    "channel": "b00bc992ef25f1a9a8d63291e20efc8d",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.13.0",
      "pid": "sunbird-portal"
    },
    "env": "signin",
    "cdata": [ {"type": "signup","id":"google"}],
  },
  "edata": {
	  "props": "",
	  "state": "", 
	  "prevstate": ""
  }
}
```

\


\


\


\


\


\


\


\


\


\


\


\


\


\
