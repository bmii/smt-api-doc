# Email functions
This documentation covers every posible action/functionality doable on `/email` level operation of the API. <br>
The `/email` section of the Web Service API provides mailing functions

[Send email](#send) | [Sent email](#sent) | [Inbox](#inbox)

<a name="send"></a>
## Email (send) `/send`

_Send new email_

**Action:** `/email/send`

**Request Parameters**

| Parameter     | Type      | Required     | Remark |
|--------------|-----------|:-----------------:|-------|
| **transport**  | `string` _option_   |   |  `SMTP`, `API`, default: `AUTO` |
| **template**  | `string`  |    | template name; |
| **gateway**  | `string`  |   | leave blank if you do not have gateway assigned |
| **domain**  | `string`  |   |  Custom domain |
| **sender**   | `object` OR `string`  |  * | `string`: "Sender Name &lt;sender@email.ext&gt;" OR simple email email@domain.ext <br> `object`: `{"name" : "Sender Name","email" : "sender@email.ext"}`  |
| **replace**   | `pattern`  |   | E.g: `name:{NAME}`,`email:{EMAIL}`  |
| **replace_keys**   | `array`  |   | keys to search for in recipient object  |
| **message**  | `object` _array_  | *  | see message object below |


**Message key/value -explained**

| Key   | Required | Value type  |
|-------|:----------:|-------------|
| **subject**   | * | `string` {5,95} Email subject  |
| **text**   |  | `string`  {15,2048} Alternative email body incase your recipient does not have HTML email viewer. If empty, default value will be applied |
| **html**   | | `html` {15,}  Rich HTML email body |
| **recipient**   | * | `array` of `string` of either: name/email pair e.g ("Sender Name &lt;sender@email.ext&gt;") or simple email (sender@email.ext) <br> **OR** <br> `string` of either: name/email pair e.g ("Sender Name &lt;sender@email.ext&gt;") or simple email (sender@email.ext). <br> Can also take `array` of `object` in case where replacement should apply. <br> E.g `[{name:name,email:email,username:username,firstname:firstname}, {name:name,email:email}]` |
| **cc**   | |  `array` of `string` of either: name/email pair e.g ("Sender Name &lt;sender@email.ext&gt;") or simple email (sender@email.ext) <br> **OR** <br> `string` of either: name/email pair e.g ("Sender Name &lt;sender@email.ext&gt;") or simple email (sender@email.ext) |
| **bcc**   | |  `array` of `string` of either: name/email pair e.g ("Sender Name &lt;sender@email.ext&gt;") or simple email (sender@email.ext) <br> **OR** <br> `string` of either: name/email pair e.g ("Sender Name &lt;sender@email.ext&gt;") or simple email (sender@email.ext) |


**Message sample**

```
[
  {
    subject : "New email",
    text : "Incase u dont have HTML email receiver.",
    html : "<html> <h2 style=\"color:red\">Hi in red.</h2> <p>This is paragraph.</p> </html>",
    recipient : [
      "Recipient One <email-one@domain.ext>",
      "email-two@gmail.com",
      "More Recipient <more@email.info"
    ],
    cc : [
      "Carbon Copy <email-one@domain.ext>",
      "email-two@gmail.com"
    ],
    bcc : [
      "Carbon Copy <email-one@domain.ext>",
      "email-two@gmail.com"
    ]
  },
    subject : "New email type 2",
    text : "Incase u dont have HTML email receiver.",
    html : "<html> <h2 style=\"color:red\">Hi in red.</h2> <p>This is paragraph.</p> </html>",
    recipient : "Recipient One <email-one@domain.ext>",
    cc : "email-two@gmail.com"
  }
]

```

**Message replacement**

This performs replacement in cases of message sent to multiple `recipient` i.e Bulk message. <br>
For this to work, you will have to provide `replace_keys`: keys to search for in the recipient object matching the pattern (`replace`). <br>
Replacement is performed on message subject and body. <br>
_Example:_ <br>

`recipient` would be:
```
[
  {
    "firstname" : "First",
    "surname" : "Surname",
    "email" : "email@example.com",
    "phone" : "+23480123456",
    "username" : "SMTUSER"
  },
  {
    "firstname" : "First 2",
    "surname" : "Surname 2",
    "email" : "email2@example.com",
    "phone" : "+23480123456",
    "username" : "SMTUSER2"
  }
]
```
`replace_keys` would be: <br>
`["firstname","surname","email","phone","username"]`


`replace` pattern would be: (each separated with comma) <br>

firstname:{FIRSTNAME},surname:{SURNAME},email:{EMAIL},phone:{PHONE} e.t.c.

`subject` can be: "Message for {FIRSTNAME} {SURNAME}" <br>

`text` or `html` can contain: <br>
 Hello {FIRSTNAME}, your email is {EMAIL} and your phone number is {PHONE}. <br>
 Please don't forget we can call you {USERNAME}

 As expected, these replacements will be performed accordingly.

#### On-Success: xtra params

- `batch` _array_
  - `email` : `qid`


<a name="sent"></a>
## Sent Email `/sent`


**Action:** `/email/sent`

**Request Parameters**

| Parameter     | Type      | Required     | Remark |
| --------------|-----------|:-----------------:|------- |
| **email**  | `string`   |   |  Sender's email address |
| **page**  | `integer`  |    | default: `1`|
| **limit** | `integer`  |    | maximum record to fetch. default: 25 |


#### On-Success: xtra params

- `sent` _object array_
  - `qid`
  - `batch`
  - `states`
  - `subject`
  - `text`
  - `html`
  - `sender`
  - `recipient`
  - `cc`
  - `bcc`
  - `created`


<a name="inbox"></a>
## Email Inbox `/inbox`


**Action:** `/email/inbox`

**Request Parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:-----------------:|------- |
| **email**  | `string`   |   |  Recipient's email address |
| **page**  | `integer`  |    | default: `1` |
| **limit** | `integer`  |    | maximum record to fetch. default: 25 |


#### On-Success: xtra params

- `inbox` _object array_
  - `qid`
  - `batch`
  - `states`
  - `subject`
  - `text`
  - `html`
  - `sender`
  - `recipient`
  - `cc`
  - `bcc`
  - `created`
