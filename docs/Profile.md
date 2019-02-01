#  Profile Functions

This documentation covers the Profile management feature of the web service. `/profile` <br /> This involves `Getters` and `Setters` functions of individual/collective SMT account profile.

## [Getters](#getters) `/` &amp; [Setters](#setters) `/set`

[Info](#info) | [Mailing address](#info-address) | [Balances](#balance) | [Kits](#kit) | [KYC](#kyc) | [Network](#network)

<a name="getters"></a>
<a name="info"></a>
### Profile (Getters) `/`

**Action:** `/profile`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **user**  | `string`  | * | _SMT username_ |
| **author**  | `string` | * | _SMT username_ who's requesting |


#### On-Success: xtra params

- `username`
- `email`
- `phone`
- `name`
- `type`  _(account type)_
- `status`
- `sex`
- `dob`
- `ref`
- `avatar`
- `profile_page`
- `ref_link`
- `currency`
- `country_code`


<a name="info-address"></a>
### Mailing address `/address`

**Action:** `/profile/address`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **user**  | `string`  | * | _SMT username_ |
| **author**  | `string` | * | _SMT username_ who's requesting |


#### On-Success: xtra params

- `user`
  - `username`
  - `address` : _object_
    - `address`
    - `country`
    - `country_code`
    - `state` _(province)_
    - `state_code`
    - `city`
    - `city_code`
    - `zip`


<a name="balance"></a>
### Account Balance `/balance`

**Action:** `/profile/balance`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **user**  | `string` _SMT username_  | * |  |
| **author**  | `string` _SMT username_  | * | Logged in SMT `username` |


#### On-Success: xtra params
- `user`
- `username`
- `wallets` _object_
 - `wallet_name`
   - `balance`
   - `updated` _last updated_


<a name="kit"></a>
### Kits `/kit`

_feature coming soon_


<a name="kyc"></a>
### KYC

Refer to [/kyc/personid](./KYC.md#personid)



<a name="network"></a>
### Network `/network`

**Action:** `/profile/network`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **user**  | `string` _SMT username_  | * | |
| **level** | `integer` `1`-`5`  | *   | network level |
| **status**  | option `string`   |   | default: `ALL`. Options: `ACTIVE`,`PENDING`,`SUSPENDED`,`BANNED` |


#### On-Success: xtra params

- `user`
- `network` _object_ _array_
 - `username`
 - `name`
 - `email`
 - `phone`
 - `sex`
 - `dob`
 - `ref`
 - `avatar`

---

<a name="setters"></a>
## Setters `/set`

[Profile](#set-profile) | [Avatar](#set-avatar) | [Mailing address](#set-address) | [Kit settings](#set-kit) | [KYC](#set-kyc) | [Network](#set-network)

<a name="set-profile"></a>
### Profile `/`

**Action:** `/profile/set`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **user**  | `string` _SMT username_  | * | |
| **author**  | `string` _SMT username_  | *  | currently logged in user performing request |
| **name**  |  `string` |   | |
| **type**  | `string`  |   |  account type: `PERSONAL` `CORPORATE` |
| **sex**  | `string`  |   | `MALE`, `FEMALE`, (`OTHER`) _for corporate account type_ |
| **dob**  | `string` _option_  |   |  date of birth or date of incorporation |
| **currency**  | `string`  |   | Preferred urrency: `NGN`,`USD`,`EUR`,`GBP` |


#### On-Success: xtra params

- `user` _object_
  - `username`
  - `name`
  - `type`  _(account type)_
  - `sex`
  - `dob`
  - `currency`


<a name="set-avatar"></a>
### Profile picture (avatar) `/avatar`

**Action:** `/profile/set/avatar`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **user**   | `string` |  * | SMT `username`  |
| **file_id**  | `integer`  | *  | File ID  |
| **author**   | `string`  |  * | SMT `username` Logged user/making request  |



<a name="set-address"></a>
### Mailing address `/address`

**Action:** `/profile/set/address`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **user**     | `string` _SMT username_  | * | |
| **author**  | `string` _SMT username_  | *  | currently logged in user performing request |
| **country_code**  |  `string` {2,2} |   | e.g. `NG` for Nigeria |
| **state_code**  |  `string` {5,5} |   | e.g. `NGLAG` for Lagos/Nigeria |
| **city_code**  |  `string` {8,8} |   | e.g. `NGLAGFES` for Festac, Lagos/Nigeria |
| **address**  | `string` {5,128}  |   | |
| **zip**  | `string` {3,25} |    |  | |


#### On-Success: xtra params

- `user` _object_
  - `country` _friendly name_
  - `country_code`
  - `state` _friendly name_
  - `state_code`
  - `city` _friendly name_
  - `city_code`
  - `address`
  - `zip`


<a name="set-kit"></a>
### Kit setting `/kit`

**Action:** `/profile/set/kit`

**Request parameters**

| Parameter    | Type     | Required     | Remark |
|--------------|----------|:------------:|--------|
| **user**  | `string` _SMT username_  | * | |
| **author**  | `string` _SMT username_  | *  | _currently logged in user performing request_ |
| **type**  |  `string` |   | _Kit type. e.g. `NFCBAND`_ |
| **kid**  | `string`  | _Kit ID_  | |
| **vcode**  |  `string` |   | verification code |


<a name="set-kyc"></a>
### KYC setting

Refer to [/kyc/personid](./KYC.md#set-personid)



<a name="set-network"></a>
### Network settings `/network`

**Action:** `/profile/set/network`

* _feature coming soon_
