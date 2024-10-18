# Update user profile fields impact

**Overview**

As of now, we allow to update the user profile fields like e-mail and phone from update user API. But, as part of the sign-up implementation, users will be required to verify the data before being registered into the sunbird platform. So, current flow to allow updating through API is not valid in current format.&#x20;

\


**Approach 1:**

Disallow changing the phone & email from update user api.

\


| Pros                                                            | Cons                                                       |
| --------------------------------------------------------------- | ---------------------------------------------------------- |
| API behavior will become consistent as per current UI behavior  | There is no way left for user/admin to update this details |
| Easy to implement, just need to disallow updating this 2 fields | <p><br></p>                                                |

**Approach 2:**

Allow user to update profile fields through API, i.e. not handling or not changing anything in current API.

**Approach 3:**

Allow update of this fields, but mark the user unverified.

To be able to login next time, user need to go through the verification process and provide the OTP to login - where user will be marked verified.

| Pros                                       | Cons                                                      |
| ------------------------------------------ | --------------------------------------------------------- |
| User has ability to change profile details | Will require additional UI & API for verification process |
| <p><br></p>                                | <p><br></p>                                               |

**Steps:**

* Update phone/email should be a seperate page & API
* When user tried to edit, he will be presented with confirm OTP screen.
* once he enters updateProfileField will be executed with changed number/email and relevant OTP for fields changed.
* Internally we will check and allow/disallow the operation based on OTP & number/email data passed through API.

\


**API**

**POST** /api/user/v1/update/profileFieldOtp

```
Request body:
{
  "request": {
    "oldEmail":"oldemail@gmail.com", //optional pair
    "newEmail": "someemail@gmail.com", 
    "oldPhone": "8888888888", //optional pair
    "newPhone": "9999999999" 
  }
}
```

**Validation**:

* if newEmail field present - oldEmail is mandatory
* if newPhone field present - oldPhone is mandatory
* Either of newEmail or newPhone is mandatory

**Responses**

**200 OK** - Otp generated successfully

**400 Bad Request**

* Request validation failures- if any
* Invalid old e-mail or old phone

**PATCH** /api/user/v1/update/profileField

```
{
  "request": {
    "email": "someemail@gmail.com", //optional pair
    "emailOtp": "2920",
    "phone": "9999999999" //optional pair
    "phoneOtp": "2921"
  }
}
```

**Validation**: if phone field present, phoneOtp is mandatory, if email present then emailOtp is mandatory. Atleast one of the phone/email field is mandatory

**Response**

**200 OK** - updated successfully

**400 Bad Request**

* Validation error
* Invalid Otp error
