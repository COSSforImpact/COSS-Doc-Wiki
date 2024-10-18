# Improve logging quality

### **Jira Ticket:** [**SB-9772**](https://project-sunbird.atlassian.net/browse/SB-9772?src=confmacro) <a href="#improveloggingquality-jiraticket-systemjirakey-summary-type-created-updated-due-assignee-reporter-pr" id="improveloggingquality-jiraticket-systemjirakey-summary-type-created-updated-due-assignee-reporter-pr"></a>

### **Overview** <a href="#improveloggingquality-overview" id="improveloggingquality-overview"></a>

As part of the ticket we need to improve overall logging quality of sunbird platform.

Currently, we face problems in two particular areas:

* To change logging level, property file need to be changed, which means we need to build & deploy application for log level change to take effect. Due to this if we want to see finer log levels, we need to redeploy the application.
* There are cases where we either lack logging, log sensitive data, use wrong log levels.

\


**Problem statement 1:** We do not have ability to change log level at run-time.&#x20;

\


**Approach 1:** we can provide an api, which when triggered will set the logging level of application accordingly.

**Challenges:**

As we deploy multiple containers, behind the proxy server, load balancer will invok requests only on one of the containers.

\


**Approach 2:** We can read the default logging level from environment variable.

Though this need to be configured on all the containers, but this is consistent approach and will update the log level for all the containers.

We will store/retrieve the current log level from environment variable : SUNBIRD\_LOG\_LEVEL.\
Allowed values are :

Standard Level intLevel\
OFF 0\
FATAL 100\
ERROR 200\
WARN 300\
INFO 400\
DEBUG 500\
TRACE 600\
ALL Integer.MAX\_VALUE

When application starts, within GlobalSettings initialization, we will check existence of environment variable SUNBIRD\_LOG\_LEVEL - if it is configured, and valid, the value will be set to root logger level accordingly.\
\-> org.apache.logging.log4j.core.config.Configurator.setLevel() (function used to adjust log-level at run-time)

If environment variable is not configured, system will automatically use value configured in log4j2.properties (which is INFO currently)

For logging level change to take effect application restart will be required.

\


**Problem Statement 2:** Due to inappropriate logging we put sensitive data in logs or lack proper data to be able to debug.

**Solution**

As part of the ticket we need to identify all the areas where the logging of sensitive data is done and remove such data from logging, Logging to be removed includes

* Full http requests along with headers
* Printing full http requests by user
* User credentials

\


\
