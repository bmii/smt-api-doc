# Payment

This documentation covers every posible action/functionality doable on `/payment` level operation of the API.

[Payment History](#payments) | [Checkout](#checkout) | [Confirm](#confirm) | [Send Link]() | [Withdrawal](#withdrawal) | [SMT Share redemption](#share-redeem)

---

<a name=payments></a>
## Payments history `/history`

Fetch payment/transaction History.

**Action:** `/payment/history`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|-------|
| **id**  | `string`  |  | when present, every other params/filters are ignored |
| **search**  | `string`  |  | E.g payer's username. |
| **type**  | `string` _option_  |  | `DEBIT`, `CREDIT` `ALL`. Default: `ALL` |
| **status**  | `string` _option_  |  | `PAID`, `PENDING` `CANCELED`.  Default: `ACTIVE` |
| **page**  | `integer`  |    | default: `1` |
| **limit**  | `integer`  |    | maximum record in cases of search. default: `25` |


#### On-Success: xtra params

- `page` _integer_
- `pages` _integer_
- `limit` _integer_
- `records` _integer_
- `next` _integer_ , _boolean_ (next page)
- `previous` _integer_ , _boolean_ (previous page)
- `payments` _object array_
  - `id`
  - `qrcode`
  - `status`
  - `amount`
  - `xrate`
  - `currency`
  - `remark`
  - `payer`
  - `receiver`
  - `created`


<a name=checkout></a>

## Checkout `/checkout`

Initiate payment.

**Action:** `/payment/checkout`

**Request parameters**

| Parameter    | Type      | Required     | Remark |
|--------------|-----------|:------------:|-------|
| **payer**  | `string`  | * | Who will pay: `SMTUSERNAME`, `email`, `phone` |
| **receiver**  | `string`  |  * | `SMTUSERNAME` -or- SMT store  |
| **type**  | `string` _option_ | * | `SELF` (default), `SMTSHARE`  |
| **share_to**  | `string`  |   | `SMTUSERNAME`  |
| **amount**  | `float` | *  |   |
| **remark**  | `string`  |   | optional message/description  |
| **request**  |  `string` _option_ |   | Send request to payer via: `SMS`, `EMAIL` Note: `SMS` attracts charge from author's account  |
| **items**  | `array`  |   | for eStore checkout only.  |
| **author**  | `string`  | *  | Logged in SMT username  |

**Guides**

**receiver** can be either SMT username (for personal receiver) or store id with prefix: `SMT\ES\{store_id}` (for stores).

In a case of automated checkout from SMT store the Receiver is `SMTSTORE` as payment is sent to system and then further splited into beneficiary(s)' accounts.

**amount** leave blank in case of eStore checkout

**items** sample:

```
[
  {
    "id" : "5a855s5",
    "type" : "CATALOG",
    "quantity" : 2
  },
  {
    "id" : "5a855s5",
    "type" : "PRODUCT",
    "quantity" : 5
  }
]
```


#### On-Success: xtra params

- `id` _integer_
- `amount` _float_
- `discount` _float_
- `qrcode`
- `url` _payment link_
- `method` _array_: allowed collection method
