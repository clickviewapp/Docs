# Additional data for creating a view key

_Please feel free to create an issue if you have any questions not answered by this documentation._

## Overview
This page outlines what data is expected when [creating and using a view key](view-key-creation.md);

The `additionalData` property on the create view key request will be used to pass user information to ClickView. Below is a generic outline of the expected properties, however the data being sent here will be an agreement between you and ClickView, additional properties outside of what is specified may be expected by ClickView. Similarly certain properties may be required that are listed as optional below.

### Schema

|Property Name|Required|Description|
|---|---|---|
|`isStudent`|Required|A boolean value identifying if the user is a student.|
|`firstName`|Required for teachers|The users first name. Must not be provided if `isStudent` is true.|
|`surname`|Required for teachers|The users surname. Must not be provided if `isStudent` is true.|
|`email`|Required for teachers|The user's email address. Must not be provided if `isStudent` is true.|
|`jobTitle`|Optional|The user's job title in their school or district.|
|`schoolName`|Optional|The name of the school the user belongs to.|
|`schoolId`|Optional|An identifier you may have on hand for the school.|
|`districtName`|Optional|The name of the district the user belongs to.|
|`districtId`|Optional|Any identifier you may have on hand for the district.|\

### Restrictions
If the `isStudent` property is set to true, the view key creation will fail if the following properties are also specified.
- `firstName`
- `surname`
- `email`

This is done as a safeguard to ensure student PII is never being sent to ClickView.

### Example teacher payload
Here is an example of a create view key request payload with all the metadata populated.

```json
{
  "mediaId": "YOUR_MEDIA_ID",
  "additionalData": {
    "isStudent": false,
    "firstName": "Valerie",
    "surname": "Frizzle",
    "email": "valerie.frizzle@school.gov",
    "jobTitle": "Bus driver",
    "schoolName": "Walkerville Elementary School",
    "schoolId": "S123",
    "districtName": "Riverside Unified School District",
    "districtId": "D123"
  }
}
```

## Example student payload
Here is an example of a create view key request payload for a student.

```json
{
  "mediaId": "YOUR_MEDIA_ID",
  "additionalData": {
    "isStudent": true,
    "schoolName": "Walkerville Elementary School",
    "schoolId": "S123",
    "districtName": "Riverside Unified School District",
    "districtId": "D123"
  }
}
```

