---
title: Send Data Message Notification from API (Server-side)
description: 2
---

Sending data messages is only possible via the API.

**Step 1:** API for Obtaining an Access Token

For details about the API, please refer to [Request for access token](https://developer.huawei.com/consumer/en/doc/development/HMS-2-References/hmssdk_huaweipush_api_reference_agent_s1).

**Step 2:** API for Sending Push Messages

Protocol: HTTPS POST

API URL: https://push-api.cloud.huawei.com/v1/[appid]/messages:send

> appId: unique ID allocated to a quick app created on AppGallery Connect. For details about how to obtain the app ID, please refer to [Obtaining the APP ID](https://developer.huawei.com/consumer/en/doc/development/quickApp-Guides/quickapp-create-quickapp#obtainAppID).

**Step 3:** Request Parameters (HTTP Header)

| **Parameter** | **Example**                                                  | **Description**                                              |
| ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Content-Type  | application/json                                             | application/json                                             |
| Authorization | Bearer  CF3Xl2XV6jMKZgqYSZFws9IPlgDvxqOf<br />FSmrlmtkTRupbU2VklvhX9kC9JCnKVSDX2VrDgAPuzvNm3WccUIaDg== | The format is as follows:  Bearer+space+Access token.  If an access token contains backslashes (\),  remove all of them. |

**API request parameter (HTTP body) example**

```json
{
    "validate_only": false,
    "message": {
        "data": JSON_FORMAT_STRING,
        "android": {
            "fast_app_target": 1
        },
        "token": ["AJRqlvj_atpAUr6qa2hZY-dRBSqzs-OJpF37fXShdXa7hXRHgX5v0M_-aF3KSXqLqhUreGMXmiiyzGVWYVToAa4ohlAUy_RsC75wxv7lnG2-rxf6RV_ivNbLjOCbYQ-tdw"]
    }
}
```

**Step 4:** API request parameter (HTTP body)

| **Parameter** | **Type** | **Mandatory /Optional** | **Description**                                              |
| ------------- | -------- | ----------------------- | ------------------------------------------------------------ |
| validate_only | boolean  | Optional                | Indicates whether a  message is a test message. The test message is only used to verify format  validity and is not pushed to user devices. The options are as follows:  ·      **true**: test message.  ·      **false**: formal message.     The default value  is **false**. |
| message       | object   | Mandatory               | Push message  structure. The message structure must contain the valid message payload and  valid sending object. For details about the fields, please refer to the table  of [Message structure](https://developer.huawei.com/consumer/en/doc/development/quickApp-Guides/quickapp-access-push-kit#message) definition. |

**Message structure**

| **Parameter** | **Type** | **Mandatory/Optional** | **Description**                                              |
| ------------- | -------- | ---------------------- | ------------------------------------------------------------ |
| data          | string   | Mandatory              | urlencoded JSON  structure of a push message, including the type, content, display, tap  action, report statistics, and extended information of the push message. For  details, please refer to the [data example](https://developer.huawei.com/consumer/en/doc/development/quickApp-Guides/quickapp-access-push-kit#dataDemo) and [data structure description](https://developer.huawei.com/consumer/en/doc/development/quickApp-Guides/quickapp-access-push-kit#dataDesc). |
| android       | object   | Mandatory              | Android push message  control. For details about the fields, please refer to the table of [AndroidConfig structure](https://developer.huawei.com/consumer/en/doc/development/quickApp-Guides/quickapp-access-push-kit#androidCfg) definition. |
| token         | string   | Mandatory              | Push token of the  target user of a push message. Each push token is the regId obtained through  the **subscribe** API  in the following format: ["pushtoken1","pushtoken2"] |

**Sample Data Message:**

```json
{
    "pushtype": 1,
    "pushbody": {
        "messageId": "111110001",
        "data": "Test message"
    }
}
```

**Step 5:** Implementing Data Message Receiver

The payload of a data message can be received in the callback.

```javascript
push.on({
    callback: function(ret) {
        console.log("received pass through message, ret=" + JSON.stringify(ret));
    }
});
```

<img src="../assets/push_kit6.png" alt="image-20201223161031796" style="width:300px;" />

## Turn Off Push Notifications

The callback in the **push.on** API will not receive the data message.

```javascript
push.off(); 
```