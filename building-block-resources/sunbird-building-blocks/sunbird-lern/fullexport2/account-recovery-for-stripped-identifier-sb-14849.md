---
icon: elementor
---

# Account recovery for stripped identifier(SB-14849)

### [Problem statement:](https://project-sunbird.atlassian.net/wiki/spaces/UM/pages/1097924677/Account+recovery+for+stripped+identifier+SB-14849#Accountrecoveryforstrippedidentifier\(SB-14849\)-Problemstatement%3A)[Solution 1:](https://project-sunbird.atlassian.net/wiki/spaces/UM/pages/1097924677/Account+recovery+for+stripped+identifier+SB-14849#Accountrecoveryforstrippedidentifier\(SB-14849\)-Solution1%3A)[Solution 2:](https://project-sunbird.atlassian.net/wiki/spaces/UM/pages/1097924677/Account+recovery+for+stripped+identifier+SB-14849#Accountrecoveryforstrippedidentifier\(SB-14849\)-Solution2%3A)Background: <a href="#accountrecoveryforstrippedidentifier-sb-14849-background" id="accountrecoveryforstrippedidentifier-sb-14849-background"></a>

Current system allowing user to claim identifier (email/phone) by verifing OTP, and once it's successfully claimed , System will ask you to login with this identifer and password.Incase login success then you can continue with this account. Incase login failure then sytem will stripped out those identifier from original account and create new account for you.&#x20;

### Problem statement: <a href="#accountrecoveryforstrippedidentifier-sb-14849-problemstatement" id="accountrecoveryforstrippedidentifier-sb-14849-problemstatement"></a>

&#x20; User is using email or phone to login.If email and phone column itself stripped then they can't be able to login. Below is following two scenario.

&#x20; 1\. User account is associated with only email or phone and that identifier stripped out then how user get into system? User has valid recovery email or recovery phone (assumption)

&#x20; 2\. User accout was associated with email and phone and both identifier was stripped out then how user get into system? User has valid recovery email or recovery phone (assumption)

\


### Solution 1: <a href="#accountrecoveryforstrippedidentifier-sb-14849-solution1" id="accountrecoveryforstrippedidentifier-sb-14849-solution1"></a>

&#x20;During stripped identifier we can check if account having only one identifier and has recovery email or recovery phone then notifiy user to use their username for login and after login ask them to add at least one primary identifier.&#x20;

&#x20;To add at least one primary identifier protal changes required.So that for next login he can use that identifier.

### Solution 2: <a href="#accountrecoveryforstrippedidentifier-sb-14849-solution2" id="accountrecoveryforstrippedidentifier-sb-14849-solution2"></a>

&#x20;During forgot password workflow , if user is able to reset password successfully and user account won't have any primary identifier then show him username on screen to login.

\


Solution 1 is more preferable. Notification can sent to user either during identifier stripped or reset password success or both.

\
