# eStore functions
This documentation covers every posible action/functionality doable on `/estore` level operation of the API.


## [Getters](#getters) `/` &amp; [Setters](#setters) `/set`

<a name=getters></a>
## Getters `/`

[Stores](#stores) | [Discount](#discount) | [Products](#products) | [Managers](#managers) | [Cashiers](#cashiers) | [Checkout Officers](#checkout-officers) | [Catalogs](#catalog) | [Catalog items](#catalog-item) | [Categories](#category) | [Checkout list](#checkouts)


<a name=stores></a>
### Stores `/`

**Action:** `/estore`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **id**  | `integer`/`string`  |  | [store id] or [store refid]: when present, every other params/filters are ignored |
| **search**  | `string`  |  | regular search query. |
| **type**  | `string` option  |  | Store type: `OFFLINE`, `ONLINE` |
| **sort**  |   |   | `DISTANCE`{ASC}  |
| **owner**  | `string` _SMT username_  |  | `username` of owner to filter |
| **manager**  | `string` _SMT username_  |  | `username` of manager to filter |
| **cashier**  | `string` _SMT username_  |  | `username` of cashier to filter |
| **city_code**  | `string`  |  | eg. `NGLAGFES` find all in this city |
| **state_code**  | `string`  |  | eg. `NGLAG` find all in this state |
| **country_code**  | `string`  |  | eg. `NG` find all in this country |
| **page**  | `integer`  |    | default: `1` |
| **limit**  | `integer`  |    | maximum record in cases of search. default: `25` |
| **author**   | `string`  |  * | Logged in user  |


#### On-Success: xtra params

- `page` _integer_
- `pages` _integer_
- `limit` _integer_
- `records` _integer_
- `next` _integer_ , _boolean_ (next page)
- `previous` _integer_ , _boolean_ (previous page)
- `stores` _object array_
  - `id`
  - `refid`
  - `type`
  - `name`
  - `regno` _(registeration number)_
  - `owner`
  - `tags`
  - `info`
  - `qrcode`
  - `url`
  - `logo`
  - `address`
  - `city_code`
  - `city`
  - `state_code`
  - `state`
  - `country_code`
  - `country`
  - `latitude`
  - `longitude`
  - `holidays`
  - `open_from`
  - `open_till`
  - `created`


<a name=discount></a>
### Stores default discount`/discount`

**Action:** `/estore/discount`

**Request parameters**

| Parameter     | Type     | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **store_id**  | `integer`  | * | store id |
| **author**  | `string`   | * | SMT  `username` of logged user |


#### On-Success: xtra params

- `store` _string array_
  - `id` _integer_
  - `name` _string_
  - `discount` _float_ the dicount in percentage


<a name=products></a>
### Products `/product`

**Action:** `/estore/product`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **id**  | `integer`/`string`  |  | [product id] or [product refid] when present, every other params/filters are ignored |
| **search**  | `string`  |  | Search query, search overrides every other filter. |
| **store_id**  | `string`  |  | find only from this store(s). For multiple: 124,444,57,5 |
| **category**  | `string`  |  | Category |
| **min_price**  | `float`  |   | |
| **max_price**  | `float`  |   | |
| **sort**  | `string`  |   | e.g `PRICE_DESC` `PRICE_ASC`, `TOKEN_ASC`, `TOKEN_DESC`, `RATING_ASC` `RATING_DESC`, `DISTANCE` |
| **latitude**  | `decimal` 10,8  |   | Required when sorting by distance  |
| **longitude**  | `decimal` 11,8  |   | Required when sorting by distance  |
| **city_code**  | `string` {8,8}  |   | Fetch within city  |
| **state_code**  | `string` {5,5}  |   | Fetch within state/province  |
| **country_code**  | `string` {5,5}  |   | Fetch within country  |
| **owner**  | `string` _SMT username_  |  | `username` of owner to filter |
| **manager**  | `string` _SMT username_  |  | `username` of manager to filter |
| **cashier**  | `string` _SMT username_  |  | `username` of cashier to filter |
| **page**  | `integer`  |    | default: `1` |
| **limit**  | `integer`  |    | maximum record in cases of search. default: `25` |
| **author**  | `string` _SMT username_  |  | `username` of logged in user |


#### On-Success: xtra params

- `page` _integer_
- `pages` _integer_
- `limit` _integer_
- `records` _integer_
- `next` _integer_ , _boolean_ (next page)
- `previous` _integer_ , _boolean_ (previous page)
- `products` _object array_
  - `id`
  - `refid`
  - `name`
  - `price`
  - `discount`
  - `use_token`
  - `store`
  - `store_id`
  - `tags`
  - `category_id`
  - `category`
  - `qrcode`
  - `rating`
  - `url`
  - `cover` cover image (photo)
  - `photos` _object array: containing links to images_
  - `created`


<a name=managers></a>
### Store managers `/manager`

**Action:** `/estore/manager`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **store_id**  | `string`  | * | find cashiers from this store(s). |
| **author**  | `string`  |  *  | SMT `username` for logged in user |


#### On-Success: xtra params

- `store` _objsect array_
  - `id` _SMT username_
  - `name`
  - `managers` _[object array]_
    - `name`
    - `manager`
    - `active`


<a name=cashiers></a>
### Cashiers `/cashier`

**Action:** `/estore/cashier`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **store_id**  | `string`  | * | find cashiers from this store(s). |
| **author**  | `string`  | *  | SMT `username` for logged in user |


#### On-Success: xtra params

- `store` _objsect array_
  - `id` _SMT username_
  - `name`
  - `cashiers` _[object array]_
    - `name`
    - `cashier`
    - `active`


<a name=checkout-officers></a>
### Checkout officers `/checkoutofficer`

**Action:** `/estore/checkoutofficer`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **store_id**  | `string`  | * | find officer from this store(s). |
| **author**  | `string`  |  *  | SMT `username` for logged in user |


#### On-Success: xtra params

- `store` _objsect array_
  - `id` _SMT username_
  - `name`
  - `officiers` _[object array]_
    - `name`
    - `officer`
    - `active`


<a name=catalog></a>
### Catalogs `/catalog`

**Action:** `/estore/catalog`

**Request parameters**

| Parameter     | Type     | Required     | Remark |
|--------------|-----------|:-------------:|--------|
| **id**  | `integer` / `string`  |  | [catalog id] -or- [catalog refid]:  when present, every other params/filters are ignored |
| **search**  | `string`  |   |   |
| **store_id**  | `integer` |  | |
| **owner**  | `string` _SMT username_  |  | `username` of owner to filter |
| **manager**  | `string` _SMT username_  |  | `username` of manager to filter |
| **cashier**  | `string` _SMT username_  |  | `username` of cashier to filter |
| **page**  | `integer`  |    | default: `1` |
| **limit**  | `integer`  |    | maximum record in cases of search. default: `25` |
| **author**  | `string`  |  *  | SMT `username` for logged in user |


#### On-Success: xtra params

- `page` _integer_
- `pages` _integer_
- `limit` _integer_
- `records` _integer_
- `next` _integer_ , _boolean_ (next page)
- `previous` _integer_ , _boolean_ (previous page)
- `catalogs` _object array_
  - `id`
  - `refid`
  - `name`
  - `tags`
  - `store`
  - `store_id`
  - `products` _integer_ product count
  - `price`
  - `discount`
  - `use_token`
  - `rating`
  - `cover`
  - `qrcode`
  - `photos`
  - `token`
  - `created`


<a name=catalog-item></a>
### Catalog items `/catalog/item`

**Action:** `/estore/catalog/item`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **id**  | `integer`  | * | catalog id |
| **author**  | `string`  |  *  | SMT `username` for logged in user |


#### On-Success: xtra params

- `items` _object array_
  - `id`
  - `name`
  - `category`
  - `store`
  - `store_id`
  - `photos` _object array: containing links to images_


<a name=category></a>
### Categories `/category`

Fetch product category list

**Action:** `/estore/category`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **name**  | `string`  |  | find by name (primary search ID) |
| **page** | `integer`  |   | Current page  |
| **limit** | `integer`  |   | Max record: default `ALL`  |
| **author** | `string`  |  * | SMT `username`  |


#### On-Success: xtra params

- `categories` _object array_
  - `name`
  - `title`
  - `products` _integer_ product count


<a name=checkouts></a>
### Checkout list `/checkouts`

Fetch checkout list

**Action:** `/estore/checkouts`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **user**  | `string`  | *  |  SMT `username` requesting view |
| **id**  | `integer`  |  | find by ID |
| **store_id**  | `integer`  |   |  filter by store |
| **status**  | `string`  |   | filters: `PAID` `PENDING` default: `ALL` |
| **page**  | `integer`  |    | default: `1` |
| **limit**  | `integer`  |    | maximum record in cases of search. default: `25` |


#### On-Success: xtra params

- `page` _integer_
- `pages` _integer_
- `limit` _integer_
- `records` _integer_
- `next` _integer_ , _boolean_ (next page)
- `previous` _integer_ , _boolean_ (previous page)
- `checkouts` _object array_
  - `id`
  - `status`
  - `price`
  - `items` _object array_
    - `name`
    - `price`

---
<a name=setters></a>
## Setters `/set`

[Store](#set-store) | [Store logo](#set-logo) | [Discount](#discount) | [Set Currency](#set-currency) | [Product](#set-product) | [Product photos](#prod-photo) | [Store manager](#set-manager) | [Cashier](#set-cashier) | [Checkout Officer](#set-checkout-officer) |  [Catalog](#set-catalog) | [Add to Catalog](#catalog-add) | [Remove from catalog](#catalog-remove) | [Checkout](#set-checkout) | [Set Cover photo](#cover-photo) | [Assign photos](#assign-photo) | [Remove Photo](#remove-photo)

<a name=set-store></a>
### Store `/set`

Create/modify store.


**Action:** `/estore/set`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **id**  | `integer`  |  | when present, modify function is performed. |
| **type**  | `string` _option_ | * | : `OFFLINE`, `ONLINE` |
| **name**  | `string` {5,95} | * | |
| **regno**  | `string` {5,55} |  | registeration number e.g CAC Reg. |
| **tags**  | `string`  | *  | |
| **info**  | `text` {125,550} | *  |  Store information |
| **holidays**   | `boolean`  | *  | open on holidays?  |
| **days_open**   | `option`  | *  | `WEEKENDS`, `WEEKDAYS`, `247`  |
| **open_from**  | `time`  | *  | e.g. `8:00` `13:24`   |
| **open_till**  | `time`  | *  | e.g. `17:25` `00:30`   |
| **address**  | `text`  | *  | |
| **city_code**  | `string`  | * | eg. `NGLAGFES` find |
| **state_code**  | `string`  | * | eg. `NGLAG` |
| **country_code**  | `string`  | * | eg. `NG` |
| **latitude**  | `decimal` 10,8  |  |  |
| **longitude**  | `decimal` 11,8 |  |  |
| **owner**  | `string` _SMT username_  | * | store owner |
| **author**  | `string` _SMT username_  | * | Logged in user |

These fields/params: `name`, `regno`, `tags`, `info`, `address`, `city_code`, `state_code`, `country_code`, `owner`, `author` are required for creating new store record. However, when making an update; all must not be sent.



<a name=set-logo></a>

### Store logo

Refer to: [`/set/cover`](#cover-photo) type=`STORELOGO`

---


<a name=set-discount></a>
### Store default discount `/set/discount`

Set/modify store default discount. <br>

**Action:** `/estore/set/discount`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **store**  | `integer`  | * | store id. |
| **rate**  | `integer` {0.1,100.00} | * | in percentage |
| **author**  | `string` | * | SMT username|

#### On-Success: xtra params

- `store`
  - `id` _integer_
  - `name` _string_
  - `discount` _integer_ percentage off



<a name=set-currency></a>
### Store accepted payment/currency currency `/set/currency`

Set/modify store default discount. <br>

**Action:** `/estore/set/discount`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **store**  | `integer`  | * | store id. |
| **currency**  | `array` | * | currency codes. [See `/data/currency`](./Data.md#currency) |
| **author**  | `string` | * | SMT username |


<a name=set-product></a>
### Store Products `/set/product`

Create/modify product.


**Action:** `/estore/set/product`

**Request parameters**

| Parameter     | Type     | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **id**  | `integer`  |  | when present, modify function is performed. |
| **store_id**  | `integer`  | * | store id |
| **cat_id**  | `integer`  | * | category id |
| **name**  | `string` {5,95} | * | |
| **currency** | `currency`  | *  | in local currency |
| **price** | `float`  | *  | in local currency |
| **discount**  | `float` {0.1,100.00}  |   | in percentage. when `null` on new record, default discount from `/estore/discount` is applied |
| **use_token**  | `boolean`  |   | whether/not to use store token |
| **quantity**  | `integer`  | *  | |
| **tags**  | `string`  | *  | |
| **info**  | `text` {55,550} | *  |  Store information |
| **author**  | `string` _SMT username_  | * | Logged in user |

These fields/params: `name`, `store_id`, `cat_id`, `info`, `address`, `city_code`, `state_code`, `country_code`, `owner`, `author` are required for creating new store record. However, when making an update; all must not be sent.

#### On-Success: xtra params



<a name=cover-photo></a>
###  Set Cover photo or store logo `/set/cover`

Set product/catalog cover(default) photo or store logo <br>

**Action:** `/estore/set/cover`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **id**  | `integer`  | * | store, product/catalog id. |
| **type**  | `string`  | *  | `PRODUCTCOVER` , 'CATALOGCOVER', `STORELOGO`  |
| **file**  | `integer` | * | file id |
| **author**  | `string` | * | SMT username |


**Types:** Product cover: `PRODUCTCOVER` | Catalog cover: `CATALOGCOVER` | Store Logo: `STORELOGO`


<a name=remove-photo></a>
###  Remove photo  `/remove/photo`

Remove from product/catalog <br>

**Action:** `/estore/remove/photo`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **id**  | `integer`  | * | store, product/catalog id. |
| **type**  | `string`  | *  | `PRODUCTPHOTO` , 'CATALOGPHOTO'  |
| **file**  | `integer` | * | file id |
| **author**  | `string` | * | SMT username |



<a name=prod-photo></a>
### Product/catalog photos

Refer to [`/assign/photos`](#assign-photo)



<a name="assign-photo"></a>
### Assign photos

Assign photos to a store product/catalog. <br>

**Action:** `/estore/assign/photos`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **id**  | `integer`  | * | product/catalog id. |
| **type**  | `string`  | *  | `PRODUCTPHOTO`,`CATALOGPHOTO`  |
| **photos**  | `array` | * | array of file ids |
| **author**  | `string` | * | SMT username |



<a name=set-cashier></a>
### Store cashier `/set/cashier`

Create/modify cashier.


**Action:** `/estore/set/cashier`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **store_id**  | `integer`  | * | store id |
| **cashier**  | `string` _SMT username_  | * | |
| **active**  | `boolean` |  | use only when removing already created cashier |
| **author**  | `string`: _SMT username_  | * | _Logged in user_.  |


<a name=set-manager></a>
### Store manager `/set/manager`

Create/modify manager.


**Action:** `/estore/set/manager`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **store_id**  | `integer`  | * | store id |
| **manager**  | `string` _SMT username_  | * | |
| **active**  | `boolean` |  | use only when removing already created cashier |
| **author**  | `string`: _SMT username_  | * | _Logged in user_.  |



<a name=set-checkoutofficer></a>
### Store cashier `/set/checkoutofficer`

Create/modify checkoutofficer.


**Action:** `/estore/set/checkoutofficer`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **store_id**  | `integer`  | * | store id |
| **cofficer**  | `string` _SMT username_  | * | |
| **active**  | `boolean` |  | use only when removing already created officer |
| **author**  | `string`: _SMT username_  | * | _Logged in user_.  |




<a name=set-catalog></a>
### Store catalog `/set/catalog`

Create/modify catalog.


**Action:** `/estore/set/catalog`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **id**  | `integer`  | * | Catalog id: when present, update/modify function is performed instead. |
| **store_id**  | `integer`  | * | store id |
| **name**  | `string`  | * | |
| **currency**   | `string`  | *  | e.g `NGN` |
| **price**   | `float`  | *  | |
| **tags**  | `string` {5,35} | *  | |
| **discount**   | `float`  |   | |
| **use_token** | `boolean`  |   | |
| **author**  | `string`: _SMT username_  | * | _Logged in user_.  |


<a name=catalog-add></a>
### Add item(s) to catalog `/set/catalogitem`


**Action:** `/estore/set/catalogitem`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **id**  | `integer`  | * |  |
| **proucts**  | `array`  | *  | array of product ids  |
| **author**  | `string`: _SMT username_  | * | _Logged in user_.  |



<a name=catalog-remove></a>
### Remove item from catalog `/set/cataloremove`


**Action:** `/estore/set/cataloremove`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **id**  | `integer`  | * |  |
| **prouct**  | `integer`  | *  | product id |
| **author**  | `string`: _SMT username_  | * | _Logged in user_.  |



<a name=set-checkout></a>
### Store checkout `/set/checkout`

Modify checkout. _Changing the status of a checkout list._ <br> This can be done by either store owner, cashier or Checkout officer.


**Action:** `/estore/set/checkout`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **id**  | `integer`  | * | Checkout ID |
| **status**  | `string` _option_  | *  |  `PAID`, `CANCELED` |
| **confirmed_by**  | `string`: _SMT username_  | * | _Logged in officer_ |
