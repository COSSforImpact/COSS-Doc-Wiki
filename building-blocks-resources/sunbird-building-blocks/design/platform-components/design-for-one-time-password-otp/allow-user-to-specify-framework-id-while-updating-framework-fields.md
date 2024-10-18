# Allow user to specify framework-id while updating framework fields

## **Overview** <a href="#allowusertospecifyframework-idwhileupdatingframeworkfields-overview" id="allowusertospecifyframework-idwhileupdatingframeworkfields-overview"></a>

Currently user is shown the framework fields, associated with root-org channel to which user belongs.

As part of the story, we want to allow the user to select the framework, and pass the framework fields accordingly.

## **Changes in existing API** <a href="#allowusertospecifyframework-idwhileupdatingframeworkfields-changesinexistingapi" id="allowusertospecifyframework-idwhileupdatingframeworkfields-changesinexistingapi"></a>

For updating the framework fields following will be the user call.

**POST** /v1/user/update

```
{
  "request": {
    "userId": "user-id",
    "framework": {
      "id": "framework-id",
      "medium": [
        "English"
      ],
      "board": [
        "NCERT"
      ],
      "gradeLevel": [
        "Class 3"
      ],
      "subject": [
        "English"
      ]
    }
  }
}
```

\


**Responses**:

**200 OK  -** if framework id is correct & framework field values are valid.

**401 Unauthorized -** If user is not logged

**400 Bad Request** -

* If framework id is not passed.
* If framework id is not valid.
* If any of the field value is not valid for the passed framework-id

## **Approach** <a href="#allowusertospecifyframework-idwhileupdatingframeworkfields-approach" id="allowusertospecifyframework-idwhileupdatingframeworkfields-approach"></a>

* If user does not pass framework id or passes invalid framework-id, we will throw error.
* We will check if we have the framework data cached for given framework id, else load and cache it.
* We will validate the framework fields against this cached data.
* If any of the field value is invalid the user will be shown the error accordingly.
