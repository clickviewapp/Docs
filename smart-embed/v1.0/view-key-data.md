# Data required for creating a view key

_Please feel free to create an issue if you have any questions not answered by this documentation._

## Overview
This page outlines the data that is expected when creating a View Key as part of the [Video Playback](video-playback.md) workflow.

The `data` property on the create View Key request will be used to pass user information to ClickView. 

The table below shows some common properties the ClickView API expects, however the data being sent here will be determined by your own agreement with ClickView. Is most cases additional properties (outside of what is specified in the table) may be expected by ClickView. 

Similarly certain properties may be required that are listed as optional below.

### Schema

|Property Name|Required for teachers|Required for students|Description|
|---|---|---|---|
|`student`|Required|Required|A boolean value identifying if the user is a student.|
|`firstName`|Required|Must not be sent|The users first name.|
|`surname`|Required|Must not be sent|The users surname.|
|`email`|Required|Must not be sent|The user's email address.|
|`jobTitle`|Optional|n/a|The user's job title in their school or district.|
|`schoolName`|Required|Required|The name of the school the user belongs to.|
|`schoolId`|Required|Required|Your internal identifier for the school.|
|`districtName`|Required|Required|The name of the district the user belongs to.|
|`districtId`|Required|Required|Your internal identifier for the district.|
|`countryCode`|Required|n/a|The ISO 3166-1 Alpha-2 Codes for which country the user is from. We required this to adhere to data sovereignty laws.|

### Restrictions
If the `student` property is set to true, the View Key creation will fail if the following properties are also specified.
- `firstName`
- `surname`
- `email`

This is done as a safeguard to ensure student PII is never being sent to ClickView.

### Example teacher payload
Here is an example of a create View Key request payload with all the metadata populated.

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
    "districtId": "D123",
    "countryCode": "US"
  }
}
```

### Example student payload
Here is an example of a create View Key request payload for a student. You will notice we do not accept any PII for student requests.

```json
{
  "mediaId": "YOUR_MEDIA_ID",
  "data": {
    "student": true,
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
- Ensure that you have reached an agreement with ClickView on which data will be exchanged. The API will validate your payload inline on your agreement with ClickView.

## Next Steps
Once you have created a view key you will need to use the reponse. Please see [View key response](video-playback.md#3-view-key-response) in the Video Playback workflow.