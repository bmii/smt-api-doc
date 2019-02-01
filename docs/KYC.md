#  Know Your Customer (KYC) Functions

This documentation covers the KYC management feature of the web service. `/kyc` <br /> This involves `Getters` and `Setters` functions of SMT accounts/stores.

## [Getters](#getters)

[Person ID](#personid) | [Store ID](#storeid)


<a name="personid"></a>
### Person ID `/personid`

**Action:** `/kyc/personid`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **user**  | `string`  | * | _SMT username_ |
| **author**  | `string` | * | _SMT username_ who's requesting |


#### On-Success: xtra params

- `kyc`
  - `accountid`
    - `username`
    - `name`
    - `email`
    - `phone`
    - `avatar`
    - `address`
    - `city`
    - `state`
    - `country`
    - `zip`
  - `personid` : _object_
    - `type`
    - `number`
    - `file`
  - `bankid` : _object_
    - `bank`
    - `type` _account type_
    - `number` _account number_
    - `sort` _account sort code_



<a name="storeid"></a>
### Store ID `/storeid`

**Action:** `/kyc/storeid`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **store**  | `integer`  | * | _Store ID_ |
| **author**  | `string` | * | _SMT username_ who's requesting |


#### On-Success: xtra params

- `kyc`
  - `storeid`
    - `id`
    - `name`
    - `regno`
    - `logo`
    - `owner`
    - `address`
    - `city`
    - `state`
    - `country`
    - `files` _KYC file: array_
  - `bankid` : _object_
    - `bank`
    - `bank_code`
    - `type` _account type_
    - `number` _account number_
    - `sort` _account sort code_




## [Setters](#setters) `/set`

[Person ID](#set-personid) | [Bank  ID](#set-bankid) | [Set KYC File](#set-file)


<a name="set-personid"></a>
### Person ID `/set/personid`

**Action:** `/kyc/set/personid`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **user**  | `string` {3,12}  | * | SMT `username` |
| **type**  | `string`  | * | Type `code` Ref: [/data/personid](./Data.md#person-id) |
| **number**  | `string`  | *  | ID number  |
| **author**  | `string` | * | _SMT username_ who's requesting |



<a name="set-bankid"></a>
### Bank ID `/set/bankid`

**Action:** `/kyc/set/bankid`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **user**  | `string`  | * | SMT `username` -OR- Store `id` |
| **identify**  | `string` option  | * | Options: `STORE`, `PERSON` |
| **bank_code**  | `string`  | * | Bank `code` Ref: [/data/bank](./Data.md#bank-code) |
| **number**  | `string`  | *  | Account number  |
| **type**  | `string` option  | *  | Account type: `SAVING`, `CURRENT`  |
| **sort**  | `string`  |   | Account sort code  |
| **author**  | `string` | * | _SMT username_ who's requesting |


<a name="set-file"></a>
### Set KYC file(s) `/set/file`

**Action:** `/kyc/set/file`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **user**  | `string`  | * | SMT `username` -OR- Store `id` |
| **type**  | `string` option  | * | Options: `KYCPID`, `KYCSID` |
| **files**  | `array`  | *  | Array of file IDs  |
| **author**  | `string` | * | _SMT username_ who's requesting |
