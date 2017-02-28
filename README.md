byteskode-android-push(WIP)
=========================

[![](https://jitpack.io/v/byteskode/byteskode-android-push.svg)](https://jitpack.io/#byteskode/byteskode-android-push)


byteskode push - Android FCM library

## Installation
Add [https://jitpack.io](https://jitpack.io) to your build.gradle with:
```gradle
allprojects {
    repositories {
        maven { url "https://jitpack.io" }
    }
}
```
add `byteskode-android-push` dependency into your project

```gradle
dependencies {
    compile 'com.github.byteskode:byteskode-android-push:v0.2.0'
}
```

## Usage

Initialize `byteskode-android-push`

```java
public class SampleApp extends Application{

    @Override
    public void onCreate() {
        super.onCreate();

        //initialize push
        Push.initialize(<context>, <apiBaseUrl>, <apiAuthorizationToken>);
    }

}
```

In activity start listen for the foreground push message

```java
public class MainActivity extends PushCompactActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    @Override
    protected void onResume() {
        super.onResume();
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
    }

    @Override
    public void onMessage(RemoteMessage remoteMessage) {
        ...
    }

     @Override
     public void onRegistrationTokenRefreshed(Device device) {
        ....
     }

     @Override
     public void onRegistrationTokenError(String error) {
        ...
     }
     
     @Override
      public void onDeviceSynced(Device device) {
        ...
      }
}
```

## Android API

### Force Device Sync with Extra Details
To force sync application specific extra details you may call `push.sync(<extraKey>, <extraValue>)` or `push.sync(mapOfExtras)`
 which will force syncing the device details to your backend api.

All extras will be send under `extras` field of the device details sent to the server.

Example
```js
{ 
  extras: { 
      phone: '255714999999' 
   },
  instanceId: <firebaseInstanceId>,
  registrationToken: <firebasePushRegistrationToken>,
  topics: [], //list of topic device subscribe to
  uuid: <uniquePseudoId> 
}
```

## API Server Implementation

API Server endpoint must implemnt `device REST aware resource` and support both `POST` and `PUT` request.

- [See Sample](https://github.com/lykmapipo/byteskode-android-push/blob/master/api/index.js)

Authorization header is set with the value `Bearer <apiAuthorizationToken>` on every request sent.


## Test
```sh
./gradlew test
```

## Contribute
It will be nice, if you open an issue first so that we can know what is going on, then, fork this repo and push in your ideas.
Do not forget to add a bit of test(s) of what value you adding.

## License

(The MIT License)

Copyright (c) 2011 lykmapipo, byteskode Group && Contributors

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
