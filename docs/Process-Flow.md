# Process Flow

To ensure shared experience across multiple platforms, these process flow must be implemented.

## COMPULSORY PROCEDURES
Here are flow update to be implemented in the Apps.

[Account](#account) | [eStore](#estore)

<a name=account></a>
## Account

### Registration flow

1. Create account `/account/register`
2. Verify the account `account/verify`
  1. Change email `account/verify/setemail` (if verification email was not received)
3. Modify profile `/profile/set`: _currency_, _type (account type)_, _sex_, _dob_
  1. Add mailing info (address) `profile/set/address`
  2. Add profile picture (not compulsory at this tym, it can be done later) `profile/set/avatar`
4. Set phone number `/account/set/phone`
5. Set PIN `/account/set/pin` (not compulsory at this tym, it can be done later)

### Explanation
#### 1. Create account
Follow parameter requirement at `account/register` to create new SMT account.

#### 2. Verify the account
After a successful `/account/register` request, its expected that user is automatically logged in, an email with **email verification** link has been sent to the email address provided via previous request.


This step confirms that user has followed instruction conveyed by the email received. Make a request to `/account/verify` to confirm this. If so, proceed to next step else inform user to follow instruction in email received.

Alternatively provide user with an option to change verification email if instruction does not arrive after 15 minutes.

#### 2.1 Change email
In the case where user did not receive verification email after 15 minutes of successful registration, make a request to `/account/verify/setemail` following parameter requirement. <br>
Upon success of this request, return to **2.** `/account/verify`

#### 3. Modify profile
Set up important profile information for user at `/profile/set`. These info includes
- Default currency `currency`
- Account type `type`
- Gender (in case of personal account) `sex`
- Date of birth/incorporation of business `dob`. This however can be left out for corporate account type.

#### 3.1 Set Mailing info
Set up user's mailing address at `/profile/address`. Regional data such as country, state/province, city can be fetched from `/data` section of the web service. <br>
Remember user already set country at registration point.

#### 3.2 Set Profile picture/avater
This can be done at `/profile/avater`. Not compulsory at this point tho.

#### 4. Set Account phone number
Follow parameter requirement at `/account/set/phone`.

#### 5. Set Account PIN
Follow parameter requirement at `/account/set/pin`. This step can be done later anyway.


<a name=estore></a>
## eStore

### Checkout list
The eStore should have a sub-page for checkouts. `/estore/checkouts` This page displays checkout list, available to store owner and assigned cashier | checkout officer.

### Store Views

The eStore button should link direct to product page which should display products with picture.
<br> Info to show includes:
- Price
- Token
- Discount

Store should be optional search/filter type and not landing page. However, there should store view section to display stores, their logo and location.


# Payment

## Send

## Receive

## Send Link

# App
