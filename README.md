# razorpay-pos-payment-react-native-sdk

You can now Integrate Razorpay POS Payment Gateway in your Android application by using Razorpay POS Android SDK with easy steps and start accepting payments.
With this Android SDK, developers who have existing android native/hybrid (React Native) apps, can integrate Razorpay PoS solution with a native android SDK implementation

## Prerequisites

* Create a Razorpay PoS account with the Razorpay PoS Team.
* Get API Keys from the Razorpay PoS Team. To go live with the integration and start accepting real payments, generate Live Mode API Keys and replace them in the integration.
* Know about Razorpay PoS Payment Flow.

## Getting started

`$ npm install react-native-ezetap-sdk --save`

### Mostly automatic installation

`$ react-native link react-native-ezetap-sdk`

### Manual installation

#### Android

1. Open  `node_modules`
    Add `react-native-ezetap-sdk@x.x.x` folder
2. Open up `android/app/src/main/java/[...]/MainApplication.java`
  - Add `import com.reactlibrary.RNEzetapSdkPackage;` to the imports at the top of the file
  - Add `new RNEzetapSdkPackage()` to the list returned by the `getPackages()` method
3. Append the following lines to `android/settings.gradle`:

    ```gradle
  	include ':react-native-ezetap-sdk'
  	project(':react-native-ezetap-sdk').projectDir = new File(rootProject.projectDir, 	'../node_modules/react-native-ezetap-sdk/android')
  	```
4. Insert the following lines inside the dependencies block in `android/app/build.gradle`:
  	```gradle
      implementation project(':react-native-ezetap-sdk')
  	```
5. Open up `android/app/src/main/AndroidManifest.xml`
  - Add `tools:replace="android:allowBackup"` in `application` tag

    ```xml
     <application
        android:name=".MainApplication"
        android:allowBackup="false"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:theme="@style/AppTheme"
        tools:replace="android:allowBackup">
    ```

## How to use

It's very simple and easy to call all the APIs available in our SDK  :

## Initialization API

```javascript
RNEzetapSdk.initialize(JSON.stringify(json));
```
The first API that needs to be integrated with is the “Initialize” API, this API performs the following 3 key activities:-
 * Initializes the SDK with global configuration settings
 * Connects to the appropriate Razorpay server based on Application mode (AppMode) = DEMO/ PROD
 * Connects to the appropriate merchant account, this depends on the app key entered

Below is the request code for API with parameters

<details>
<summary>Code Snippet</summary>

```javascript
import RNEzetapSdk from 'react-native-ezetap-sdk';
var json = {
        "appMode": "Your environment",
        "merchantName": "merchantName",
        "demoAppKey": "Your demo app key",
        "prodAppKey": "Your prod app key",
        "userName": "userName",
        "currencyCode": 'INR', 
        "captureSignature": 'true',
        "prepareDevice": 'false',
        "captureReceipt": 'false'
      };
```
</details>

<details>
<summary>Keys Information</summary>


| **ATTRIBUTES**               | **DESCRIPTION**           | **MANDATORY**   | 
| -----------              | -----------           | ----------- |      
| **appMode**           | Add Demo/Prod appmode | Yes         | 
| **merchantName - String(80)** | Merchant name provided to every merchant by Razorpay PoS is part of your account credentials|   Yes     |
| **demoAppKey - String(50)**  | Demo app key provided by Razorpay PoS Team | Yes (In case of demo integration)         | 
| **prodAppKey - String(50)**  | Prod app key provided by Razorpay PoS Team|   Yes (In case of prod integration)     |
| **userName - String(20)**    | Username provided by Razorpay PoS Team| Yes         | 
| **currencyCode**     | Currency code|   No     |
| **captureSignature - Boolean**| If you want to capture the signature is userId| No| 
| **prepareDevice - Boolean**  |  | No         | 
| **captureReceipt - Boolean**| if you want to capture receipt  |   No     |

</details>

## Prepare Device API

```javascript
RNEzetapSdk.prepareDevice();
```
Prepare Device is used to initialize the device (card reader) with the updated encryption keys from the corresponding bank

This API doesn't need any request parameters

## Send Receipt API

```javascript
await RNEzetapSdk.sendReceipt(JSON.stringify(sendReceiptJson));
```
Ezetap provides a way to send e-receipts to customers. You can pass mobile, email respectively as part of object.

Below is the request code for API with parameters

<details>
<summary>Code Snippet</summary>

```javascript
import RNEzetapSdk from 'react-native-ezetap-sdk';
 var sendReceiptJson = {
        "customerName": "customerName",
        "mobileNo": "mobileNo",
        "email": "emailId",
        "txnId": "transactionID"
      };
```
</details>

<details>
<summary>Keys Information</summary>

| **ATTRIBUTES**               | **DESCRIPTION**           | **MANDATORY**   | 
| -----------              | -----------           | ----------- |      
| **txnId** | The transaction Id of the transaction | Yes         | 
| **mobileNo** | Mobile number of the user |   Yes     |
| **email**  | Email id  of the user  | Yes        | 
| **customerName**  |  Name of the user  | No        | 

</details>

## Service Request API

```javascript
RNEzetapSdk.serviceRequest(JSON.stringify(json));
```
Razorpay provides a way to send service on request to customers. You can pass merchnat mobile number, email , issue type, issue info respectively as part of object.

Below is the request code for API with parameters

<details>
<summary>Code Snippet</summary>

```javascript
import RNEzetapSdk from 'react-native-ezetap-sdk';
  var json = {
        "issueType": "issueType",
        "issueInfo": "issueInfo",
        "tags": [
          "tag1","tag2"
        ]
  };
```
</details>
<details>
<summary>Keys Information</summary>

| **ATTRIBUTES**               | **DESCRIPTION**           | **MANDATORY**   | 
| -----------              | -----------           | ----------- |      
| **issueType**  | Type of the issue fro the request  | No        | 
| **issueInfo**  | Information about the issue  | No        | 
| **tags**  | Tags related to the issue  | No        | 

</details>

## Search Transaction API

```javascript
RNEzetapSdk.searchTransaction(JSON.stringify(json));
```
Razorpay provides a way to search transaction. You can pass agent name and save locally respectively as part of object.

Below is the request code for API with parameters

<details>
<summary>Code Snippet</summary>

```javascript
import RNEzetapSdk from 'react-native-ezetap-sdk';
  var json = {
        "agentName": "name",
        "saveLocally": false
  };
```
</details>
<details>
<summary>Keys Information</summary>

| **ATTRIBUTES**               | **DESCRIPTION**           | **MANDATORY**   | 
| -----------              | -----------           | ----------- |      
| **agentName**  | Name of the agent  | No        | 
| **saveLocally**  | If you want to saev it locally  | No        | 

</details>

## Get Transaction API

```Java
RNEzetapSdk.getTransaction(JSON.stringify(json));
```
This API is used to get the transaction details with reference.

Below is the request code for API with parameters
<details>
<summary>Code Snippet</summary>

```javascript
import RNEzetapSdk from 'react-native-ezetap-sdk';
  var json = {
        "amount": "100",
        "options": {
          "amountTip": 0.0,
          "references": {
            "reference1": "sffr",
            "additionalReferences": [
      
            ]
          },
          "customer": {
          },
          "serviceFee": -1.0,
          "addlData": {
            "addl1": "addl1",
            "addl2": "addl2",
            "addl3": "addl3"
          },
          "appData": {
            "app1": "app1",
            "app2": "app2",
            "app3": "app3"
          }
        }
      };
```
</details>
<details>
<summary>Keys Information</summary>

| **ATTRIBUTES**               | **DESCRIPTION**           | **MANDATORY**   | 
| -----------              | -----------           | ----------- |      
| **amount** | Transaction Amount| No         | 
| **amountTip** | Amount Tip |   No     |
| **references**  | Transaction reference  | No        | 
| **customer** | Customer Information |   No     |
| **addlData** | Additional Data|   No     |
| **appData**  | App data   | No        | 

</details>

## Check For Incomplete Transaction API

```Java
RNEzetapSdk.checkForIncompleteTransaction(JSON.stringify(json));
```
In case of incomplete transaction for a user, the user is intimated about the status of the previous transaction. The App will prompt the user to check the status of the previous transaction before attempting a new transaction. The API will return details of the transaction (Status) as well.

This request does not required any parameters

## Void Transaction API

```Java
RNEzetapSdk.voidTransaction(transactionID);
```
If the customer choose to return the service and you wish refund the money on the same day, in this case you can do void of a payment. Voiding a payment means that you cancel the payment before the settlement of money is made. If settlement is initiated then void won't work, this API is helpful if same day refund needs to be done

Below is the request code for API with parameters

<details>

<summary>Code Snippet</summary>

```javascript
import RNEzetapSdk from 'react-native-ezetap-sdk';
var transactionID = "order123"
```
</details>

<details>
<summary>Keys Information</summary>

| **ATTRIBUTES**               | **DESCRIPTION**           | **MANDATORY**   | 
| -----------              | -----------           | ----------- |      
| **trasactionId** | Transaction id of the void transaction| Yes         | 

</details>

## Attach Signature API

```Java
RNEzetapSdk.attachSignature(transactionID);
```
This API allow you to attach an e-signature from the customer for payments.

Below is the request code for API with parameters

<details>

<summary>Code Snippet</summary>

```javascript
import RNEzetapSdk from 'react-native-ezetap-sdk';
var transactionID = "order123"
```
</details>
<details>
<summary>Keys Information</summary>

| **ATTRIBUTES**               | **DESCRIPTION**           | **MANDATORY**   | 
| -----------              | -----------           | ----------- |      
| **trasactionId** | Transaction id of the void transaction| Yes         | 

</details>


## Pay API

```Java
RNEzetapSdk.pay(JSON.stringify(json));
```
This API is used to pay for transactions with different modes like creedit card, debit card, cash, cheque, UPI etc.

Below is the request code for API with parameters

<details>

<summary>Code Snippet</summary>

```javascript
import RNEzetapSdk from 'react-native-ezetap-sdk';
var json = {
    "amount": "123",
    "options": {
      "serviceFee": 100,
      "paymentBy": "CREDIT OR DEBIT OR ANY (**To be used only if the service fee is being added.)",
      "paymentMode": "Card/Cash/Cheque/UPI/UPI_VOUCHER/RemotePay/BHARATQR/Brand_Offers/Brand_EMI/Normal_EMI/Wallet ",
      "providerName": "<NBFC> eg. ZestMoney. (**providerName and emiType are to be passed only if user wants to use ZestMoney. In this scenario, set \"paymentMode”:”EMI”)",
      "emiType": "NORMAL, BRAND, EMI",
      "references": {
        "reference1": "1234",
        "additionalReferences": [
          "addRef_xx1",
          "addRef_xx2"
        ]
      },
      "appData": {
        "walletAcquirer": "freecharge/ola_money/ etc.(**walletAcquirer are to be passed only if user sets \"paymentMode”:”Wallet”)"
      },
      "customer": {
        "name": "xyz",
        "mobileNo": "1234567890",
        "email": "abc@xyz.com"
      }
    }
  };
```
</details>

<details>
<summary>Keys Information</summary>

| **ATTRIBUTES**               | **DESCRIPTION**           | **MANDATORY**   | 
| -----------              | -----------           | ----------- |      
| **amount**     | Amount to be paid | Yes         | 
| **serviceFee** | Service fee for   |   Yes     |
| **paymentBy**  | Credit or debit or any other | Yes (In case of demo integration)         | 
| **paymentMode**  | It can be Card/Cash/Cheque/UPI/UPI_VOUCHER/RemotePay/BHARATQR/Brand_Offers/Brand_EMI/Normal_EMI/Wallet|   Yes |
| **emiType**    | Type of EMI| No         | 
| **references**     | Additional references|   No     |
| **appData**| app data| No| 
| **customer**  | Customer information | No         | 
| **name**| Name of the customer  |   No     |
| **mobileNo**|  Mobile number of the customer |   No     |
| **email**|  Email of the customer  |   No     |

</details>

  
## Print Receipt API

```Java
RNEzetapSdk.printReceipt(transactionID);
```
You can use below API to print Razorpay PoS's payment receipt or charge-slip

Below is the request code for API with parameters

<details>

<summary>Code Snippet</summary>

```javascript
import RNEzetapSdk from 'react-native-ezetap-sdk';
var transactionID = "order123"
```
</details>

<details>
<summary>Keys Information</summary>

| **ATTRIBUTES**               | **DESCRIPTION**           | **MANDATORY**   | 
| -----------              | -----------           | ----------- |      
| **trasactionId** | Transaction id of the transaction to be printed| Yes         | 

</details>

## Print Bitmap API

```Java
RNEzetapSdk.printBitmap(base64ImageString);
```
You can use this API to print custom receipt or invoice images you would like to.

Below is the request code for API with parameters

<details>

<summary>Code Snippet</summary>

```javascript
import RNEzetapSdk from 'react-native-ezetap-sdk';
var base64ImageString = ""
```
</details>

<details>
<summary>Keys Information</summary>

| **ATTRIBUTES**               | **DESCRIPTION**           | **MANDATORY**   | 
| -----------              | -----------           | ----------- |      
| **base64ImageString** | Image data to print bitmap| No         | 

</details>

## Logout API

```Java
RNEzetapSdk.logout();
```
You can use this API to logout form the application.

This API doesn't need any request parameters

## Stop Payment API

```Java
RNEzetapSdk.stopPayment(JSON.stringify(json));
```
This API can be used to stop the payment for the list of transactions. You need to pass a list of transaction ids in this API.

Below is the request code for API with parameters
<details>

<summary>Code Snippet</summary>

```javascript
import RNEzetapSdk from 'react-native-ezetap-sdk';
var json = {"txnIds":[""]};
```
</details>

<details>
<summary>Keys Information</summary>

| **ATTRIBUTES**               | **DESCRIPTION**           | **MANDATORY**   | 
| -----------              | -----------           | ----------- |      
| **txnIds** | A list of string ids for which payment needs to be stopped. | Yes         |

</details>

 ## Scan Barcode API

 ```Java
RNEzetapSdk.scanBarcode();
```
You can use this API to scan barcode 

This API doesn't need any request parameters

## Refund Transaction API

 ```Java
RNEzetapSdk.refundTransaction(JSON.stringify(json));
```
To initiate the refund for the transaction this API can be used. You have to fill in the required details of the transaction and call the API to initiate a refund.

Below is the request code for API with parameters

<details>

<summary>Code Snippet</summary>

```javascript
import RNEzetapSdk from 'react-native-ezetap-sdk';
var json = {
       "amount": "100",
       "txnId": "transactionID"
};
```
</details>

<details>
<summary>Keys Information</summary>
| **ATTRIBUTES**               | **DESCRIPTION**           | **MANDATORY**   | 
| -----------              | -----------           | ----------- |      
| **amount** | Amount of the transaction | Yes         |
| **txnId** | Transaction Id of the transaction | Yes         |
</details>

 ## Check for updates API

 ```Java
RNEzetapSdk.checkForUpdates();
```
This API is used to Check for service application updates

This API doesn't need any request parameters

## Java/Kotlin

[https://github.com/AtifQEzetap/razorpay-pos-payment-sdk](https://github.com/AtifQEzetap/razorpay-pos-payment-sdk)

## Flutter

https://github.com/AtifQEzetap/razorpay-pos-payment-flutter-sdk

## Support

Razorpay is a tech company. We handle technical support too. If you are facing any kind of issue, You can write to us at (emailId). You can expect a response from the developers who are responsible for the SDK within 2 working days.
