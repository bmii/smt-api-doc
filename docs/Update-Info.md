[Update 15-10-2018](#15-10-2018)

----

<a name="15-10-2018"></a>
# Reported issue resolution

**[Q1]:** **[RESOLVED]**: Edit Store: If we edit a store's open time, closing time, open days, location, etc, it doesn't edit, shows error "Please contact administrator" error: RunTym error but if we edit other fields the store gets updated successfully.


**[Q2]:** Products List screen > Select product from MyStore > send myStore ID to /estore API we don't get a result for it.

**[ANS]:** This happens because of:

1. The store might not [`status`] active. A store by default is not active until KYC has been fulfilled and Admin verified.
2. Inactive store is not show to the public.
2. Required params not parsed: if either: owner, manager, cashier is not passed with request, the API assumes it is the public requesting and therefore not return inactive store.

**As a temporal fix, i have changed the status of all store to be active**


**[Q3]:**  **[RESOLVED]** SignUp > Country list API need author now to hit, where would we get author from in sign up page.


**[Q4]:** **[RESOLVED]** Store Avatar URL is not coming in Estore list to display


**[Q5]:** **[RESOLVED]** Products > Edit Products > how to edit or remove product pictures already present for a product.


**[Q6]:** Payment flow needs to be discussed, product buying flow needs to be discussed


**[Q7]:** **[RESOLVED]** Estore List > Doesnt show updated details like, open time, closing time, open days, location, etc.


**[Q8]:** **[RESOLVED]** Catalouge,
When the Catalouge is created we have no option to add proucts to the catalouge, how is that to be done. How can a user buy a whole catalouge as         it is mentioned in the checkout API. How do we know a particular product belongs to a catalouge.


**[Q9]:** **[RESOLVED]** Setting Pin,

Setting pin for the app requires an OTP as mandatory, when we come in the initial flow this screen is to be shown after adding phone which also needs  an OTP, how are we to send OTP for the pin and where is it to be sent.

**[ANS]:**

- OTP for can be sent to both email/phone, primarily email unless special cases such as adding/changing phone number.
- PIN OTP can be sent to email.


**[Q10]:** **[RESOLVED]** Flow of KYC and its related API not clear. Where should we upload files, in the upload file screen or KYC screen itself

**[ANS]:** Any can do. If user already has file uploaded,  he can choose to use it else shoe the user upload screen.

**[Q11]:** **[RESOLVED]** User Avatar is not setting up, not getting saved.



# UPDATES

There has been new update in following sections

# Store:

## [`/estore`](./eStore.md#set-store)

  1. [`refid`]: this is unique human friendly way to reference a store. its (all lower-case) alphanumeric can only contain - or _ as punctuation.
    * this makes the address of a store e.g: https://smt.ac/es/store-refid
    * when creating new store, kindly suggest the [store name] to the user entered as refid; replacing spaces with - and making it lowercase.
  2. [`type`] `OFFLINE` -or- `ONLINE` (as option). this makes it easier to filter local stores and online stores


## [`/estore/product`](./eStore.md#set-product)
  1. [`refid`] this is unique human friendly way to reference a product. its (all lower-case) alphanumeric can only contain - or _ as punctuation.
    * this makes the address of a product e.g: https://smt.ac/pr/product-refid
    * when creating new product, kindly suggest the [product name] to the user entered as refid; replacing spaces with - and making it lowercase.

## [`/estore/catalog`](./eStore.md#set-catalog)
  1. [`refid`] this is unique human friendly way to reference a catalog. its (all lower-case) alphanumeric can only contain - or _ as punctuation.
    * this makes the address of a catalog e.g: https://smt.ac/cg/product-refid
    * when creating new catalog, kindly suggest the [catalog name] to the user entered as refid; replacing spaces with - and making it lowercase.

## [`/estore/assign/photos`](./eStore.md#prod-photo)

This for adding/modifying preview photos for product and catalog.


## [`/estore/set/cover`](./eStore.md#cover-photo)

This for setting default photo for a product/catalog.


## [`/estore/remove/photo`](./eStore.md#remove-photo)

Remove set photo from product/catalog.


## [`/estore/set/catalogremove`](./eStore.md#catalog-remove)

Remove set product from catalog.


## [`/estore/set/catalogitem`](./eStore.md#catalog-add)

Add products to catalog catalog.


## [`/estore/set/currency`](./eStore.md#set-currency)

This for setting store's accepted payment/currency photo for a product/catalog.

## [`/estore/category`](./eStore.md#category)

This was updated to make category human readable. `id` was removed, `name` is now primary search key. `title` was added to give description.

# Data:

  1. [ [`/data/currency`](./Data.md#currency) ]: added to fetch list of supported currencies.
  2. [ [`/data/bank`](./Data.md#bank-code) ]: added to fetch bank list/detail.
  3. [ [`/data/mobilenetwork`](./Data.md#mobile-network) ]: added to fetch mobile network list/info.
  4. [ [`/data/mobileplan`](./Data.md#mobile-plans) ]: added to fetch mobile network data plans.
  5. [ [`/data/charges`](./Data.md#charges) ]: added to fetch service charges.
  6. [ [`/data/xrate`](./Data.md#xrate) ]: added to fetch xchange rates.
  7. [ [`/data/personid`](./Data.md#person-id) ]: added to fetch list if accepted person id types.
  8. [ [`/data/about`](./Data.md#about) ]: added to fetch company's about info.
  9. [ [`/data/terms`](./Data.md#terms) ]: added to fetch company's terms of service.
  10. [ [`/data/policy`](./Data.md#terms) ]: added to fetch company's policies.
  11. [ [`/data/faq`](./Data.md#faq) ]: added to fetch company's FAQs and Answers.
