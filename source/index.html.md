---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Actum Integration Guide

Actum's API allows developers to manage a variety of powerful tasks, such as creating and updating transacions, managing customer and payment data, and querying settlement information. It was initially built for merchants requiring a high level of customization. Its customizable architecture now enables simple integration with software partners, as well. Actum uses HTTPS for all transactions to ensure the safety of consumer information. 

This guide provides an overview for our merchants and partners of how to start using Actum. If you have any questions throughout the process, please don't hesitate to contact us at [support@actumprocessing.com](support@actumprocessing.com).

# Getting Started
 
To get started using Actum's API, you'll want to follow these steps:
 
### Step 1: Register for a Test Account
 
First, you will want to navigate to Actum's [Register for a Test Account](https://www.actumprocessing.com/register-test-account/) page. You will need to enter your First Name, Last Name, Email, Company Name, and Phone Number to sign up. Actum's support team will use this information for verification purposes in order to create your account.

Once your account is created (typically within less than 24 hours on business days), you will receive a welcome email with your new test account credentials. 

### Step 2: Log into your Test Account

To begin testing, you will be able to log into a test portal using the username and password provided by Actum's support team. Actum's portal is available at the following link: [https://join.actumprocessing.com](https://join.actumprocessing.com)

It is recommended that you change your password immediately upon login. There is no need to create a separate API key to complete setup, as your username and password will allow you to authenticate to Actum's test enviroment, securely.

### Step 3: Create a Call

To create a new API call, you'll first want to join the server at [https://join.actumprocessing.com/cgi-bin/dbs/man_trans.cg](https://join.actumprocessing.com/cgi-bin/dbs/man_trans.cgi). The following parameters are required:

* `username` (your assigned username)
* `password`(the password associated with your username, that can be changed)

(unsure of the following):
* `syspass` (a system password assigned your account, that cannot be changed)
* `action_code` (this uses `D`)
* `order id` (order number of a test transaction

**Note:** All API request methods are `POST` only. In this case, `POST` requests act similarly to `GET` requests, in that the requests function primarily to return information pertaining to a specific resource. 

The content type you'll need to use is `application/x---www---form---urlencoded **or** multipart/form--data`.

#### Understanding Responses

Text to explain returns from different objects.

#### Status Codes

Explanation and table of status codes.

#### Understanding Webhooks

Explanation and examples

### Step 4: Test your Calls

Description

In-app consequences of a return
Payment retries and refunds

# Customers and Accounts

* View customer account information
* Verify customer accounts with Authentecheck
* Initiate and verify micro-deposits


### Merchant Object  [consider renaming if integration partners would use this in a different way than a merchant]

The `merchant` object represents account information pertaining to the merchant that submits a debit or credit transaction.

| Parameter | Description | Type | Req |
|---|---|---|---|
| `parent_id` | Parent ID of merchant. [max Length = 8] | ALPHANUMERIC | Y |
| `sub_id` | Sub ID of merchant. [max Length = 8] | ALPHANUMERIC | Y |
| `pmt_type` | Type of payment being submitted (check, or `chk`, is the default value). | -- | N |
| `response_location` | The `man_trans.cgi` script will respond to this URL with response variables if passed in. | Full path URL | N |


# Submitting a Transaction

The following information outlines the required and optional parfields for submitring a debit or credit transaction to Actum.

It may be helpful to familiarize yourself with the following resources, prior to submitting a transction.

* [ACH Transaction Types]
* [ACH Transaction Lifestyle]

### Account Object

The `Accounts` object represents the bank account information associated with the customer being debited or credited.

| Parameter | Description | Type | Req |
|---|---|---|---|
| `companyname` | The name of business being debited or credited (used when a business account is being debited/credited). [max Length = 64] | ALPHANUMERIC | Y |
| `chk_acct` | The customer's checking account number. [max length = 32] | ALPHANUMERIC | Y |
| `chk_aba` | The customer's ABA, or routing number. This field supports US. routing numbers. [max length = 9]| ALPHANUMERIC | Y |
| `acct_type` | Use one of the following values for this parameter: `C` for checking, or `S` for savings. This field is required for savings accounts only. | -- | N |
| `chk_fract` | Fractional number (Example: `123-45/1234`). [max length = 16] | ALPHANUMERIC | N |
| `chk_number` | The customer's check number. | NUMBER | N |
| `currency` | The type of currency being processed. Only U.S. currency is supported. The default value will reflect `US` if nothing is passed in. | -- | N |

### Consumer Object

The `Consumer` object represents the Know Your Customer (KYC) details associated with the customer, or consumer, being debited or credited.

| Parameter | Description | Type | Req |
|---|---|---|---|
| `custmane` | The consumer's full name (first and last names) [max length = 64] | ALPHANUMERIC | Y |
| `custemail` | The consumer's email address. This field may be required, based on merchant settings. [max length = 64] | ALPHANUMERIC | C |
| ` custaddress1` | The first line of a consumer's street address. This field may be required, based on merchant settings. [max length = 64] | ALPHANUMERIC | C |
| `custaddress2` | The second line of a consumer's street address. [max length = 64] | ALPHANUMERIC | N |
| `custcity` | The city in which the consumer resides. This field may be required, based on merchant settings. [max length = 32] | ALPHANUMERIC | C |
| `custstate` | The state in which the consumer resides. This field may be required, based on merchant settings. [max length = 32] | ALPHANUMERIC | C |
| `custzip` | The consumer's zip code. This field may be required, based on merchant settings. [max length = 16] | ALPHANUMERIC | C |
| `custphone` | The consmer's phone number. This field may be required, based on merchant settings. [max length = 16] | ALPHANUMERIC | C
| `shipaddress1` | The first line of a consumer's shipping address. [max length = 64] | ALPHANUMERIC | N |
| `shipaddress2` | The second line of a consumer's shipping address. [max length = 64] | ALPHANUMERIC | N | 
| `shipcity` | The city included in the consumer's shipping address. [max length = 32] | ALPHANUMERIC | N | 
| `shipstate` | The state included in the consumer's shipping address. [max length = 32] | ALPHANUMERIC | N |
| `shipstate` | The zip code included in the consumer's shipping address. [max length = 16] | ALPHANUMERIC | N |
| `custssn` | The social security details of the consumer. This field may be expressed as the last four digits, or the full social security number. This field may be required, based on merchant settings. [max length = 16] | -- | C |
| `birth_date` | The consumer's birth date, expressed in `MMDDYYYY` format. This field may be required, based on merchant settings. | -- | C | 


### Billing Information

Information about setting up recurring payments (and can expand on how to manage these here, also)

| Parameter | Description | Type | Req |
|---|---|---|---|
| `initial_amount` | The initial amount of a bill payment. The field should be specified in XX.XX format, such as `49.95` for the amount. | -- | Y |
| `recur_amount` | The recurring Amount not required for one-time billing. Default to `initial_amount` if no value is defined. | -- | N |
| `billing_cycle` | A numerical value that corresponds with the frequency with which customer payments will be made. Input values include the following: One-Time Billing = -1, Weekly = 1, Monthly = 2, Bi-Monthly = 3, Quarterly = 4, Semi-Annually = 5, Annually = 6, Bi-Weekly = 7, Business-Daily = 8 | NUMBER | Y |
| `days_til_recur` | The number of days remaining until `recur_amount` is billed | NUMBER | N |
| `max_num_billing` | Maximum number of times consumer will be billed.  Default to “-1” (perpetual billing) if no value is defined. | NUMBER | N |

### Miscellaneous Information

... can we call this an object? Can we integrate this info. into the other sections?

| Parameter | Description | Type | Req |
|---|---|---|---|
| `ip_forward` | The IP address of the client connecting to your server. Max length = 32 | VARCHAR2 | Y |
| `futureinitial` | This field is required for submitting a transaction to originate on a future date. | DATE MM/DD/YYYY | N |
| `merordernumber` | The merchant defined order number.  This field will be saved to the database Max length = 512 | VARCHAR2 | N |
| `action_code` | P = Process (default) | -- | N |
| `creditflag` | Set `creditflag=1` to issue a credit.  **Note:** This is not for refunds, but rather to issue a credit for a transaction that was not initially debited. | NUMBER | N |
| `trans_modifier` | S = Same-day transaction, N = Pre-note transaction, Y = NSF retry | N |
| `retry_fee_amt` | The return fee you'll want to bill on an NSF Retry.  Must be separate than the `initial_amount`. | XX.XX ex. 10.00 | N |

# Payment Retries and Refunds

### Payment Retries

| Parameter | Description | Type | Req |
|---|---|---|---|
| `trans_modifier` | S = Same-day transaction, N = Pre-note transaction, Y = NSF retry | N |
| `retry_fee_amt` | The return fee you'll want to bill on an NSF Retry.  Must be separate than the `initial_amount`. | XX.XX ex. 10.00 | N |

### Payment Refunds

Refunds can only be submitted against the transaction status of `Check Settlement`.

| Parameter | Description | Type | Req |
|---|---|---|---|
| `username` | The merchant's Actum portal username. Max length = 16 | ALPHANUMERIC | Y |
| `password` | The merchant's Actum portal password. Max length = 16 | ALPHANUMERIC | Y |
| `syspass` | The merchant's system password assigned by Actum. Max length = 16 | ALPHANUMERIC | Y |
| `action_code` | You will want to enter `action_code=R` to tell the script we are refunding the transaction. Max length = 16 | ALPHANUMERIC | R |
| `prev_history_id` | The `History_ID` of the transaction you want to refund. | NUMBER | If `order_id` is not provided |
| `order_id` |The order ID of the transaction you want to refund. Max length = 32 | ALPHANUMERIC | Y |
| `initial_amount` | The initial amount of the bill.  Partial refunds are not accepted. | XX.XX ex. 49.95 | Y |
 
# Revoking Transactions

Revoking a transaction will prevent the transaction from being originated to the bank for processing. Standard debits and credits can be revoked until 4pm CT the same day of submission.  Same Day Debits / Credits can be revoked until 11am CT.  If you have the ability to originate transactions using late-night processing, you will have until 9pm CT to revoke.

The response may contain the following parameters:
*	`status=success`
*	`status=Error` 
* `error=Order Number Not Found` (transaction has already originated)

(note that a lot of info. in this section is repetitive)

| Parameter | Description | Type | Req |
|---|---|---|---|
| `username` | The merchant's Actum portal username. Max length = 16 | ALPHANUMERIC | Y |
| `password` | The merchant's Actum portal password. Max length = 16 | ALPHANUMERIC | Y |
| `syspass` | The merchant's system password assigned by Actum. Max length = 16 | ALPHANUMERIC | Y |
| `action_code` | You will want to enter `action_code=K` to tell the script we are revoking the transaction. Max length = 16 | ALPHANUMERIC | Y |
| `prev_history_id` | The `History_ID` of the transaction you want to revoke. | NUMBER | If `order_id` is not provided |
| `order_id` |The order ID of the transaction you want to revoke. Max length = 32 | ALPHANUMERIC | Y |


# Recurring Transactions

### Canceling Recurring Transactions

In order to cancel recurring transactions, the following parameters are required.  Please note that “canceling” is not the same as “revoking” a transaction.

The response may contain the following parameters:

*	`status=success lastdateactive=01/01/2019` (if order is active)
* `status=Error error=Order Inactive!` (if order is already canceled)

When canceling recurring transactions, please note the transaction that is scheduled to originate the same day as the cancel request will still originate to the bank.


| Parameter | Description | Type | Req |
|---|---|---|---|
| `username` | The merchant's Actum portal username. Max length = 16 | ALPHANUMERIC | Y |
| `password` | The merchant's Actum portal password. Max length = 16 | ALPHANUMERIC | Y |
| `syspass` | The merchant's system password assigned by Actum. Max length = 16 | ALPHANUMERIC | Y |
| `action_code` | You will want to enter `action_code=C` to tell the script that we are canceling further recurring transactions. Max length = 16 | ALPHANUMERIC | Y |
| `prev_history_id` | The `History_ID` of the transaction you would like to cancel. | NUMBER | If `order_id` is not provided |
| `order_id` |The order ID of the transaction you would like to cancel. Max length = 32 | ALPHANUMERIC | Y |
| `canceltype` | `canceltype=1` | NUMBER | Y |
| `response_location` | The URL where you would like to store the response. | Full path URL | N |


### Editing Existing Transactions

In order to edit an existing transaction that is scheduled to originate the same day, the following parameters are needed in the request.  Please note that if you change any of the consumer information, it will be updated, as well.

| Parameter | Description | Type | Req |
|---|---|---|---|
| `username` | The merchant's Actum portal username. Max length = 16 | ALPHANUMERIC | Y |
| `password` | The merchant's Actum portal password. Max length = 16 | ALPHANUMERIC | Y |
| `syspass` | The merchant's system password assigned by Actum. Max length = 16 | ALPHANUMERIC | Y |
| `action_code` | You will want to enter `action_code=D` to indicate that this transaction is being updated. Max length = 16 | ALPHANUMERIC | Y |
| `order_id` | The order ID you would like to update. | NUMBER | Y |
| `recur_amount` | The new billing amount for the consumer. | XX.XX ex. 49.95 | Y |
| `billing_cycle` | A numerical value that corresponds with the frequency with which customer payments will be made. Input values include the following: One-Time Billing = -1, Weekly = 1, Monthly = 2, Bi-Monthly = 3, Quarterly = 4, Semi-Annually = 5, Annually = 6, Bi-Weekly = 7, Business-Daily = 8 | NUMBER | Y |   
| `max_num_billing` | The maximum number of times that a consumer will be billed (-1 is for perpetual billing). | NUMBER | Y |
| `next_bill_date` | The date of the next billing. | DATE MM/DD/YYYY | Y |

### Updating Recurring Transactions

To update the billing amount, billing cycle, maximum number of billings, or the next billing date, the following parameters are required.  If any of the parameters are left blank, the adjustments will not take place.  Please note that this request will apply to the transaction scheduled for the following business day.

The response may contain the following parameters:
*	`status=success`
*	`status=error` (with reason for error)

| Parameter | Description | Type | Req |
|---|---|---|---|
| `username` | The merchant's Actum portal username. Max length = 16 | ALPHANUMERIC | Y |
| `password` | The merchant's Actum portal password. Max length = 16 | ALPHANUMERIC | Y |
| `syspass` | The merchant's system password assigned by Actum. Max length = 16 | ALPHANUMERIC | Y |
| `action_code` | You will want to enter `action_code=D` to indicate that this transaction is being updated. Max length = 16 | ALPHANUMERIC | Y |
| `order_id` | The order ID you would like to update. | NUMBER | Y |
| `recur_amount` | The new billing amount for the consumer. | XX.XX ex. 49.95 | Y |
| `billing_cycle` | A numerical value that corresponds with the frequency with which customer payments will be made. Input values include the following: One-Time Billing = -1, Weekly = 1, Monthly = 2, Bi-Monthly = 3, Quarterly = 4, Semi-Annually = 5, Annually = 6, Bi-Weekly = 7, Business-Daily = 8 | NUMBER | Y |   
| `max_num_billing` | The maximum number of times that a consumer will be billed (-1 is for perpetual billing). | NUMBER | Y |
| `next_bill_date` | The date of the next billing. | DATE MM/DD/YYYY | Y |


# Transaction Status

To check the transaction status, the following parameters are required.

The response may contain the following parameters:
* `curr_bill_status`:  PreAuth, Settled, Returned, Declined
*	`refund_status` (if applicable):  Accepted, Pending, Declined 
*	`join_date` 
*	`recurstatus` (only for type=extended):  Active, Inactive   
*	`billing_cycle` (only for type=extended)   
*	`last_billing_date`  (only for type=extended)   
*	`next_billing_date`  (only for type=extended)
*	`error`

| Parameter | Description | Type | Req |
|---|---|---|---|
| `username` | The merchant's Actum portal username. Max length = 16 | ALPHANUMERIC | Y |
| `password` | The merchant's Actum portal password. Max length = 16 | ALPHANUMERIC | Y |
| `action_code` | You will want to enter `action_code=A` to tell the script that you are cancelling further recurring transactions. Max length = 16 | ALPHANUMERIC | Y |
| `prev_history_id` | The `History_ID` from the transaction that you would like to check the status on. Max length = 32 | VARCHAR | If `order_id` is not provided |
| `order_id` |The order ID of the transaction you would like to check the status on. Max length = 32 | ALPHANUMERIC | Y |
| `type` | The transaction type can be either `basic` or `extended` (if neither are provided, then `default=basic`) | -- | N


# Validation Errors

Upon submission, the Actum Processing system will validate each form field.  If all required form fields are valid, the request will be sent to our transaction server.  If a form field is invalid or not supplied as required, the output returned to your script will contain a listing of errors, which are listed below.

* Email address is required.
* Email address is invalid.
* Email address is too long.
* First name is required.
* First name <First Name> is invalid.
* Last name is required.
* Last name <Last Name> is invalid.
* Last name is too long.
* Address is required.
* Address is invalid.
* Address is too long.
* City is required.
* City is invalid.
* City is too long.
* State is required.
* State is invalid.
* State is too long.
* Account Number is required.
* Account Number is invalid.
* Account Number is too long.
* Routing Number is required.
* Routing Number is invalid.
* Routing Number is too long.
* Routing Number must be at least 8 in length.
* Zip Code required.
* Zip Code is invalid.
* Zip Code is too long.
* Zip Code must be at least 5 in length.
* Phone Number is required.
* Phone Number is invalid.
* Phone Number is too long.
* Social Security Number is required.
* Social Security Number is invalid.
* Social Security Number must be at least 4 in length.
* Social Security Number is too long.
* Date of Birth month is required.
* Date of Birth month is too long.
* Date of Birth month is invalid.
* Date of Birth year is required.
* Date of Birth year is too long.
* Date of Birth year is invalid.
* Date of Birth day is required.
* Date of Birth day is too long.
* Date of Birth day is invalid.
* Invalid birth date entered.
 
 
# Decline Codes

| Code | Definition |
|---|---|
| DAR104	| Account number length > 17 |                                                                                  
| DAR105	| Account number contains 123456 |                                                                               
| DAR108	| Invalid ABA Number |                                                                                           
| DAR109	| Invalid Fractional |                                                                                           
| DCR103	| Name scrub |                                                                                                   
| DCR105	| Email blocking |                                                                                               
| DCR106	| Previous scrubbed account (Negative BD) |                                                                      
| DCR107	| Recurring Velocity Check Exceeded |                                                                            
| DDR101	| Duplicate Check indicates that this transaction was previously declined |                                      
| DMR001	| Invalid merchant |                                                                                             
| DMR002	| Invalid billing profile |                                                                                     
| DMR003	| Invalid cross sale ID |                                                                                        
| DMR004	| Invalid Consumer Unique |                                                                                      
| DMR005	| Missing field: `processtype`, `parent_id`, `mersubid`, `accttype`, `consumername`, `accountname`, `host_ip`, or `client_ip` |
| DMR006	| Payment Type Not Supported |                                                                                  
| DMR007	| Invalid Origination Code |                                                                                     
| DMR104	| Merchant not authorized for credit |                                                                           
| DMR105	| Invalid or non-matching original order for `repeat-order-only` subid |                                           
| DMR106	| Invalid Amount Passed In |                                                                                   
| DMR107	| Invalid Merchant TransID Passed In |                                                                           
| DMR109	| Invalid SysPass or Subid |                                                                                     
| DMR110	| Future Initial Billing not authorized for this merchant |                                                      
| DMR201	| Amount over the per-trans limit |                                                                              
| DMR202	| Amount over daily amount limit |                                                                               
| DMR203	| Count over daily count limit |                                                                                 
| DMR204	| Amount over monthly amount limit |                                                                             
| DMR205	| Count over monthly count limit |                                                                               
| DOR002	| A recur has been found for Order |                                                                             
| DOR003	| A return has been found for Order |                                                                           
| DOR004	| Order was not found |                                                                                          
| DOR005	| Order is not active |                                                                                         
| DOR006	| The merchant does not match the order |                                                                      
| DOR008	| Could not find original transaction for orderkeyid |                                                          
| DOR009	| Recur Record not found for keyid |                                                                            
| DOR010	| Multiple transactions found with that TransID |                                                                
| DTA001	| Consumer identity could not be verified |
| DTE200	| Account information could not be verified |                                                                   


# Sample Responses

Sample responses come in two types: `Accepted` and `Declined`.  Each type of response is outlined below in the following sections and can be directed to the same or different scripts, based on preference.  

Responses are not URL encoded and are new-line delimited.  Below is a sample response, which contains the status of the transaction `Accepted` or `declined`, a reason for any declined status, and a set of variables returned from the transaction server, and `PostedVars`, which is a block that contains all variables passed to the Actum Processing system, except for the account information.

### Example Accepted Response

```
status=Accepted
order_id=12345678
history_id=1234567
consumer_unique=/GNmcHNsfsUHE
authcode=CHECK PRE-AUTH:001234567
PostedVars=BEGIN
parent_id=ACTUM
sub_id=SUBID
pmt_type=CHK
custname=John Doe
custemail=alkdj@alkdj.com
custaddress1=123 John Doe Way
custaddress2=
custcity=Sometown
custstate=TX
custzip=78717
custphone=1234567890
initial_amount=1.25
billing_cycle=2
recur_amount=99.99
days_til_recur=14
max_num_billing=6
currency=US
chk_number=1234
PostedVars=END 
```

### Example Declined Response

```
status=declined
reason=Your transaction has been declined.
history_id=9396994
authcode=Invalid ABA Number
PostedVars=BEGIN
parent_id=ACTUM
sub_id=SUBID
pmt_type=CHK
custname=John Doe
custemail=alkdj@alkdj.com
custaddress1=123 John Doe Way
custaddress2=
custcity=Sometown
custstate=TX
custzip=78717
custphone=1234567890
profile_id=	
initial_amount=1.25
billing_cycle=2
recur_amount=99.99
days_til_recur=14
max_num_billing=6
currency=US
chk_number=1234
PostedVars=END 
```


# Tracking a Transaction

The transaction history files contain all initial sales (Check Pre-Auth, Same-day Debit), Returns (Check Return), Funded Debits (Check Settlement), and Refunds / Credits (Check Refund, Same-day Credit) from the previous day.  A transaction history file will come in a flat, quote-qualifier, comma-delimited file, which can either be picked up from our SFTP server or sent to the merchant’s SFTP server. 

The following Operating systems are expecting the following to know when there is an end of line:

* UNIX uses a (LF) Linefeed
* Windows uses a (CRLF) Carriage Return / Line Feed
* The Transaction History File on our server will only have a (LF) Line Feed

If you transfer the file correctly using ASCII on a Windows Machine, you will get a file with (CRLF) Carriage Return / Line Feed. If transferred incorrectly, the file in BINARY will looked garbled and all data will be on the first line.

You will need to download the file in ASCII to make sure there is no data corruption.

## Transaction History File Format

### Returned Variables

The naming format of the transaction history file will be:

`PARENTID-trans-ACTUM-YYYYMMDD.txt` e.g.: `ACTUMTEST-trans-ACTUM-20050212.txt`

The files will contain the following fields:

| Field Name | Description |
|---|---|
| SubID	| Your SubID assigned by Actum Processing |
| Transaction Date |	Date of the transaction |
| Amount |	Amount of the transaction |
| Consumer Name	| Consumer's full name |
| Account Name |	Consumer's account name |
| Transaction Type	| Details the transaction type Check Pre-Auth for preauthorization, Check Return for returned check, Check Settlement for funds that have been received.  Check Refund for refund or credit.  Same-Day Debit for same-day debit.  Same-Day Credit for same-day credit. ACH NOC for notice of change.  Check Pre-Note for pre-note transaction |
| Transaction Result |	Details whether the transaction was approved, declined, or returned |
| Authorization Code	| This is the code that we received from the Consumer's bank |
| Account Type | Description	Will always be check |
| Recurring | Description	Will be initial or recurring |
| Company Name	| Company Name if given during transaction |
| Billing Address |	Consumer Mailing information |
| Billing Address2	| |
| Billing City |	Consumer City |
| Billing State	| Consumer State |
| Billing Zip	| Consumer Zip Code |
| Billing Country | |	 
| Shipping Address | |
| Shipping Address2	 | |
| Shipping City | |	 
| Shipping State	| | 
| Shipping Zip	| | 
| Shipping Country	| | 
| Phone Number |	Consumer Phone Number |
| E-Mail Address |	Consumer E-mail Address |
| IP Address	| The IP address of the consumer |
| Server Referrer	| This field contains referrer information that was submitted during transaction |
| MerchantOrderNumber |	This field contains any extra affiliate code information submitted during transaction |
| Order Number	| Unique key assigned to every order |
| History KeyID	| Unique key associated with each transaction of an order |
| Reference KeyID	| Contains the previous History Keyid |
| Profile KeyID	| If a billing profile keyid was provided it will be listed here |
| Reseller Code	| Used for cross sell transactions |
| Partner Code	| Will contain the partner associated with this transaction |
| Username	| If username is sent, we will include it here |
| ConsumerUniqueID	| Will be used later for offering One-Click sales to current/former consumers |

The file format should be in the order listed above, but here is each field inside example delimiting fields:


"SubID","Transaction Date","Amount","Consumer Name","Account Name","Transaction Type","Transaction Result","Authorization Code","Routing Number","Account Number","Account Type Description","Credit Card Number","Credit Card Expiration Date","Recurring Description","Company Name","Billing Address","Billing Address2","Billing City","Billing State","Billing Zip","Billing Country","Shipping Address","Shipping Address2","Shipping City","Shipping State","Shipping Zip","Shipping Country","Phone Number","E-Mail Address","IP Address","Server Referrer","MerchantOrderNumber","Order Number","History KeyID","Reference KeyID","Profile KeyID","Reseller Code","Partner Code","Username","ConsumerUniqueID"

### Returned Variables Examples

**Note:** There will be no word wrap in the Transaction history files; therefore, each example listed below will actually be on one line.

**Check Pre-Auth:**
"ACTUM01","Jun 28, 2003 12:03AM","6.95","John Doe","John Doe","Check Pre-Auth","Approved","CheckAuth:009999999","HIDDEN","HIDDEN","Check","","","Initial","","123 JohnDoe st","","Johnson City","TX","12345","","","","","","","","(123)123-4567","johndoe@website.com","123.123.123.123","","1000","1234567","1234567","","12345","","",""

**Check Settlement:**
"ACTUM02","Jun 28, 2003 02:21AM","6.95","John Doe","John Doe","Check Settlement","Approved","CheckAuth:009999999","HIDDEN","HIDDEN","Check","","","Initial","","123 JohnDoe st","","Johnson City","TX","12345","","","","","","","","(123)123-4567","johndoe@website.com","123.123.123.123","","1000","1234567","1234567","","12345","","",""

**Check Late Return:**
"ACTUM02","Jun 28, 2003 02:21AM","6.95","John Doe","John Doe","Check Late Return","Declined","Consumer Advises: Not Authorized","HIDDEN","HIDDEN","Check","","","Initial","","123 JohnDoe st","","Johnson City","TX","12345","","","","","","","","(123)123-4567","johndoe@website.com","123.123.123.123","","1000","1234567","1234567","","12345","","",""

**Check Return:**
"ACTUM03","Jun 28, 2003 02:27AM","6.95","John Doe","John Doe","Check Return","Declined","NSF","HIDDEN","HIDDEN","Check","","","Initial","","123 JohnDoe st","","Johnson City","TX","12345","","","","","","","","(123)123-4567","johndoe@website.com","123.123.123.123","","1000","1234567","1234567","","12345","","",""

### Order Tracking

**Persistent Data:** Order Number, SubID
**Reference Data:** History KeyID, Reference KeyID

### Definitions

**Order:** An order is all transactions of Check Pre-Auth, Check Settlement, Check Return, Check Late Return for an order by a consumer.

**Transaction:** This is one particular piece of a transaction as in the Check Pre-Auth, etc.

**Transaction Block:** Is the block of transactions from validating the account / requesting the monies to receiving the monies or receiving a return. One order can have several transaction blocks for the initial transactions and the recurred transactions.

**To Determine Initial Transactions:**  
Take all transactions for a date range then parse them out by Check Pre-Auth where the Reference KeyID is blank and Recurring Description is Initial. This number gives you the total number of initial signups during that time period.

**Refunds:** Refunds can only be issued after a Check Settlement.

**Tracking the Stages of an Order:** Each product sold will have a persistent Order Number throughout the life span of the order, even when it is in a recurring stage. The combination of the Order Number, Reference KeyID and History KeyID will let you track the step-by-step transactions that led to the current status of an order.  

**Linking up Transactions for a Particular Order**

If you get a Check Return but you don’t know where it occurred in the order or from what transaction block, you can use referencekeyid found with the Check Return entry to start the process of finding which block it came from for this particular order. Take this reference keyid and look for a transaction that contains that referencekeyid as the historykeyid. This should return the Check Pre-Auth for which we received the Check Return. You can use this process for any Check Return, Check Late Return, Check Refund, Check Settlement, ACH NOC, etc… until you find a transaction entry that has a blank referencekeyid. This puts you at the beginning of this particular transaction block.

One thing to note is that each time we recur a transaction the Check Pre-Auth will have a blank referencekeyid indicating that a new transaction block is starting. The easiest way to see the transaction blocks in order would be to grab all transactions for a particular orderid and then sort those by date and referencekeyid, which should put those into order from start to finish. Remember, sometimes you may see a Check Settlement for the recurred billing before the initial trial price settles.

Another approach if you wanted to display each transaction block would be to grab all Check Pre-Auth sorted by date with a blank referencekeyid. Then, go through each of those using the historykeyid and find the next transaction in the list by looking for the next transaction that contains that history keyid as the referencekeyid. Grab the history keyid for that transaction and look for the transaction that contains that as the referencekeyid. You can continue this process until you get no more results indicating that you have hit the end of the transaction block and continue with the next transaction block in the list.

Our recommendation is to import everything because the data can be used to your advantage later. Order Number and SubID will always be persistent, and if you sort the transactions by date, you can get a very clear idea of what went on with the account.  In rare cases, we send two transactions per Order Number in one day, but timestamps should show the definitive order.

# Batch Import Specifications

### ACH Transaction File Format

The name of the file will need to begin with “ACH_YOURPARENTID_”. The ParentID will be unique to your account and will be assigned by a merchant support specialist upon integration. The file must be a plain text, ASCII file, and all data items may contain only normal ASCII characters (ASCII 32-126). ASCII control characters (ASCII 0-31), Upper-ASCII characters (ASCII 127-255) or Unicode characters are not allowed. This means foreign language (i.e. non-English) characters are not allowed.
Each transaction must be on its own line after the header record - one line per transaction and one transaction per line - after the header line. The field values must be comma-delimited, and all values must be surrounded by double quotes.
Header Line (Line 1 in the file)

The first line of the file is a header line. This line specifies the fields and the order of the fields in every other line in the file:

"ParentID","SubID","PmtType","TransactionType","CustName","CustPhone","CustEmail","CustAddress1","Cus tAddress2","CustCity","CustState","CustZip","ShipAddress1","ShipAddress2","ShipCity","ShipState","ShipZip"," AccountType","ABANumber","AccountNumber","MerOrderNumber","Currency","InitialAmount","BillingCycle"
,"RecurAmount","DaysTilRecur","MaxNumBillings","FreeSignUp","ProfileID","PrevHistoryID","CheckNumber"," Username","Password","NextBillingDate"

### Field Descriptions:

1.	ParentID (required): This field must contain a ParentID string assigned by Merchant Support to the merchant during the initial set up.

2.	SubID (required): This field must contain a SubID string assigned by Merchant Support to the merchant during the initial set up.

3.	PmtType (required): This field must contain the following value – “CHK”.

4.	TransactionType (required): This field must contain one of the following values:
•	“D” = Debit
•	“C” = Credit
•	“R” = Refund
•	“SD” = Same-day Debit
•	“SC” = Same-day Credit
•	“DN” = Pre-Note
•	“DY” = NSF Retry (see note on “InitialAmount”)

5.	CustName (required): This field must contain the consumer’s or company’s name.

6.	CustPhone (depends on SubID setting – default is required): This field may contain the consumer’s or company’s phone number.
 
7.	CustEmail (depends on SubID setting – default is optional): This field may contain the consumer’s or company’s email address.

8.	CustAddress1 (depends on SubID setting – default is required): This field must contain the consumer’s or company’s address.

9.	CustAddress2 (optional): This field may contain additional address information if it is present, but it is
generally better to leave this blank and put all relevant information in “CustAdress1”.

10.	CustCity (depends on SubID setting – default is required): This field must contain city of residence.

11.	CustState (depends on SubID setting – default is required): This field must contain the state of residence.

12.	CustZip (depends on SubID setting – default is required): This field must contain the zip code of residence.

13.	ShipAddress1 (optional): This field may contain the shipping address if it is different from the billing address.

14.	ShipAddress2 (optional): This field may contain an additional line of the shipping address if it is different from the billing address.

15.	ShipCity (optional): This field may contain the shipping city if it different from the billing city.

16.	ShipState (optional): This field may contain the shipping state if different from the billing state.

17.	ShipZip (optional): This field may contain the ship zip code if different from the billing zip code.

18.	AccountType (required): This field must contain one of the following values –
•	“C” = Checking Account
•	“S” = Savings Account

19.	ABANumber (required): This field must contain the ABA Routing number of the bank account.

20.	AccountNumber (required): This field must contain the bank account number.

21.	MerOrderNumber (optional): This field is usually left blank for batch transaction imports, but it may be used for any extra information regarding the transaction that the merchant may wish to keep track of. Actum will store this information to the database and it will be sent back to the merchant through the daily transaction file.
 
22.	Currency (required): This field must contain the value of “US” – U.S. Dollars.

23.	InitialAmount (required – See note on recurring): This field must contain the amount of the transaction to be processed. This amount must be entered as a decimal amount, for example “29.20” and NOT “29.2”. A value of “29.2” in the field will fail to be imported.

To submit an NSF Fee along with the retry, add a second amount to the “InitialAmount” value delimited with a colon; e.g. to do a 19.95 retry transaction along with a 10.00 NSF Fee, submit “19.95:10.00” for “InitialAmount”.

24.	BillingCycle (required): This field must contain one of the following values:
•	“-1” = One-Time Billing (i.e. no recurring transactions)
•	“1” = Weekly
•	“2” = Monthly
•	“3” = Bi=Monthly (once every 2 months)
•	“4” = Quarterly
•	“5” = Semi-Annually (once every 6 months)
•	“6” = Annually
•	“7” = Bi-Weekly (once every 2 weeks)
•	“8” = Business-Daily

25.	RecurAmount (required if “BillingCycle” indicates periodic billing; optional otherwise – See note on Recurring)
If the “BillingCycle” indicates a periodic billing and the periodic rebilling amount is different from the “InitialAmount”, enter that rebilling amount here. Like the “InitialAmount”, this amount must be
entered as a decimal amount, for example “29.20” and NOT “29.2”. A value of “29.2” in this field will
fail to be imported.

If the “BillingCycle” indicates a One-Time Billing, then this should be left blank, i.e. a double-quoted empty string (“”).

26.	DaysTilRecur (optional): If the “BillingCycle” indicates a periodic billing, then put the number of days after the initial transaction is billed that the first recurring transaction should be billed. If the “BilllingCycle” indicates a One-Time Billing, then this should be left blank, i.e. a double-quoted empty string (“”).

27.	MaxNumBillings (optional): If the “BillingCycle” indicate a One-Time Billing then this should be left blank, i.e. a double-quoted empty string (“”). If the recurring billing is to be continued until canceled, this field should be set to “-1”. If the recurring billing should be for a fixed number of payments then automatically stop, this field should contain the appropriate integer (e.g. “4”)

28.	FreeSignUp (optional): If the “BillingCycle” indicates a periodic billing, then this field should contain a
“1” if the “InitialAmount” is free (i.e. 0.00). Otherwise this field should contain a “0”. If the
“BillingCycle” indicates a One-Time Billing, then this should be left blank, i.e. a double-quoted empty string (“”).
 
29.	ProfileID (optional): This is an option to the itemized billing information fields (InitialAmount, BillingCycle, RecurAmount, DaysTilRecur, MaxNumBillings, FreeSignUp). This option requires a billing profile to be set up by Actum Merchant Support and the ID for that profile given to the merchant. If this value is specified the itemized billing information fields may be left blank, i.e. a double-quoted empty string. ("")

30.	PrevHistoryID (optional): Leave this field blank, i.e. a double-quoted empty string. (“”)

31.	CheckNumber (optional): If you have the check number of the check, put in this field. Otherwise, you may leave this field blank, i.e. a double-quoted empty string. (“”)

32.	Username (optional): If there is a username associated with this record, put it in this field. Otherwise, you may leave this field blank, i.e. a double-quoted empty string. (“”)

33.	Password (optional): If there is a username associated with this record, put it in the field. Otherwise, you may leave this field blank, i.e. a double-quoted empty string. (“”)

34.	NextBillingDate (required if billing date is in the future. See note on recurring.): In this field, if the record is to be billed on a future date, put this date in this field. Format of field is “MM/DD/YYYY”. Otherwise, you may leave this field blank, i.e. a double-quoted empty string. (“”)

**Recurring Note:** If importing recurring transactions that will be billed on a future date, please set the “InitialAmount” field to
“0.00”. “RecurAmount” and “NextBillingDate” will be required.

### Examples

The below is some sample data to illustrate what the file should look like.
•	Record 1 is an initial one-time transaction.
•	Record 2 is a monthly recurring transaction with an initial billing of $29.90 which will recur at $39.90 14 days after the initial billing.
•	Record 3 is a monthly recurring transaction that will bill $39.90 on 12/12/2012.

#### Record 1

"ParentID","SubID","PmtType","TransactionType","CustName","CustPhone","CustEmail","CustAddress1","Cus tAddress2","CustCity","CustState","CustZip","ShipAddress1","ShipAddress2","ShipCity","ShipState","ShipZip"," AccountType","ABANumber","AccountNumber","MerOrderNumber","Currency","InitialAmount","BillingCycle"
,"RecurAmount","DaysTilRecur","MaxNumBillings","FreeSignUp","ProfileID","PrevHistoryID","CheckNumber"," Username","Password","NextBillingDate"
"ACTUM01","TEST01","CHK","C","Joe Q Public","512-555-1234","joe@null.com","100 Main St.","CustAddress2","Austin","TX","00893","","","","","","S","999999999","13371337","","US","29.90","- 1","","","","","","",""

#### Record 2

"ParentID","SubID","PmtType","TransactionType","CustName","CustPhone","CustEmail","CustAddress1","Cus tAddress2","CustCity","CustState","CustZip","ShipAddress1","ShipAddress2","ShipCity","ShipState","ShipZip"," AccountType","ABANumber","AccountNumber","MerOrderNumber","Currency","InitialAmount","BillingCycle"
,"RecurAmount","DaysTilRecur","MaxNumBillings","FreeSignUp","ProfileID","PrevHistoryID","CheckNumber"," Username","Password","NextBillingDate"
"ACTUM01","TEST02","CHK","C","Bob Yakuza","512-555-0893","bob@null.com","893 Ginza","CustAddress2","Austin","TX","00893","","","","","","C","999999999","483219
3828","","US","29.90","2","39.90","14","-1","","","","","","",""

#### Record 3

"ParentID","SubID","PmtType","TransactionType","CustName","CustPhone","CustEmail","CustAddress1","Cus tAddress2","CustCity","CustState","CustZip","ShipAddress1","ShipAddress2","ShipCity","ShipState","ShipZip"," AccountType","ABANumber","AccountNumber","MerOrderNumber","Currency","InitialAmount","BillingCycle"
,"RecurAmount","DaysTilRecur","MaxNumBillings","FreeSignUp","ProfileID","PrevHistoryID","CheckNumber"," Username","Password","NextBillingDate"
"ACTUM01","TEST03","CHK","C","Bob Yakuza","512-555-0893","bob@null.com","893 Ginza","CustAddress2","Austin","TX","00893","","","","","","C","999999999","483219 3828","","US","0.00
","2","39.90","","-1","","","","","","","12/12/2012"

### Decline Codes

Please refer to the following table: [Decline Codes](https://github.com/JillTempelmeyer/jilltempelmeyer.github.io/blob/master/API%20Reference/Submitting%20a%20Transaction.md#decline-codes)

# ACH Transaction Types

Now that you understand the ACH payment flow, this document will introduce you to the different transaction types that are available to your users, and provide an overview of how to get started with them.

## Table of Contents

* [Introduction to Transaction Types](#Introduction-to-Transaction-Types)
   * [Debiting Transaction Types](#Debiting-Transaction-Types)
   * [Debiting and Crediting Transaction Types](#Debiting-and-Crediting-Transaction-Types)
   * [Crediting Transaction Types](#Crediting-Transaction-Types)
* [Submission Deadlines](#Submission-Deadlines)
    * [Through the API](#Through-the-API)
    * [Through the SFTP](#Through-the-SFTP)
* [Debits](#Debits)
* [Same-Day Debits](#Same-Day-Debits)
* [Reinitiated Debits](#Reinitiated-Debits)
* [Pre-Notes](#Pre-Notes)
* [Credits](#Credits)
* [Same-Day Credits](#Same-Day-Credits)
* [Refunds](#Refunds)
* [Micro-Deposits](#Micro-Deposits)

## Introduction to Transaction Types

There are two main categories into which all 8 transaction types fall, based on the movement of money: 

*	**Debiting** (pulling money from a Receiver’s account)
*	**Crediting** (depositing money into a Receiver’s account)  
 
### Debiting Transaction Types

1.	Debits
2.	Same-Day Debits
3.	Reinitiated Debits

### Debiting and Crediting Transaction Type

4.	Pre-Notifications or Pre-Notes

### Crediting Transaction Type:

5.	Credits
6.	Same-Day Credits
7.	Refunds
8.	Micro-Deposits 

Remember, transactions can be submitted to Actum through one of three methods:

* On the web through the Virtual Terminal
* Uploading transaction files via the shared SFTP
* Through a direct API integration. 

 
## Submission Deadlines

### Through the API

Most transactions must be submitted to Actum by **4:00 PM** (Central Time) in order to be included in that day’s batch file for processing.  Transactions that are submitted after that time will be processed the following day. Originators that need a later submission deadline (e.g., West Coast and/or online businesses) can sign up for Actum’s Late-Night Processing service, which pushes back the submission deadline from **4:00 PM to 9:00 PM** (Central). Both submission deadlines allow for transactions to take effect (i.e., be reflected in the Receiver’s bank account) the following banking day, usually at 9:00 AM (RDFI’s local time).

It’s important to note that Actum accepts transactions around the clock and will not decline a transaction for being late; it will simply be included in the next day’s batch.

There are two transaction types that have an earlier submission deadline: **Same-Day Debits** and **Same-Day Credits**.  These transactions need to be submitted to Actum by 11:00 AM (Central) in order to take effect by 4:00 PM (Central) later that day.  

### Through the SFTP

Transaction files submitted to us through the SFTP can take longer to process prior to being sent to the ODFI. Therefore, the submission deadlines are 30 minutes prior to the API cutoff times, as shown in the following details:

*	Regular transactions must be submitted by **3:30** PM (Central)
*	Late-Night transactions must be submitted by **8:30** PM (Central)
*	Same-Day transactions must be submitted by **10:30AM** (Central)

## Debits

ACH Debits are used to pull money from the Receiver’s account.  They are the most common transaction type.
Each Debit transaction must include the following data:

1.	Receiver’s Full Name (including the Company Name for B2B transactions)
2.	Receiver’s Bank Account and Routing Numbers
3.	Amount to be Debited
4.	IP Address of the client connecting to your server

In addition to having all the right data fields completed, transactions must not exceed certain **exposure limits**. These are maximums that are set based on historical and expected transaction activity, and are meant to limit the ACH Network’s exposure to the risk of excessive or fraudulent transactions.

Exposure limits are different for every Originator, and it’s the Originator’s job to stay within those limits.  Transactions that exceed an exposure limit will be declined by Actum automatically, which could cause unnecessary payment delays for the Originator.

**Note:**  To help your clients avoid such delays, Actum recommends that you help them keep track of their exposure limits, which are available through our Exposure Limits API.  Here, you can set up alerts for when a client is getting dangerously close to an exposure limit, so that he/she can proactively contact Actum to request a limit increase.  

There are five exposure limits:

*	Maximum dollar amount per transaction
*	Maximum dollar amount per day
*	Maximum dollar amount per month
*	Maximum transaction count per day
*	Maximum transaction count per month

## Same-Day Debits

Similar to regular ACH debits, **Same-Day Debits** have the same requirements, and are subject to the same exposure limits, as regular ACH Debits.  The only difference is the submission deadline (11:00 AM instead of 4:00 PM, Central) and the effective date (today instead of tomorrow morning).  They must also be designated for same-day processing in the API request or file.

The data requirements are spelled out in greater detail in our [Integration Guide](Link) and [File Import Specifications](Link).

**Note:**  Because Actum does not decline late transactions, and instead includes them in the next batch file, it may be helpful for your software solution to include an automated post-submission message letting your client know the submission was late and will therefore take effect on the following banking day instead of later that day.

## Reinitiated Debits

There are two kinds of **Reinitiated Debits**: 

* **Stopped Payment Retries**, which are used when a Debit transaction failed due to the following ACH Return Code:
  *	`R08` for Payment Stopped (the Receiver has placed a stop payment order on this debit Entry)
* **NSF Retries**, which are used to reinitiate previously failed Debit transactions resulting from one of two qualifying ACH Return Codes: 
  *	`R01` for Insufficient Funds (the Receiver’s available balance is not sufficient to cover the dollar value of the debit Entry), and
  * `R09` for Uncollected Funds (the Receiver has a sufficient ledger balance to satisfy the dollar value of the transaction, but the available balance is below the dollar value of the debit entry).
  
If a Debit transaction fails due to ACH Return Code `R08`, the Originator must receive separate authorization from the Receiver to reinitiate the Debit.  

For `R01` and `R09`, while a separate authorization is not required, it is considered a best practice for the Originator to follow up with their customer (the Receiver) to arrange a future date for the NSF Retry.

**Note:** An Originator is limited to 2 Reinitiated Debits and must submit them within 180 days of the initial Debit.  
NACHA requires that these transactions be identified as Reinitiated Debits rather than submitted as new transactions.  Any fees that are assessed by the Originator must also be clearly identified or explained at the time of the initial authorization.  Actum recommend using the following, or substantially similar, language:

* _“If your payment is returned unpaid, you authorize us to make a one-time electronic fund transfer from your account to collect a fee of [$ ];”_ or 
* _“If your payment is returned unpaid, you authorize us to make a one-time electronic fund transfer from your account to collect a fee. The fee will be determined [by/as follows]: [ ].”_ 

Actum recommends that you create an action (allowing your users to reinitiate a previous failed transaction) that turns on automatically, upon the receipt of a qualifying ACH Return Code.  The action should include fields where your users can enter a return fee and a future date for the Reinitiated Debit.  Your system should also disable the action based on the number of attempts (two maximum) and the time that has elapsed (180 days).  Actum's developer support team will offer guidance on how best to program this action in your software solution.

## Pre-Notes

**Pre-Notes** are zero-dollar transactions that are used to validate the Receiver’s bank account number.  They precede the authorized Debit or Credit transaction by three banking days.

An RDFI that receives a Pre-Note has three days to return it or to provide the ODFI with a **Notification of Change (NOC)**. 
NOCs are a type of return that the RDFI sends when they accept a transaction despite there being minor errors in the data. 

For example, if the RDFI was able to locate the Receiver’s account based on the submitted information, but the account number was slightly off, they would send an NOC (with the correct account number) to the ODFI. As part of our service, Actum will automatically apply those corrections in the subsequent debit transaction and in our database.

If the Pre-Note does not get returned by the end of Day 3, the account will have been validated, and the accompanying Debit or Credit Entry will go out automatically. Similarly, if the Pre-Note does get returned, then the Entry will not be processed and the Originator should follow up with the Receiver to get the correct information.

_While using Pre-Notes does delay fund settlement by three additional days, it’s considered a best practice. In fact, starting September of 2019, NACHA will require Originators to validate all newly authorized bank account numbers for web transactions using commercially reasonable methods.  And while there are some cool API-driven online bank account verification services to accomplish this (e.g., Plaid, Yodlee, Quovo, MicroBilt, etc.), Pre-Notes are the only full-coverage option available._

**Note:** Because a Pre-Note transaction must also include an authorized Debit or Credit, they are not submitted as two separate Entries, but rather, as one normal Entry with the authorized amount (subject to the same rules and exposure limits) and a special designation to be Pre-Noted.

The data requirements are spelled out in greater detail in our [Integration Guide](Link) and [File Import Specifications](Link).

## Credits

**ACH Credits** are used to deposit money into the Receiver’s account.  

The most important rule to understand here is that Credit transactions must be pre-funded.  Not all Originators will utilize ACH Credits, but the ones that do will understand that they must maintain a Credit Reserve Balance in their Actum account to fund their submitted Credit transactions.

The Credit Reserve Balance must be separately funded by one of several options: 

* Wires initiated by the Originator
Reverse wires authorized by the Originator and initiated by Actum
* ACH debits initiated by Actum from the Originator’s bank account
* Transfers from the Originator’s settled Debits before they are paid out.

Actum automatically declines any Credit Entries submitted through the API that would cause the Credit Reserve Balance to go negative.  

The same information that’s required for an ACH Debit transaction is also required for an ACH Credit transaction (e.g., Receiver’s name, bank account details, transaction amount, etc.).  Unlike Debits however, Credits do not have the same exposure limits, unless the Originator requests them.  

**Note:**  Actum recommends that you use our [Credit Reserve API](Link) to display an up-to-date balance as a reference point for your clients. 

## Same-Day Credits

**Same-Day Credits** are submitted just like normal Credit Entries.  They are subject to the same Credit Reserve Balance requirement as normal Credits.  The only difference is the same-day designation and the earlier submission deadline.

How these transactions get designated as same-day Entries will be further spelled out in our [Integration Guide](Link) and [File Import Specifications](Link).

**Note:** Currently, NACHA limits the transaction size for Same-Day Credits to $25,000 per Entry.  Effective March 20, 2020, NACHA will increase the per-transaction dollar limit to $100,000.

## Refunds

**Refunds** are a type of Credit transaction back to the Receiver.  
So far, all the transaction types we’ve reviewed are submitted through a single API: Actum’s Submit API. Refunds, however, are submitted through a separate Refund API.

Because Refunds can only be issued against a previously settled Debit transaction, the required data are limited to that previous transaction’s unique IDs (generated by Actum) and the amount to be refunded.

Currently, our system does not allow for partial Refunds and the amount to be refunded must equal the amount of the initial Debit transaction.  Partial Refund functionality will be announced in the near future.

**Note:**  Actum recommends creating a Refund action that gets enabled for each Debit or Same-Day Debit transaction upon settling.  All previous transactions should be stored and easily searchable so that if your users get a Refund request from the Receiver, they can process it with a click of a button.

## Micro-Deposits

**Micro-Deposits**, while not as common as they used to be, can be a useful verification tool for certain applications.  

It’s easy enough for someone to steal another person’s bank account information and use that to fraudulently pay the Originator for services.  To protect against that, some Originators will submit a Micro-Deposit transaction, which includes two separate amounts (usually a few pennies), and ask the Receiver to report back those amounts.  If the amounts match up, then the Originator has verified that the bank account is indeed the Receiver’s. 

**Note:**  This is the one transaction type that is optional for our software partners to accommodate.  If you think it would be a useful addition to your software solution, let us know and we’ll help you build it out.

Now that you understand each transaction type, you’re ready to delve into our [Integration Guide](Link) (or [File Import Specifications](Link), depending on how you want to submit transactions to Actum).

Once you review those documents, we will go over the Reporting Requirements once a transaction gets submitted, including the various unique IDs that are generated by Actum that must be permanently associated with their respective transactions in your system.

Finally, we will go through our **Actum Partner Certification Checklist** together to make sure that your solution provides the smoothese ACH payment processing experience possible to your clients.

# Understanding the ACH Payment Flow

Before embedding a software or web-based solution to facilitate Automated Clearing House (ACH) payments, you'll want to make sure that you understand how the ACH payment flow works.  The rules and processes around ACH will impact the features you build and how you communicate the status of a transaction. 

This document will briefly introduce you to the ACH payment flow and how it relates to Actum's ACH processing procedures and policies.

## Table of Contents

* [Introduction](#introduction)
* [How ACH Works](#how-ach-works)
* [ACH Returns](#ach-returns)
* [Batch Processing](#batch-processing)
* [How Actum Transactions Work](#how-actum-transactions-work)
* [Late Returns](#late-returns)
* [Using Actum outto Facilitate ACH Payments](#using-actum-to-facilitate-ach-payments)
* [Actum's API](#actums-api)

## Introduction

Before building out a software or web-based solution to facilitate Automated Clearing House (ACH) payments, it is first important to understand how the ACH payment flow works.  The rules and processes around ACH will impact the features you build and how you communicate the status of a transaction. 


The ACH Network is managed by **NACHA** and is made up of banks and credit unions, called depository financial institutions.  Only depository financial institutions can transmit transaction data to the Federal Reserve (or the Electronic Payments Network, another ACH Operator), and they do so in batches throughout the day.  

**Note:** _NACHA is the governing body that establishes and enforces the processes and rules for ACH transactions._

## How ACH Works

In the world of ACH Processing, there’s **Originating** and there’s **Receiving**.  

For the purposes of understanding the ACH payment flow, it can be helpful to think of these actions as describing the movement of transaction data (and not the actual money).  Whether a merchant collects or sends funds from a customer, the merchant's business is the **Originator**, and its customer the Receiver.  

_The Originator is an individual or entity that has received authorization from the Receiver to initiate a direct payment (ACH debit) or direct deposit (ACH credit) over the ACH Network._

Not all originating merchants have ACH originating capability with their depository financial institutions.  In fact, most businesses require an intermediary with an established relationship at an **Originating Depository Financial Institution (ODFI)** in order to originate transactions. In this case, that intermediary is Actum Processing. 

With an intermediary involved, the Originator will submit a transaction to Actum, which will then send that data to its ODFI, and transmit that data to the Federal Reserve or other ACH Operator.  

As an example, let’s say that the customer’s bank account is at Wells Fargo.  In this case, Wells Fargo would be the Receiving Depository Financial Institution (RDFI).  If this transaction were an ACH debit for $100, Wells Fargo would see its ledger at the Federal Reserve decrease by $100, automatically, while the ODFI would see an increase by $100 (if this were an ACH credit, Wells Fargo would see its ledger increase, while the ODFI would see a decrease).  This increase or decrease should be further reflected in the individual accounts at the different banks.   

## ACH Returns

In most cases, an RDFI has two business days to object to a transaction and take back the funds from the ODFI.  This objection comes in the form of an ACH Return Code.  
For example, if the customer’s account had insufficient funds or simply didn’t exist, Wells Fargo would send the ACH Return Codes `R01` or `R03`, respectively, to Actum’s ODFI and the transaction would be reversed, leading to a failed transaction.  There are many reasons why a transaction might be returned, and sometimes customers have up to 60 days to dispute a charge, which could reverse a transaction that had already settled.

**Note:**  When there’s a return due to insufficient funds, the business that received the return can follow up with the customer and resubmit the transaction. However,it must not be submitted as a new transaction. Per NACHA rules, the transaction must be submitted as a `Retry PYMT`, which may include the addition of a retry fee in order for the merchant to recoup the return fee that Actum passes on from its ODFI (such as a bounced check fee).  

Therefore, your software (or web) solution should account for this requirement.

Refer to this list of [85 ACH Return Codes](Placeholder for Document), so that your software can translate them in a way that allows the user to quickly take action, such as contacting the customer).

## Batch Processing

As you can see, ACH doesn’t happen in real-time. While Actum helps streamline ACH processing as much as possible, it is not a fully-automated process.

Not only is the process somewhat manual because the RDFI can return a transaction, even after the money technically “changed hands” between banks, but also because ODFIs use a batch processing system.  

**Batch processing** occurs when an ODFI waits to aggregate all incoming transaction data into a single batch file before transmitting it to the Federal Reserve at regular intervals throughout the day.  Similarly, ACH Return Codes are also batched before being transmitted from the ODFI to Actum at regular intervals throughout the day.

Actum operates by a batch processing system.  This can be helpful to understand, as there is typically a buffer zone between when the Originator submits their transaction data and when Actum sends it to the ODFI. As a result, the Originator can edit or revoke a recently submitted transaction.  It also means that the status of a transaction can change only at predetermined times throughout the day.

## How Actum Transactions Work

A transaction that you submit to Actum can get accepted or declined. However, being accepted by Actum doesn not mean that the transaction cleared. Rather, it means that Actum's system automatically approved it for transmission to an Actum ODFI.

**Note:** If a transaction submitted through Actum's API gets declined, a response code that details the reason for the decline will be generated automatically.

Once a transaction is accepted by Actum, its status will remain `pending` until one of two things happens:

1. the transaction settles (a predetermined time period, or settlement period, has elapsed), or
2. the transaction fails (an ACH Return Code is received during the settlement period).

All accepted transactions will settle, as long as an ACH Return Code is not received by the end of its settlement period.  
If the transaction settles, it will do so at 2:00PM (Central Time) on the last day of its settlement period. The status will change from `pending` to `settled` at 2:00PM, as a result.  The Originator can then expect to receive their associated funds on the following business day, depending on how their account is setup.

If an ACH Return Code is received before the end of the settlement period, the transaction will fail. In this case, the failure may not be reflected in its status immediately.  Because of the batch processing system, it can take a few hours between when an RDFI returns a transaction, notifies the ODFI, and when the ODFI notifies Actum, and in turn the Originator.

Actum updates its files twice a day, once at 6:00AM (which would include any returns from the past 24 hours) and again at 4:00PM (which would include any other returns that might have come in until 3:00PM that day). Ultimately, for failed transactions, the status can only change either at 6:00AM or 4:00PM.

These times are important to note, because Originators want to know as soon as the information is available, if a transaction failed, so that they can act on it (e.g., follow up with the customer, suspend delivery of service, etc.).  

**Note:**  To meet the evolving expectations in the software industry, we are currently developing webhooks to push status changes to you as they happen.  Until then, we can only provide statuses on-demand through an API call.  Traditionally, it has been up to the Originator (or the software partner facilitating payments for the Originator) to develop their own status update protocols on their platform based on:

* Their own settlement date calculations, and
* Parsing through their clients’ transaction history files (provided through an SFTP on a daily or twice daily basis) to match return line items with their respective transactions using their Reference Key IDs.  

## Late Returns

What happens when an ACH Return Code comes in after the settlement period ends?  

First, Actum will advocate on your behalf to dishonor the return, if applicable.  If the return is legitimate, however, then it will be considered a Late Return and deducted from that day’s settlement calculation. 

As an example, if you had 10 transactions of $20 each, scheduled to settle today, and there were no returns by 2:00PM, the full $200 would settle and be paid out to the Originator.  If a legitimate return for one of those transactions is received later that day or tomorrow, and you have another $200 scheduled to settle tomorrow, only $180 would end up settling tomorrow ($200 settlement LESS the $20 late return).

## Using Actum to Facilitate ACH Payments

There are three main ways to interact with Actum:

1.	On the web through our Virtual Terminal
2.	Via SFTP to upload transaction files and download history files
3.	Through a direct API integration

Many of Actum's software partners and web merchants use a combination of the last two methods, by pushing transactions to Actum in real-time through an API call, then pulling transaction history files from us at scheduled intervals (6:00AM and 4:00PM) through a shared SFTP.

Some merchants use payment management software that is not directly integrated with Actum. Those merchants will often use the SFTP method to upload transaction files, or the Virtual Terminal to manually enter transactions and access their reports. 

## Actum's API

The following actions are available through our APIs:

* Submit transactions
* Validate a customer’s bank account
* Refund a transaction
* Edit or revoke a recently submitted transaction before it gets sent to the ODFI
* Cancel or update a recurring transaction

You can reference our APIs in our [Integration Guide](Placeholder for link to integration guide).

There are several transaction types that your software (or web) solution should accommodate:
*	Debits
*	Credits
*	Same-day Debits
*	Same-day Credits
*	Refunds
* Pre-Notes
* NSF Retries



# Introduction

Welcome to the Kittn API! You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/lord/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

