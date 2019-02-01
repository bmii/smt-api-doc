# Account functions
This documentation covers every posible action/functionality doable on `/account` level operation of the API.

[Register](#register) | [Verify](#verify) | [Set verify email](#verify-set) | [Reset password](#resetpass) | [Authenticate](#authenticate) | [Change password](#password) | [Change email](#email) | [Change Phone](#phone) | [Change PIN](#pin) | [Invite](#invite)

**App resource:** account

<a name="register"></a>
## Register `/register`
_Create new Simple Merchant Account._

**Action:** `/account/register`

**Request Parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **username**  | `alphanum` {3,12}   |*   |  letters and numbers only. |
| **ref**  | `alphanum` {3,12}   |   |letters and numbers only |
| **name**  | `string` {5,55}  |*   |full person/organization name. |
| **email**  | `string`   | *   | valid/receiving email |
| **device_type**  | `alphanum` {3,35}  | *   | |
| **device_token**  | `alphanum` {4,255}  | *   | |
| **country_code**   | `string`  | *  | e.g. `NG` |
| **password**  | `string` {8,16}   | *   | |
| **password_repeat**  |    | *   | same as password |
| **accepted_terms**  | `boolean`   | *   | |
| **signature**  | `string`   | *   | | |

**Signature Hashing params and order:**

**order:** `SMTB&{app_private_key}&{email}&{username}`

### On-Success: xtra params

Info required to log user in:

- `user` _object_
  - `uniqueid` : username
  - `username` : account username
  - `email` : account email
  - `phone` : account phone number
  - `status` : account status
  - `avatar` : profile picture


<a name="verify"></a>
## Verify `/verify`
_Check if account email has been verified._

**Action:** `/account/verify`

**Request Parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **email**  | `string`   | *   | valid/receiving email |


### On-Success: xtra params

- `user` _object_
  - `username` : account username
  - `email` : account email
  - `status` : account status


<a name="verify-set"></a>
## Set verify email `/setemail`
_Change account email for failure to receive verification email._

**Action:** `/account/verify/setemail`

**Request Parameters**

| Parameter     | Type     | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **old_email**  | `string`   | *   | old email to be changed |
| **password**  | `alphanum`  | *  |  user's current password |
| **email**  | `string`   | *   | new email |



<a name="resetpass"></a>
## Reset password `/resetpass`
**Action:** `/account/resetpass`

**Request parameters**

| Parameter     | Type      | Required     | Remark |
|--------------|-----------|-----------------|-------|
| **user**  | `string` `email`&#124;`phone`  | *   | |
| **otp**  | `alphanum` , `string` `numbers` {6,12}  | *  | `otp` recieved from `/otp` operation |
| **password**  | `alphanum` {8,16}  | *  | |
| **password_repeat** |   | *  | Same as password |
| **signature**  | string  | *   | | |

**Signature hashing params and order:**

- `user`
- `otp`
- `password`

**Order**
 `SMTB&{app_private_key}&{user}&{otp}&{password}`

<a name="authenticate"></a>
 ## Authenticate `/authenticate`

 **Action:** `/account/authenticate`

 **Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **user**  | `string` `username`&#124;`email`&#124;`phone`  | *   |  |
| **password**  | `alphanum` {8,16}  | *  | |
| **country_code**   | `string` {2,2}  |   | E.g: `NG` Helps when user is logging in with phone number entered in local format.  |

#### On-Success: xtra params

- `user` _object_
  - `uniqueid` : username
  - `username` : account username
  - `email` : account email
  - `phone` : account phone number
  - `status` : account status
  - `avatar` : profile picture


<a name="password"></a>
## Change password `/set/password`

**Action:** `/account/set/password`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **username**  | `string` `username`  | *   | |
| **old_password** | `string`  | *  | |
| **password**  | `string` {8,16}  | *  | |
| **password_repeat**  |   | * | Same as password |


<a name="email"></a>
## Change email `/set/email`

**Action:** `/account/set/email`

Before sending this request, you must have initiated OTP request from `/otp/email` to get `otp` code for the new email you want to change to.

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **user**  | `string`  | *   | SMT username |
| **email**  | `string` `email`  | *   | where OTP was sent to |
| **otp** | `string`, `alphanum`  | *  | OTP received |
| **password**  | `string`  | *  | current user's password |


<a name="phone"></a>
## Change phone `/set/phone`

**Action:** `/account/set/phone`

Before sending this request, you must have initiated OTP request from `/otp/sms` to get `otp` code for the new phone number you want to change to.

**Request parameters**

| Parameter     | Type     | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **user**  | `string`  | *   | SMT username |
| **phone**  | `string` `phone`  | *   | `ISO` _E.164_ number format |
| **otp** | `string`, `alphanum`  | *  | OTP received |
| **password**  | `string`  | *  | current user's password |


<a name="pin"></a>
## Change PIN `/set/pin`

**Action:** `/account/set/pin`

Before sending this request, you must have obtained OTP code from `/otp/sms` | `/otp/email`.


**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **user**  | `string` `email`&#124;`phone`  | *   | where OTP `code` was sent |
| **otp**  | `string` `alphanum`  | *   | code received |
| **pin** | `interger` {4,6}  | *  | |
| **pin_repeat** |   | *  | same as 'pin' |
| **password**   | `string`  |  * | Account password  |


<a name="invite"></a>
## Invite to join `/invite`

**Action:** `/account/invite`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **user**  | `string` `user`  | *   | SMT username |
| **receiver**  | `string` `email`&#124;`phone`  | *   | where invitation will be sent. NOTE: if set to phone number `user` will be charged for SMS rate. |
| **greeting** | `string` {25,125}  |   | Friendly (additional) greeting message |
