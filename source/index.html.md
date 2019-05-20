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

