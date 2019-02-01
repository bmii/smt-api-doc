#  OTP Functions

This documentation covers the One Time Password feature of the web service. `/otp` <br /> There are two methods to send One Time Password for authentication users' requests.

[Email](#email) | [SMS](#sms) | [Resend](#resend) | [Verify](#verify)

<a name="email"></a>
## Email `/email`

**Action:** `/otp/email`

**Request parameters**

| Parameter     | Type      | Required     | Remark |
|---------------|-----------|:-------------:|-------|
| **email**  | `string` `email`  | *   | where OTP will be sent to. |
| **length**  | `integer`  |    | default: `6` |
| **otp**  | `string`  |    | custom `code` |
| **subject**  | `string` {5,35} |    | custom subject.
| **message**  | `string` {25,125} |    | custom message. if you wish to set custom greeting message. `message` should contain '{{OTP}}' as placeholder for OTP code. |
| **alphanum** | `boolean`  |   | should OTP be mixed? default: `false` |
| **signature**  |  `string` | *  | | |

**Signature Hashing params and order:**

- `email`

**order:** `SMTB&{app_private_key}&{email}`

#### On-Success: xtra params

- `otp` _object_
  - `id`



<a name="sms"></a>
## SMS `/sms`

**Action:** `/otp/sms`

**Request parameters**

| Parameter     | Type      | Required     | Remark |
|---------------|-----------|:------------:|-------|
| **phone**  | `string` `phone`  | *   | where OTP will be sent to. `ISO` _E.164_ number format |
| **length**  | `integer`  |    | default: `6` |
| **otp**  | `string`  |    | custom `code` |
| **message**  | `string` {25,120} |    | custom message. if you wish to set custom greeting message. `message` should contain '{{OTP}}' as placeholder for OTP code. |
| **alphanum** | `boolean`  |   | should OTP be mixed? default: `false` |

**Signature Hashing params and order:**

- `phone`

**order:** `SMTB&{app_private_key}&{phone}`

#### On-Success: xtra params

- `otp` _object_
  - `id`


<a name="resend"></a>
## Resend OTP `/resend`

**Action:** `/otp/resend`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **id**  | `integer`  | *   | OTP id |

#### On-Success: xtra params

- `otp` _object_
  - `id`


<a name="verify"></a>
## Verify OTP `/verify`

**Action:** `/otp/verify`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **user**  | `string`  | *   | email or Phone (ISO E.164  format) |
| **otp**  | string  | *  |  received OTP code |
