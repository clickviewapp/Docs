# Data required for creating a view key

_Please feel free to create an issue if you have any questions not answered by this documentation._

## Overview
This page outlines what data is expected when creating a view key as part of the [Video Playback](video-playback.md) workflow.

The `data` property on the create view key request will be used to pass user information to ClickView. Below is a generic outline of the expected properties, however the data being sent here will be an agreement between you and ClickView, additional properties outside of what is specified may be expected by ClickView. Similarly certain properties may be required that are listed as optional below.

### Schema

|Property Name|Required for teachers|Required for students|Description|
|---|---|---|---|
|`student`|Required|Required|A boolean value identifying if the user is a student.|
|`firstName`|Required|Must not be sent|The users first name.|
|`surname`|Required|Must not be sent|The users surname.|
|`email`|Required|Must not be sent|The user's email address.|
|`jobTitle`|Optional|n/a|The user's job title in their school or district.|
|`schoolName`|Optional|Optional|The name of the school the user belongs to.|
|`schoolId`|Optional|Optional|Any identifier you may have on hand for the school.|
|`districtName`|Optional|Optional|The name of the district the user belongs to.|
|`districtId`|Optional|Optional|Any identifier you may have on hand for the district.|

### Restrictions
If the `student` property is set to true, the view key creation will fail if the following properties are also specified.
- `firstName`
- `surname`
- `email`

This is done as a safeguard to ensure student PII is never being sent to ClickView.

### Example teacher payload
Here is an example of a create view key request payload with all the metadata populated.

```json
{
  "mediaId": "YOUR_MEDIA_ID",
  "data": {
    "student": false,
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

### Example student payload
Here is an example of a create view key request payload for a student.

```json
{
  "mediaId": "YOUR_MEDIA_ID",
  "data": {
    "isStudent": true,
    "schoolName": "Walkerville Elementary School",
    "schoolId": "S123",
    "districtName": "Riverside Unified School District",
    "districtId": "D123"
  }
}
```

## Best practices
- For `districtId` and `schoolId`, if you do not have universal identifiers on hand, ClickView would still appreciate any identifiers that are unique within your system, allowing us more reliable mapping as we process the data.
- Do not send `firstName`, `surname` or `email` for students.
- Ensure that you have reached an agreement with ClickView on how and what data will be sent. Each parnter will go through unique validation.

## Next Steps
Once you have created a view key you will need to use the reponse. Please see [View key response](video-playback.md#view-key-response) in the Video Playback workflow.