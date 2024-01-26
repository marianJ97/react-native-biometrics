# @marianJ97/react-native-biometrics

This is fork from the [SelfLender/react-native-biometrics repository](https://github.com/SelfLender/react-native-biometrics/tree/master)
It allows additional options when generating keys, for now only accesGroup for ios (more added later).
Fork is made from react-native-biometrics version `3.0.0`
For official documentation and more informations, reach [SelfLender/react-native-biometrics repository](https://github.com/SelfLender/react-native-biometrics/tree/master).

React native biometrics is a simple bridge to native iOS and Android keystore management. It allows you to create public private key pairs that are stored in native keystores and protected by biometric authentication. Those keys can then be retrieved later, after proper authentication, and used to create a cryptographic signature.

## React Native Compatibility

| `@marianJ97/react-native-biometrics` version | Required React Native Version |
| :------------------------------------------: | :---------------------------: |
|                  `>= 1.0.0`                  |           `>= 0.60`           |

## Getting started

using either Yarn:

`yarn add @marianJ97/react-native-biometrics`

or npm:

`$ npm install @marianJ97/react-native-biometrics --save`

### Install pods

`$ npx pod-install`

### Link / Autolinking

On React Native 0.60+ the [CLI autolink feature](https://github.com/react-native-community/cli/blob/master/docs/autolinking.md) links the module while building the app.

## Additional configuration

#### iOS

This package requires an iOS target SDK version of iOS 10 or higher

Ensure that you have the `NSFaceIDUsageDescription` entry set in your react native iOS project, or Face ID will not work properly. This description will be presented to the user the first time a biometrics action is taken, and the user will be asked if they want to allow the app to use Face ID. If the user declines the usage of face id for the app, the `isSensorAvailable` function will indicate biometrics is unavailable until the face id permission is specifically allowed for the app by the user.

#### Android

This package requires a compiled SDK version of 29 (Android 10.0) or higher

## Usage

All other cases are identical, so for more information reach [SelfLender/react-native-biometrics repository](https://github.com/SelfLender/react-native-biometrics/tree/master).

## Difference

### createKeys()

Generates a public private RSA 2048 key pair that will be stored in the device keystore. Returns a `Promise` that resolves to an object providing details about the keys.

**Result Object**

| Arguments   | Type   | Description                                                                  |
| ----------- | ------ | ---------------------------------------------------------------------------- |
| accessGroup | string | String representation of accessGroup in which will be keys stored (iOS only) |

| Property  | Type   | Description                                         |
| --------- | ------ | --------------------------------------------------- |
| publicKey | string | A base64 encoded string representing the public key |

**Example**

```js
import ReactNativeBiometrics from "react-native-biometrics";

const rnBiometrics = new ReactNativeBiometrics();

rnBiometrics.createKeys().then((resultObject) => {
  const { publicKey } = resultObject;
  console.log(publicKey);
  sendPublicKeyToServer(publicKey);
});
```

**iOS Example**

```js
rnBiometrics
  .createKeys({ accessGroup: "yourGroupIdentifier" })
  .then((resultObject) => {
    const { publicKey } = resultObject;
    console.log(publicKey);
    sendPublicKeyToServer(publicKey);
  });
```
