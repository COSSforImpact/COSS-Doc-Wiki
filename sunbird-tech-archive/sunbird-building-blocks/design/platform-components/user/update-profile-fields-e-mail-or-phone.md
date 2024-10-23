---
icon: elementor
---

# Update Profile fields - E-Mail or Phone

### **Overview** <a href="#updateprofilefields-e-mailorphone-overview" id="updateprofilefields-e-mailorphone-overview"></a>

Currently user is not allowed to update e-mail or phone details from profile page. This design talks about, how user can change his existing e-mail or phone number.

### **Solution** <a href="#updateprofilefields-e-mailorphone-solution" id="updateprofilefields-e-mailorphone-solution"></a>

* Once user is logged in he will be able to see the edit button against e-mail or phone.
* Once clicked user will be redirected to screen to enter new e-mail or phone and verify the data.
* Here user will enter and click generate OTP, on which user will be redirected to enter OTP form.
* User will enter OTP and click verify
* On successful verification user data will be updated through update User API
* If verification fails, user will be redirected to profile page, without changing the data.

### **Other points to consider** <a href="#updateprofilefields-e-mailorphone-otherpointstoconsider" id="updateprofilefields-e-mailorphone-otherpointstoconsider"></a>

* Data will only be updated on successful OTP verification.
* OTP will expire as per configuration done (which is currently applicable to user sign-up)
* OTP throttling will be as per configuration done (which is currently applicable to user sign-up)
* No new API needs to be developed to support this feature.

## **Usage of existing API** <a href="#updateprofilefields-e-mailorphone-usageofexistingapi" id="updateprofilefields-e-mailorphone-usageofexistingapi"></a>

* **POST /v1/otp/generate -** will be called when user is on modify e-mail/phone page.
* **POST /v1/otp/verify -** will be called when user is on screen to verify e-mail/phone update.
* **PATCH /v1/user/update** - will be called for finally updating the user once verification is done.
