# Data functions
This documentation covers every posible action/functionality doable on `/data` level operation of the API. <br>
The `/data` provides basic resources for different operations.


[Country](#country) | [State/Province](#state) | [City](#city) | [Local Government Area](#lga)


[Mobile Networks](#mobile-network) | [Mobile Data plans](#mobile-plan) | [Exchange rate](#xrate) | [Bank information](#bank-code) | [Currency List](#currency)


[Service Charges](#charges) | [Person ID Types](#person-id) | [About us](#about) | [Terms of Service](#terms) | [Policies](#policy) | [FAQs](faq)


<a name="country"></a>
## Country `/country`

_Fetch countries (list)._

**Action:** `/data/country`

**Request Parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **code**  | `string` {2,2}   |   |  Country code. (if u want to fetch just one country) |
| **page**  | `integer`  |    | default: `1` |
| **limit** | `integer`  |    | maximum record to fetch. default: `ALL` |
| **author**  | `string`  | *  | Requesting/logged in user. (SMT username)  |


#### On-Success: xtra params

- `records`
- `page`
- `pages`
- `limit`
- `has_previous`
- `has_next`
- `previos`
- `next`
- `countries` _object array_
  - `code`
  - `name`
  - `numbercode`
  - `phonecode` _International dialing code_
  - `iso3` _ISO 3 code_


<a name="state"></a>
## State/province `/state`

_Fetch states/provinces for given country  (list)._


**Action:** `/data/state`

**Request Parameters**

| Parameter    | Type     | Required     | Remark |
|--------------|----------|:------------:|-------|
| **country_code**  |  `string` {2,2} |   | |
| **code**  | `string` {5,5}   |   |  only neccessary when `country_code` is not present |
| **page**  | `integer`  |    | default: `1` |
| **limit** | `integer`  |    | maximum record to fetch. default: `ALL` |
| **author**  | `string`  | *  | Requesting/logged in user. (SMT username)  |


#### On-Success: xtra params

- `records`
- `page`
- `pages`
- `limit`
- `has_previous`
- `has_next`
- `previos`
- `next`
- `states` _object array_
  - `country`
  - `country_code`
  - `code`
  - `name`


<a name="city"></a>
## City `/city`

_Fetch cities for given state  (list)._


**Action:** `/data/city`

**Request Parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|-------|
| **state_code**  |  `string` {5,5} |   | |
| **code**  | `string` {8,8}   |   |  only neccessary when `state_code` is not present |
| **page**  | `integer`  |    | default: `1` |
| **limit** | `integer`  |    | maximum record to fetch. default: `ALL` |
| **author**  | `string`  | *  | Requesting/logged in user. (SMT username)  |


#### On-Success: xtra params

- `records`
- `page`
- `pages`
- `limit`
- `has_previous`
- `has_next`
- `previos`
- `next`
- `cities` _object array_
  - `state`
  - `state_code`
  - `code`
  - `name`


<a name="lga"></a>
## Local Government Area `/lga`

_Fetch Local Government Areas for given state  (list)._


**Action:** `/data/lga`

**Request Parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:-------------:|-------|
| **state_code**  |  `string` {5,5} |   | |
| **code**  | `string` {8,8}   |   |  only neccessary when `state_code` is not present |
| **page**  | `integer`  |    | default: `1` |
| **limit** | `integer`  |    | maximum record to fetch. default: `ALL` |
| **author**  | `string`  | *  | Requesting/logged in user. (SMT username)  |


#### On-Success: xtra params

- `records`
- `page`
- `pages`
- `limit`
- `has_previous`
- `has_next`
- `previos`
- `next`
- `lgas` _object array_
  - `state`
  - `state_code`
  - `code`
  - `name`


<a name="mobile-network"></a>
## Mobile Network information `/mobilenetwork`

**Action:** `/data/mobilenetwork`

**Request Parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:-------------:|-------|
| **name**  |  `string` {2,25} |   | Network code e.g `MTNNG`. When given only one record will be returned |
| **inset**  | `array`  |   | array of network names/code  |
| **author**  | `string`  | *  | Requesting/logged in user. (SMT username)  |


#### On-Success: xtra params

- `networks` _object array_
  - `name`
  - `title`



<a name="mobile-plans"></a>
## Mobile Data plan `/mobileplan`

**Action:** `/data/mobileplan`

**Request Parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:-------------:|-------|
| **network**  |  `string` {3,25} | * | Network code/name e.g `MTNNG` |
| **author**  | `string`  | *  | Requesting/logged in user. (SMT username)  |


#### On-Success: xtra params

- `plans` _object array_
  - `name`
  - `title`
  - `price`


<a name="charges"></a>
## Service Charges `/charges`

**Action:** `/data/charges`


| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:-------------:|-------|
| **name**  |  `string` {3,25} |  | When given, only single matching record will be returned |
| **author**  | `string`  | *  | Requesting/logged in user. (SMT username)  |


#### On-Success: xtra params


- `charges` _object array_
  - `name`
  - `amount` _(`decimal`)_
  - `fixed` _(`boolean` whether/not fixed rate, If `false` amount is in percentage)_
  - `cap` _maximum charged (in case of non-fixed amount)_
  - `remark`


<a name="xrate"></a>
## Xchange rates `/xrate`

**Action:** `/data/xrate`


| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:-------------:|-------|
| **xfrom**  |  `string` {3,5} |  | Currency code: When given, only matching record will be returned |
| **convert**  | `decimal`  |   | 18,8  |
| **date_from**  | `date`  |   | [Min]: Find from this date  |
| **date_to**  | `date`  |   | [Max]: Find till this date  |
| **author**  | `string`  | *  | Requesting/logged in user. (SMT username)  |


#### On-Success: xtra params

- `rates` _object array_
  - `currency`
    - `subrates` _(currency code)_
      - `rate`
      - `updated`


<a name="bank-code"></a>
## Payment Bank list/info `/bank`

**Action:** `/data/bank`


| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:-------------:|-------|
| **code**  |  `string` {3,15} |  | Bank code: When given, only matching records will be returned |
| **author**  | `string`  | *  | Requesting/logged in user. (SMT username)  |


#### On-Success: xtra params

- `banks` _object array_
    - `code`
    - `name`


<a name="person-id"></a>
## KYC Person ID types `/personid`

**Action:** `/data/personid`


| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:-------------:|-------|
| **code**  |  `string` {3,15} |  | ID code: When given, only matching records will be returned |
| **author**  | `string`  | *  | Requesting/logged in user. (SMT username)  |


#### On-Success: xtra params

- `types` _object array_
    - `code`
    - `name`


<a name="currency"></a>
## Fetch list of currencies `/currency`

**Action:** `/data/currency`


| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:-------------:|-------|
| **code**  |  `string` {3,8} |  | Currency code: When given, only matching records will be returned |
| **author**  | `string`  | *  | Requesting/logged in user. (SMT username)  |


#### On-Success: xtra params

- `currencies` _object array_
    - `code`
    - `title`


<a name="about"></a>
## Fetch About info of company `/about`

**Action:** `/data/about` `POST` `GET`


#### On-Success: xtra params

- `html` _HTML formatted content_


<a name="terms"></a>
## Fetch company's terms of service `/terms`

**Action:** `/data/terms` `POST` `GET`


#### On-Success: xtra params

- `html` _HTML formatted content_


<a name="policy"></a>
## Fetch company's Policies `/policy`

**Action:** `/data/policy` `POST` `GET`


#### On-Success: xtra params

- `html` _HTML formatted content_


<a name="faq"></a>
## Fetch company's FAQs `/faq`

**Action:** `/data/faq` `POST` `GET`


#### On-Success: xtra params

- `html` _HTML formatted content_
