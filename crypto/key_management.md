#Overview to AOSP api components

Below there is info on the `KeyStore`

> KeyStore is responsible for maintaining cryptographic keys and their owners.

and the `KeyChain`

> Use the KeyChain API when you want system-wide credentials. When an app requests the use of any credential through the KeyChain API, users get to choose, through a system-provided UI, which of the installed credentials an app can access. This allows several apps to use the same set of credentials with user consent.

#KeyStore

##Version changes
- 1.6+
  -Keystore implemented as a native keystore daemon that used a local socket as its IPC interface
- 4.3
  - [Credential storage enhancements in Android 4.3](http://nelenkov.blogspot.co.uk/2013/08/credential-storage-enhancements-android-43.html)
  - can store public / private keys
  - can have multiple device users
    - before 4.3 only PRIMARY user could use
  - CANT store AES keys
    - but could encypt the AES key with created public / private key and in keystore
    - can store directly via hidden apis - see link above
    - Can with [`Vault`](https://android.googlesource.com/platform/development/+/master/samples/Vault/src/com/example/android/vault/SecretKeyWrapper.java) wrapper class
      - check out [g+ post](https://plus.google.com/+JeffSharkey/posts/9BmGb3xbPcA)
  - [Android 4.3 release notes](http://developer.android.com/about/versions/android-4.3.html#Security)
  - deamon retired and replaced with binder interface
- 4.4
  - support for elliptic curve

#KeyChain

- "...application access to the system key store and allows users to grant application access to the credentials stored there."
- 4.0+ api for cred storage. 4.3 hardware support