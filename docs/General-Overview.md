# Simple Merchant – SMT 1.0 API Web service
## Documentation
**API endpoint:**`{ENDPOINT}`
1. **Testing/dev:**  smtest.info
2. **Production:** simplemerchant.com

All requests must be sent with pre-created app credentials to https://api.{ENDPOINT}. <br> You can create a request app from [https://dev.{ENDPOINT}](https://dev.{ENDPOINT})

### App access
When creating an app, you must define resource type you want to consume with the app as your access will be restricted to only the approved resources.

#### Modifying an App.
When an app is modified/updated, it becomes inactive and can not make a request until it is manually verified by an Admin.

#### App Resource/Access

| Resourse  | Access      |
|----------:|-------------|
| `ultimate`   | Ultimate access to all resources  |
| `account`  | Ultimate account access  |
| `account-login`   | Can initiate account login request  |
| `account-register` | Can create new account |
| `account-profile` | Update created account including KYC |
| `estore` | Manipulate eStore content |
| `payment` | Initiate and view payment |
| `email` | Email access |
| `sms` | SMS access |
| `otp` | One Tym Password access |
| `settings` | View and manage settings |
| `data` | Data and miscellaneous content |

### General requirements.
To access the API, some custom header has to be sent with request.

** Custom headers: **
1. **Smt-App:** the app name
2. **Smt-Key:** app public key
3. **Signature-Method:**  hashing signature method for request e.g sha256 or sha512
4. **Tymstamp:** request tym (time) in milliseconds
5. **Smt-Signature:**  hash (lowercase hexits ) of the following parameters/string accordingly concatenated with ‘&’:
  - **SMTH** – header prefix
  - **Smt-App**
  - **App private key**
  - **Signature method**
  - **Tymstamp**

This value (Smt-Signature) should be base64_encoded.

** Optional Header **
1. **Accept:** `application/json`

## Request
The web service accepts only `JSON` body. However not all request requires a body to be sent.

### Request Parameters

`*` Marks required field otherwise blank for optional field

`A|B` either (one) `A` or `B` must be sent with request.

`{5,8}` Minimum Character length or Minimum number value = `5`, Maximum Character length or Maximum number value = `8`

### Body signature

For sensitive requests, you might be required to provide signature as parameter along with request body.


When this measure is required, parameters information will be provided in order of how it should be hashed.

The hash string is a group of parameters concatenated with '&' symbol. The default parameters are:

- SMT body prefix : `SMTB`
- App private key: `app_private_key`
- Other parameters: _will be provided when necessary_

In this case, the hash string will be: `SMTB&{app_private_key}&{other parameters}`

The hash string should be calculated with same `Signature-Method` passed to the request header and `base64_encoded`. Same process for hashing the header's `Smt-Signature` but with different parameter combination.


---
## Response
If connection is successful you will get a `JSON` response body.

## Handling response
Every response must contain following.
1.	status – `[string]` e.g. 00 == everything went well
  - error code
  - error count
2.	message – `[string]` Request response message
3.	errors – `[array]` holds error details. Empty when all went well

### On-Success: xtra params
Upon successful request, some request may contain extra parameters appended to response body. These parameteers will be specified where applicable.

### Error codes
The error codes ranges from 0-9
-	**0:** No error
-	**1:** Authentication error
-	**2:** Privilege error
-	**3:** Parameter error
-	**4:** Runtym error
-	**5:** Third party error
-	**9:** Unknown/uncaught  error
