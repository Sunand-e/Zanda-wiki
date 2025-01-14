## Sign in

/api/v1/user/sign_in

POST

**Body:**

```json
{
  "email": "test@example.com",
  "password": "qwerty"
}
```

**Response:**

```json
{
  "user": {
    "id": "7029bd65-21eb-484b-a64d-4c6eda83ae53",
    "first_name": "Arun",
    "last_name": "Patil",
    "email": "test@example.com",
    "tenant_id": "f03f8411-53b7-437d-bf7b-c2fca2caece3",
    "created_at": "2023-01-09T11:07:42.828Z",
    "updated_at": "2023-01-09T11:47:35.390Z",
    "user_type": "SuperAdmin",
    "status": "active",
    "deleted_at": null,
    "password": null,
    "from_bulk": null,
    "profile_image_url": null,
    "settings": {}
  },
  "token": "[REDACTED]",
  "tenant": {
    "id": "3889ae06-ecc6-4705-8c64-f794c8ae389f",
    "name": "eLearning Plus",
    "short_name": "eL+",
    "url": "127.0.0.1",
    "created_at": "2023-01-09T11:08:49.583Z",
    "updated_at": "2023-01-09T14:44:35.864Z",
    "deleted_at": null,
    "settings": {
      "public_settings": {}
    },
    "parent_id": null,
    "logo": null,
    "logo_white": null,
    "logo_square": null,
    "logo_square_white": null
  }
}
```

## Sign Out

/api/v1/user/sign_out

DELETE

**Params**: add the **authentication token** of the user to this request

**Response:**

```json
{
  "message": "Signed out successfully."
}
```

## Sign Up

api/v1/users

POST

#### Body:

```json
{
  "user": {
    "first_name": "Arun",
    "last_name": "Patil",
    "email": "test@example.com",
    "invite": true
  }
}
```

#### Response:

```json
{
  "user": {
    "id": "76e0c2c5-d36c-4478-8c08-f85307ff688f",
    "first_name": "Arun",
    "last_name": "Patil",
    "email": "test@example.com",
    "tenant_id": "8dbb3a1d-98f6-4a75-a0dc-67f4470b400e",
    "created_at": "2022-04-01T05:26:44.198Z",
    "updated_at": "2022-04-01T05:26:44.335Z",
    "user_type": null,
    "status": "active",
    "deleted_at": null,
    "password": null,
    "from_bulk": null
  }
}
```

## Accept User Invitation

api/v1/users/invitation/accept

PUT

#### Body:

```json
{
  "invitation_token": "xxZubLu5Y8rGCkiyEweA",
  "password": "12345",
  "password_confirmation": "12345"
}
```

#### Response:

```json
{
  "status": "Invitation Accepted!",
  "user": {
    "email": "test@example.com",
    "id": "76e0c2c5-d36c-4478-8c08-f85307ff688f",
    "first_name": "Arun",
    "last_name": "Patil",
    "tenant_id": "8dbb3a1d-98f6-4a75-a0dc-67f4470b400e",
    "created_at": "2022-04-01T05:26:44.198Z",
    "updated_at": "2022-04-01T05:27:51.653Z",
    "user_type": null,
    "status": "active",
    "deleted_at": null,
    "password": "12345",
    "from_bulk": null
  },
  "token": "[REDACTED]"
}
```

## Upload media items

uploads/upload_media

POST

#### Body (form-data)

```json
[
  {
    "key": "files[]",
    "description": "",
    "type": "file",
    "enabled": true,
    "value": [
      "/home/patil/Downloads/arrival.png",
      "/home/patil/Downloads/BE Certificate.pdf",
      "/home/patil/Downloads/Beginner's Installation (1).odt",
      "/home/patil/Downloads/BusinessGreen-Webinar-Nigel-Griffiths-slides.ppt"
    ]
  },
  {
    "key": "tenant_id",
    "value": "8dbb3a1d-98f6-4a75-a0dc-67f4470b400e",
    "description": "",
    "type": "text",
    "enabled": true
  },
  {
    "key": "title",
    "value": "My media",
    "description": "",
    "type": "text",
    "enabled": true
  },
  {
    "key": "alt_text",
    "value": "Some alternate text",
    "description": "",
    "type": "text",
    "enabled": true
  }
]
```

#### Response: 

```json
{
  "success": "Media successfully uploaded",
  "uploaded_medias": [
    {
      "files": {
        "id": "6126f759-d3bc-46c4-b586-49063d1ec71c",
        "title": "My media",
        "alt_text": "Some alternate text",
        "properties": null,
        "location": "http://localhost:3000/rails/active_storage/blobs/redirect/eyJfcmFpbHMiOnsibWVzc2FnZSI6IkJBaHBSQT09IiwiZXhwIjpudWxsLCJwdXIiOiJibG9iX2lkIn19--9566e959342cb3153a353fe6ba31ba8f85f3776a/arrival.png",
        "tenant_id": "8dbb3a1d-98f6-4a75-a0dc-67f4470b400e",
        "media_type": "image/png",
        "deleted_at": null,
        "created_at": "2021-11-18T13:01:10.968Z",
        "updated_at": "2021-11-18T13:01:10.991Z",
        "file_name": "arrival.png"
      }
    },
    {
      "files": {
        "id": "24e40aca-d0dd-4db4-84c6-3cb18feece6b",
        "title": "My media",
        "alt_text": "Some alternate text",
        "properties": null,
        "location": "http://localhost:3000/rails/active_storage/blobs/redirect/eyJfcmFpbHMiOnsibWVzc2FnZSI6IkJBaHBSUT09IiwiZXhwIjpudWxsLCJwdXIiOiJibG9iX2lkIn19--32dea80820d9103381097a6abdc95fb67623ec30/BE%20Certificate.pdf",
        "tenant_id": "8dbb3a1d-98f6-4a75-a0dc-67f4470b400e",
        "media_type": "application/pdf",
        "deleted_at": null,
        "created_at": "2021-11-18T13:01:11.001Z",
        "updated_at": "2021-11-18T13:01:11.010Z",
        "file_name": "BE Certificate.pdf"
      }
    },
    {
      "files": {
        "id": "dffa0757-95a7-4c59-8f21-c5f853964711",
        "title": "My media",
        "alt_text": "Some alternate text",
        "properties": null,
        "location": "http://localhost:3000/rails/active_storage/blobs/redirect/eyJfcmFpbHMiOnsibWVzc2FnZSI6IkJBaHBSZz09IiwiZXhwIjpudWxsLCJwdXIiOiJibG9iX2lkIn19--faf3114caabe3f3967d220db88a9c710df59eaeb/Beginner's%20Installation%20(1).odt",
        "tenant_id": "8dbb3a1d-98f6-4a75-a0dc-67f4470b400e",
        "media_type": "application/vnd.oasis.opendocument.text",
        "deleted_at": null,
        "created_at": "2021-11-18T13:01:11.017Z",
        "updated_at": "2021-11-18T13:01:11.027Z",
        "file_name": "Beginner's Installation (1).odt"
      },
      "signed_id": "eyJfcmFpbHMiOnsibWVzc2FnZSI6IkJBaHBSZz09IiwiZXhwIjpudWxsLCJwdXIiOiJibG9iX2lkIn19--faf3114caabe3f3967d220db88a9c710df59eaeb"
    },
    {
      "files": {
        "id": "a3009fc3-b2ab-4c1a-92ad-05c3f120145a",
        "title": "My media",
        "alt_text": "Some alternate text",
        "properties": null,
        "location": "http://localhost:3000/rails/active_storage/blobs/redirect/eyJfcmFpbHMiOnsibWVzc2FnZSI6IkJBaHBSdz09IiwiZXhwIjpudWxsLCJwdXIiOiJibG9iX2lkIn19--8c5ac65d13dfb02f6237223f2fa27a0cb3f82290/BusinessGreen-Webinar-Nigel-Griffiths-slides.ppt",
        "tenant_id": "8dbb3a1d-98f6-4a75-a0dc-67f4470b400e",
        "media_type": "application/vnd.ms-powerpoint",
        "deleted_at": null,
        "created_at": "2021-11-18T13:01:11.017Z",
        "updated_at": "2021-11-18T13:01:11.027Z",
        "file_name": "BusinessGreen-Webinar-Nigel-Griffiths-slides.ppt"
      }
    }
  ]
}
```

## Tenant settings

api/v1/tenant/setting

GET

#### Response:

```json
{
  "settings": {}
}
```

## Update Tenant logos

api/v1/tenant/update

PUT

#### Params:
```json
{
  profile_image: FILE
  login_image: FILE
  tenant_id: string // (optional)
}
```
#### Response :

```json
{​​​​​​
  "tenant": {​​​​​​
    "id": "b9adb12d-c679-449a-bf70-81091fd9db41",
    "name": "Kreatio Software",
    "short_name": "kreatio",
    "url": "127.0.0.1",
    "created_at": "2022-04-08T07:06:46.469Z",
    "updated_at": "2022-08-01T13:03:54.194Z",
    "deleted_at": null,
    "settings":  {
      "public_settings": { ... }
    }
    "parent_id": null,
    "profile_logo":   "http://127.0.0.1:3000/rails/active_storage/blobs/redirect/eyJfcmFpbHMiOnsibWVzc2FnZSI6IkJ BaEpJaWsyT1RGbE56VTFZeTA0TXpVMUxUUTBZV1F0T1RJek5DMHpPV1V4WVRReU9UWTJaV1lHT2daRlZBPT0iLCJleHAiOm51bGwsInB1ciI6ImJsb2JfaWQifX0=--16580f9935bdfc8005e8d5df1e72d9983cf6d464/skype2.jpeg",
    "login_logo":   "http://127.0.0.1:3000/rails/active_storage/blobs/redirect/eyJfcmFpbHMiOnsibWVzc2FnZSI6IkJBaEpJaWt4T0dKa01EbG1PQzFtWTJWa0xUUTBNRE10T0RJNU9TMW1OV1V6WTJGbU56SXpNekVHT2daRlZBPT0iLCJleHAiOm51bGwsInB1ciI6ImJsb2JfaWQifX0=--c4b1465c3b7b717c93197568da5f8ce183c7196b/skype2copy.jpeg"
  }
}
```

## Generate meta data

api/v1/generate_meta_data?url=[url_string]

Method: GET

#### Response: 

```json
{
  "meta_data": {​​​​​​​​​
    "url": "<https://rocketvalidator.com/>",
    "scheme": "https",
    "host": "rocketvalidator.com",
    "root_url": "<https://rocketvalidator.com/>",
    "title": "Automated site-wide validation for large sites :: Rocket Validator",
    "best_title": "Automated site-wide validation for large sites :: Rocket Validator",
    "author": null,
    "best_author": null,
    "description": "Simplify site validation. Find Accessibility and HTML issues in your large sites, in seconds.",
    "best_description": "Simplify site validation. Find Accessibility and HTML issues in your large sites, in seconds.",
    "h1": [
      "Automated site-wide validation for large sites"
    ],
    "h2": [
      "Site-wide validation made easy",
      "One click, thousands of checks",
      "Test your sites at different screen resolutions",
      "Simple, actionable reports",
      "Validated by current standards",
      "Continuous validation",
      "What developers say",
      "Frequently asked questions",
      "Rocket Validator",
      "About Our Service",
      "Guides and Tutorials",
      "Follow us"
    ],
    "h3": [
      "Lightning-fast site validation",
      "Accessibility scanner",
      "HTML validation",
      "Scheduled validations",
      "Deploy hooks",
      "API integration",
      "Device viewport emulation",
      "Share reports with your team",
      "How much does it cost?",
      "Is there a free trial?",
      "Can I cancel or change plans any time?",
      "Can I validate more than one site?",
      "Can I share reports with other people?",
      "How long are reports stored?",
      "Ready to check your sites? Start your trial today."
    ],
    "h4": [],
    "h5": [],
    "h6": [],
    "links": {​​​​​​​​​​​​​​​​
    "internal": [
      "<https://rocketvalidator.com/>",
      "<https://rocketvalidator.com/#main>",
      "<https://rocketvalidator.com/pricing?billing=monthly>",
      "<https://rocketvalidator.com/html-validation>",
      "<https://rocketvalidator.com/accessibility-validation>",
      "<https://rocketvalidator.com/blog>",
      "<https://rocketvalidator.com/contact>"
    ],
    "external": [
      "<https://docs.rocketvalidator.com/>",
      "<https://www.deque.com/axe/>",
      "<https://validator.w3.org/nu>",
      "<https://docs.rocketvalidator.com/api/>",
      "<https://docs.rocketvalidator.com/guest-accounts/>",
      "<https://www.ideas4all.com/?site_language=en-US>",
      "<https://www.fulfilmentcrowd.com/>",
    ],
    "non_http": []
    }​​​​​​​​​​​​​​​​,
    "images": [
      "<https://d2bcamzsryg1pm.cloudfront.net/images/screenshots/rocket-summary-8d0f1565b5c93290b245f0b11b4435ef.jpg?vsn=d>",
      "<https://d2bcamzsryg1pm.cloudfront.net/images/screenshots/new-site-report-6fef36d2c93c3ce04465f19177dd29c2.png?vsn=d>",
      "<https://rocketvalidator.com/images/screenshots/devices/reverb-iphone13.jpg>",
    ],
    "charset": "utf-8",
    "feed": null,
    "feeds": [],
    "content_type": "text/html",
    "meta_tags": {​​​​​​​​​​​​​​​​
      "name": {​​​​​​​​​​​​​​​​
        "viewport": [
          "width=device-width, initial-scale=1.0"
        ],
        "description": [
          "Simplify site validation. Find Accessibility and HTML issues in your large sites, in seconds."
        ],
        "csrf-token": [
          "IXUJPywzHxsABhdCCg8UWwx3TBs9VSZZWGpIzkLPXcY1xBdiGE4UbfCo"
        ],
        "twitter:card": [
          "summary"
        ],
        "twitter:site": [
          "@rocketvalidator"
        ],
        "twitter:title": [
          "Automated site-wide validation for large sites :: Rocket Validator"
        ],
        "twitter:description": [
          "Simplify site validation. Find Accessibility and HTML issues in your large sites, in seconds."
        ],
        "msapplication-tilecolor": [
          "#ffffff"
        ],
        "msapplication-tileimage": [
          "<https://d2bcamzsryg1pm.cloudfront.net/images/favicons/ms-icon-144x144-926526bf32801c6d07982f14bda5df8f.png?vsn=d>"
        ],
        "theme-color": [
          "#ffffff"
        ]
      }​​​​​​​​​​​​​​​​,
      "http-equiv": {​​​​​​​​​​​​​​​​
      "x-ua-compatible": [
        "ie=edge"
      ]
      }​​​​​​​​​​​​​​​​,
      "property": {​​​​​​​​​​​​​​​​
        "og:image": [
          "<https://d2bcamzsryg1pm.cloudfront.net/images/screenshots/rocket-home-4a1b19b37eef201bfb934a31ae9b505f.jpg?vsn=d>"
        ]
      }​​​​​​​​​​​​​​​​,
      "charset": [
      "utf-8"
      ]
    }​​​​​​​​​​​​​​​​,
    "favicon": "<https://d2bcamzsryg1pm.cloudfront.net/images/favicons/android-icon-192x192-eb96bf829d7d32335efae2e772c428fd.png?vsn=d>",
    "response": {​​​​​​​​​​​​​​​​
      "status": 200,
      "headers": {​​​​​​​​​​​​​​​​
        "connection": "keep-alive",
        "access-control-allow-credentials": "true",
        "access-control-allow-origin": "*",
        "access-control-expose-headers": "",
        "cache-control": "max-age=0, private, must-revalidate",
        "content-length": "45216",
        "content-type": "text/html; charset=utf-8",
        "date": "Thu, 18 Aug 2022 13:31:46 GMT",
        "server": "Cowboy",
        "strict-transport-security": "max-age=31536000",
        "x-request-id": "a9d86a26-95d4-42a4-8e6c-13d761066aaf",
        "via": "1.1 vegur"
      }​​​​​​​​​​​​​​​​
    }​​​​​​​​​​​​​​​​
  }​​​​​​​​​​​​​​​​
}​​​​​​​​​​​​​​​​
```

Generate Image URL on Fly

uploaded_images/[media_item_id]?w=[integer]&h=[integer]>

Method: GET

#### Response: 
```json
{​​​​​
  "url": "<http://127.0.0.1:3000/rails/active_storage/representations/redirect/eyJfcmFpbHMiOnsibWVzc2FnZSI6IkJBaEpJaWszWldZeFlUWmtZaTAyT1RreUxUUTFZekV0T1RsaU5DMWxPRFZsWVRKak1USTBPRFVHT2daRlZBPT0iLCJleHAiOm51bGwsInB1ciI6ImJsb2JfaWQifX0=--4bf67c6cdd2f9047532b36644260ec59f23127a8/eyJfcmFpbHMiOnsibWVzc2FnZSI6IkJBaDdCem9MWm05eWJXRjBTU0lKYW5CbFp3WTZCa1ZVT2hSeVpYTnBlbVZmZEc5ZmJHbHRhWFJiQjBraUNEWXdNQVk3QmxSSklnZzBNREFHT3daVSIsImV4cCI6bnVsbCwicHVyIjoidmFyaWF0aW9uIn19--fdfe212d80b8892a0d39dde3dc90befca5154087/DSC_0264%20(1)-min.JPG>"
}​​​​​
```

## Update Password

api/v1/user/update_password

PUT

#### Body: 
```json
{​​​​​​​
    "reset_password_token": "w8LJcSFuhuLP-ZUueHAG",
    "old_password": "qw456",
    "new_password": "123456",
    "new_password_confirmation": "123456"
}​​​​​​​
```

#### Response: 
```json
{​​​​​​​​​​
    "user": {​​​​​​​​​​
    "email": "test@example.com",
    "id": "7029bd65-21eb-484b-a64d-4c6eda83ae53",
    "first_name": "Arun S",
    "last_name": "Patil",
    "tenant_id": "77005c63-ccbf-4e8d-8d14-3788bd9cca21",
    "created_at": "2022-05-04T10:08:02.572Z",
    "updated_at": "2022-09-07T11:07:41.888Z",
    "user_type": "SuperAdmin",
    "status": "active",
    "deleted_at": null,
    "password": "123456",
    "from_bulk": null,
    "profile_image_url": null,
    "settings": {​​​​​​​​​​}​​​​​​​​​​
    }​​​​​​​​​​
}​​​​​​​​​​
```

## Password reset

api/v1/user/request_password_reset

PUT

#### Body:
```json
{​​​
  "email": "test@example.com"
}​​​​​​​​​​
```

#### Response:
```json
{​​​​​​​​​​​​
    "message": "Reset password instruction sent successfully for test@example.com"
}​​​​​​​​​​​​​​​​​​​
```

## Act as another user

api/v1/user/act_as/[user_id]

GET

#### Response: 
```json
{​​​​​​​​
    "token": "[REDACTED]"
}​​​​​​​​
```

## Send Invitation

api/v1/users/send_invitation

POST

#### Body: 
```json
{​​
  "user_ids": ["f0f8a28f-f350-45bb-a82c-6f58f6543738", "f2a64dc2-ee3e-4dc7-bf68-137fc46143b4"]
}
```
or
```json
{
  "emails": ["test@example.com"]
}
```
OR
```json
{
  "bulk_import_id": "f0f8a28f-f350-45bb-a82c-6f58f6543738"
}​​​​​​​​​
```

#### Response:
```json
{​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
    "message": "Invitations Sent"
}​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
```

## Tenant Font Upload

/api/v1/tenant/upload_fonts

POST

#### Params:
```json
{
  name: "Sample Name",
  file: [FILE],
  description: "",
}
```

Response:
```json
{
  "status": "success",
  "tenant_font": {
    "id": "e13b3615-c160-487b-aa40-6cdbb04f7e69",
    "tenant_id": "f03f8411-53b7-437d-bf7b-c2fca2caece3",
    "name": "Lato 4",
    "description": null,
    "file_path": "<http://localhost:3000/rails/active_storage/blobs/redirect/eyJfcmFpbHMiOnsibWVzc2FnZSI6IkJBaEpJaWxrWmpsak9UZzRNaTFqWTJFekxUUXlZekl0T1ROaVlpMWpZMkl4WXpnM09EQTFaR0lHT2daRlZBPT0iLCJleHAiOm51bGwsInB1ciI6ImJsb2JfaWQifX0=--5bc4ce09f029bd8778d965ab5fc58a2a0b35c284/Lato%204>",
    "created_at": "2023-08-14T13:36:14.797Z",
    "updated_at": "2023-08-14T13:36:14.900Z"
  },
  "message": "Fonts uploaded and metadata set successfully"
}
```

Login
Log out
Sign Up
Send invitation
Accept invitation
Update password
Password reset
Act as another user
Upload tenant font
Tenant settings
Update Tenant logos
Upload media items
Generate meta data
