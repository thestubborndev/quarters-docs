# Quarters Unity SDK - v0.8.1

**Supported platforms**: `iOS` and `Android`.

» **[Download Quarters Unity SDK.](http://downloads.pocketfulofquarters.com/quarters-sdk-latest.unitypackage)**

## Configuration
Follow [Getting Started guide](/getting-started) to create your Quarter App.

## Unity integration
Import `Quarters SDK` from `Unity Asset Store`, add `QuartersSDK/Prefab/QuartersInit.prefab` to your first scene, then copy your `APP_ID` and `APP_KEY` to QuartersInit inspector.


## Platform specific setup

### iOS
No platform specific setup is needed for iOS. Deep linking setup is handled automatically by a post process.

[Click here](https://www.youtube.com/watch?v=YJU192xItO0&list=PL0TyRhVVizdBsWYGCcXJ-h43ybYBYm_Gu) to watch a video on how to get started with Quarters SDK for iOS in under 3 mins!

---

### Android
In Unity top menu go `Quarters/Android/Generate Android Manifest`. Android Manifest will automatically generate enabling deep linking.

If your project contain Android Manifest already, manual manifest will be required.

[Click here](https://www.youtube.com/watch?v=YJU192xItO0&list=PL0TyRhVVizdBk-apKTf6lBUAMkEc7E4Y7) to watch a video on how to get started with Quarters SDK for Android!

Authorization
----
Before you can use Quarters API you must authorise users session.


Example:

    using QuartersSDK;

    Quarters.Instance.Authorize(OnAuthorizationSuccess, OnAuthorizationFailed);


    public void OnAuthorizationSuccess() {
    	Debug.Log("OnAuthorizationSuccess");
    }


    public void OnAuthorizationFailed(string error) {
    	Debug.LogError("OnAuthorizationFailed: " + error);

    }

Quarters is using OAuth in external browser. This means your user will be sent outside the app for OAuth in the browser. After successful or failed authorisation user is seamlessly deep linked back to the app.


Get User Details
----
Get user details can be only called after successful authorization. Success delegate returns `User` object with basic user details.


Example:

    using QuartersSDK;

    Quarters.Instance.GetUserDetails(delegate(User user) {
    	Debug.Log("User loaded");

    } , delegate (string error) {
    	Debug.LogError("Cannot load the user details: " + error);

    } );




Get accounts
----
Get account can be only called after successful authorization. On success delegate will be called with a list of user accounts. (Note: Only one user account is currently supported by the API).


Example:
----

    using QuartersSDK;

    Quarters.Instance.GetAccounts(delegate (List<User.Account> accounts) {

    //success

    }, delegate (string error) {

    //failed

    });


Get Account Balance
----
Get account balance can be only called after successful authorization. On success delegate is fired with `User.Account.Balance` object.


Example:

    using QuartersSDK;

    Quarters.Instance.GetAccountBalance(delegate (User.Account.Balance balance) {

    }, delegate (string error) {

     });



Transfer
----
Transfer request can be only called after successful authorization. This call allows to charge user quarters that will be transferred to your Quarters app. Transfer request is done through external browser, similar to Authorize call. On Success transaction hash is returned. Please note it can take up to 3 minutes for your transfer to appear.


Example:

    using QuartersSDK;

    TransferAPIRequest request = new TransferAPIRequest(int.Parse(tokensInput.text), descriptionInput.text, delegate (string transactionHash) {

    //success

    }, delegate (string error) {

    //failed

    });

    //start transfer
    Quarters.Instance.CreateTransfer(request);


## RELEASE NOTES

General notes:
- only one account is currently supported by API, hence Get Accounts and Account balance calls are working with first returned account
- a post authorization calls can be called at any time. There is no need for calling API in any order. Example: After Authorizing session
GetAccountBalance can be called right away without need of calling GetUserDetail -> GetAccounts -> GetAccountBalance.



#####
0.8.0
- Added PlayFab module
- Supporting Playfab server side Quarters apps to user transfers


#####




#####
0.7.0
- Quarters UI added
- Editor scripts are now inheriting from UnityEditor.Editor to avoid potential conflicts with custom Editor namespace


#####


#####
0.6.0
- Added automated Android Manifest Generation in Quarters/Android/Generate Android Manifest
- Android package name can now contain uppercase characters


#####


#####
0.5.0
- Deep linking is now dynamic. Multiple apps using Quarters SDK are now supported on single Android or iOS device


#####


#####
0.4.0
- Added URIParser to better deep link parameters handling
- Full Transfer support on iOS and Android
- Added automated iOS post process builds
- iOS deep linking


#####


#####
0.3.0
- added seamless support for GetAccounts call
- added seamless support for GetAccountBalance
- basic one way support for Transferring quarters added

known issues:
- no deep linking with parameters support for TransferRequest. Doe to lack of API support for this functionality. Its coming in next release.


#####

#####
0.2.0
- Added Android deep linking. Quarters SDK will now automatically handle URL schemes
- Android support added for oauth calls outside the app
- Basic Android Manifest added for handling linking, intents and permissions
- Android support for Authorize call
- Example - added simple on screen console


#####


#####
0.1.0
- Added simple authorization in editor
- Refresh and access token are handled during Authorization
- Added GetUserDetails API call with refreshing access token if expired



Known issues:
- QuartersInit App ID and App key aren't serialised into Unity scene - fixed in 0.2.0

#####
