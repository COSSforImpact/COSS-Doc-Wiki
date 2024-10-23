---
icon: elementor
---

# Account Recovery workflow in Portal

### **Overview:** <a href="#accountrecoveryworkflowinportal-overview" id="accountrecoveryworkflowinportal-overview"></a>

Currently, Sunbird uses account recovery flow of Keycloak with minimal customization. Keycloak provides secure account recovery flow, that accepts primary account identifier(Phone or Email) to recovery account. If the user doesn't have access to his primary account identifier he can't reset his account with the secondary/recovery account identifier. To enhance this flow we are proposing to move the complete flow in the portal.

### **Problem statement:** <a href="#accountrecoveryworkflowinportal-problemstatement" id="accountrecoveryworkflowinportal-problemstatement"></a>

Account recovery workflow should be handled in portal securely and with proper state management.

### **Solutions:**  <a href="#accountrecoveryworkflowinportal-solutions" id="accountrecoveryworkflowinportal-solutions"></a>

Proposed [UI Design](https://projects.invisionapp.com/share/CDT3XPDB7SJ#/screens) and Workflow (attached below) for account recovery is 4 step process.&#x20;

\


&#x20;                                        &#x20;

**Step 1:** In the screen, the user will enter Phone/Email and UserName with which he has signed up in Sunbird. User can retry if the UserName doesn't match only one time. If he couldn't find his account after 2 failed attempts, then he should be redirected to the Login page with proper massage. If the user entered details yields matched accounts(can contain more than one identifier like phone, email, prev used phone, prev used email) user will be redirected to next step.

**Step 2:** Here user can choose to which contact channel he wants his OTP to be sent to. The list will contain all matched accounts contact channel(phone, email, prevEmail, prevPhone). OTP should be sent to contact channel that the user enters. If the OTP was successfully sent user will be redirected to the next step. If the user **refreshes the page,** then we need to redirect him to the first step.

**Step 3:** Here user can verify the OTP that has been sent to contact type of his choosing. If he fails to validate the account even after the second attempt he should be sent to the login page. If verification is successful, then the user will be redirected to the next step. If the user **refreshes the page,** then we need to redirect him to the first step.

**Step 4**: Here he can enter new password and confirm it to recover the account. If the password reset successful user will be redirected login page with succus message.  If the user **refreshes the page,** then we need to redirect him to the first step.

**Drawbacks:**&#x20;

1. No state information is maintained in URL or browser session, hence on **page refresh** user are redirected to the first page.
2. Reset password API is exposed as we are not maintaining any state in the portal backend. So anyone can call this API without verifying the contact type and hack others account.

\
