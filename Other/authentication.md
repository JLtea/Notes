# User Authentication

**OAuth** is an open standard for access delegation, commonly used as a way for Internet users to grant websites or applications access to their information on other websites but without giving them the passwords. OAuth is an authorization protocol, rather than an authentication protocol. Using OAuth on its own as an authentication method may be referred to as pseudo-authentication.

#### Session-based Authentication

**Browser** `send` Login Data => `save` Session to Database **Server**

**Browser** <= `return` Cookie{SessionId} **Server**

**Browser** `send` Authenticated request with Cookie{SessionId} => `Check` SessionId with stored Session **Server**

**Browser** <= `return` response **Server**

#### **JWT** JSON Web Token

The advantage of using Token-base Authentication over Session-based Authentication is storing the JWT on the _client_ side(Local Storage for Browser, Keychain for IOS and SharedPreferences for Android) as opposed to storing the user's session on Cookie.

Three Important parts:
**Header**
**Payload**
**Signature**

Standard Structure:

```
x-access-token: [header].[payload].[signature]
```
