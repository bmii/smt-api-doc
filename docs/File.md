# File functions
This documentation covers every posible action/functionality doable on `/file` level operation of the API. <br>
The `/file` is file management tool to upload and further manipulate already uploaded file.

## Getters
[File list](#file) | [Folders](#folder)
## Setters
[Upload](#upload) | [Create/edit folder](#mkdir) | [Add files to folder](#set-folder) | [Set caption](setcaption) | [Delete file]


<a name="file"></a>
## File `/`

_Fetch files owned by given user._

**Action:** `/file`

**Request Parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **id**  | `integer`  |   | when sent, all other filter will be ignored.  |
| **owner**   | `string`  | *  | SMT `username`  |
| **page**  | `integer`  |    | default: `1` |
| **limit** | `integer`  |    | maximum record to fetch. default: `56` |
| **author**   | `string`  | *  | Logged in SMT `username'/`uniqueid`  |


#### On-Success: xtra params

- `records`
- `page`
- `pages`
- `limit`
- `has_previous`
- `has_next`
- `previous`
- `next`
- `files` _object array_
  - `id`
  - `name`
  - `url`
  - `mime`
  - `size`
  - `owner`
  - `caption`
  - `privacy`
  - `created`


<a name="folder"></a>
## Folders `/folder`

_Fetch folders owned by given user._

**Action:** `/file/folder`

**Request Parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **id**  | `integer`  |   | when sent, all other filter will be ignored.  |
| **owner**   | `string`  | *  | SMT `username`  |
| **author**   | `string`  | *  | Logged in SMT `username'/`uniqueid`  |


#### On-Success: xtra params

- `folders` _object array_
  - `id`
  - `name`
  - `files` _files count_
  - `created`


## Setters
[Upload](#upload) | [Create/edit folder](#mkdir) | [Add files to folder](#set-folder) | [Set caption](setcaption) | [Delete file/folder](#delete)


<a name="upload"></a>
## Upload file `/upload`

_Upload file(s)._

**Action:** `/file/upload`

**Request Parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **owner**   | `string`  | *  | SMT `username`  |
| **privacy**   | `string`  | *  | `PRIVATE` [only owner will have viewing access] -OR- `PUBLIC` (default) |
| **folder**   | `integer`  |   | folder `id` where file(s) will be saved to. Default is: `Uploads`  |
| **files**   | `array`  | *  |   |
| **author**   | `string`  | *  | Logged in SMT `username'/`uniqueid`  |


**`files` array**
```
[
  {
    "name" => "filename.ext", # required
    "type" => "image/png", # required
    "size" => "1024", # required (in bytes)
    "caption" => "",
    "data" => ""  # required [base64_encoded file data/content]
  },
  {
    "name" => "filename2.ext",
    "type" => "image/png",
    "size" => "2048",
    "caption" => "my store logo",
    "data" => "hujsdkkkudshusdhh=ksuekjsdjhsdnuiewkkskjsllio"
  }
]
```

#### On-Success: xtra params
- `failed` _array of index/names_
- `uploaded` _object array_
  - `id`
  - `name`
  - `url`
  - `mime`
  - `size`
  - `owner`
  - `caption`
  - `privacy`
  - `created`


<a name="mkdir"></a>
## Create/edit folder `/mkdir`

_Create or change folder name._

**Action:** `/file/mkdir`

**Request Parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **id**   | `integer`  |   | only changing folder name  |
| **name**   |  `string` | *  | folder name  |
| **owner**   | `string`  | *  | SMT `username`  |
| **author**   | `string`  | *  | Logged in SMT `username'/`uniqueid`  |


#### On-Success: xtra params

- `folder` _object array_
  - `id`
  - `name`
  - `owner`
  - `created`


<a name="set-folder"></a>
## Add files to folder `/setfolder`

**Action:** `/file/setfolder`

**Request Parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **folder**   | `integer`  | *  | folder id |
| **files**   |  `array` | *  | array of file ids: `[1,255,784,41]`  |
| **author**   | `string`  | *  | Logged in SMT `username'/`uniqueid`  |


<a name="setcaption"></a>
## Set file caption `/setcaption`

**Action:** `/file/setcaption`

**Request Parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **file**   | `integer`  | *  | file id |
| **caption**   |  `string` | *  |   |
| **author**   | `string`  | *  | Logged in SMT `username'/`uniqueid`  |


<a name="delete"></a>
## Delete file/folder `/delete`

**Action:** `/file/delete`

**Request Parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|--------|
| **id**   | `integer`  | *  | file/folder id |
| **type**   |  `string` | *  | `FILE` -OR- `FOLDER`  |
| **author**   | `string`  | *  | Logged in SMT `username'/`uniqueid`  |
