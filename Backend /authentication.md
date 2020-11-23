# User Authentication

## Key Terms

**OAuth** is an open standard for access delegation, commonly used as a way for Internet users to grant websites or applications access to their information on other websites but without giving them the passwords. OAuth is an authorization protocol, rather than an authentication protocol. Using OAuth on its own as an authentication method may be referred to as pseudo-authentication.

**CSRF** Cross-Site Request Forgery

## Session-based Authentication

**BROWSER** `send` Login Data -> **SERVER** `save` Session to Database -> `return` Cookie{SessionId}

**BROWSER** `send` Authenticated request with Cookie{SessionId} -> **SERVER** `Check` SessionId with stored Session -> `return` response

The Session on Server has an expiration time. After that time, this Session has expired and the user must re-login to create another Session.

## JWT JSON Web Token

**BROWSER** `send` Login Data (username, password) -> **SERVER** `create` JWT with 'secret' -> `return` JWT

**BROWSER** `send` Authenticated request with JWT in Header -> **SERVER** `validate` JWT -> `return` response

The advantage of using Token-base Authentication over Session-based Authentication is storing the JWT on the _client_ side as opposed to storing the user's session on Cookie. i.e. it allows for the same backend to authenticate users on a mobile app or other platforms that do not have Cookie.

Storing JWT on Client side depends on platform:

- Browser: Local Storage
- IOS: Keychain
- Android: SharedPreferences

Standard Structure:

```
x-access-token: [header].[payload].[signature]
```

### Header: how to calculate JWT?

Common JWT Headers:

- `typ` **Token type** If present, it is recommended to set this to JWT.
- `cty` **Content type** If nested signing or encryption is employed, it is recommended to set this to JWT; otherwise, omit this field.[1]
- `alg` **Message** authentication code algorithm The issuer can freely set an algorithm to verify the signature on the token. However, some supported algorithms are insecure.[10]
- `kid` **Key ID** A hint indicating which key the client used to generate the token signature. The server will match this value to a key on file in order to verify that the signature is valid and the token is authentic.
- `x5c` **x.509 Certificate Chain** A certificate chain in RFC4945 format corresponding to the private key used to generate the token signature. The server will use this information to verify that the signature is valid and the token is authentic.
- `x5u` **x.509 Certificate Chain** URL A URL where the server can retrieve a certificate chain corresponding to the private key used to generate the token signature. The server will retrieve and use this information to verify that the signature is authentic.
- `crit` **Critical** A list of headers that must be understood by the server in order to accept the token as valid

### Payload: What to store in JWT?

Example

```
{
  "userId": "abcd12345ghijk",
  "username": "bezkoder",
  "email": "contact@bezkoder.com",
  // standard fields
  "iss": "zKoder, author of bezkoder.com",
  "iat": 1570238918,
  "exp": 1570238992
}
```

### Signature: Hash algorithm

```
const data = Base64UrlEncode(header) + '.' + Base64UrlEncode(payload);
const hashedData = Hash(data, secret);
const signature = Base64UrlEncode(hashedData)
```

### All Together

```
const encodedHeader = base64urlEncode(header);
/* Result */
"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9"

const encodedPayload = base64urlEncode(payload);
/* Result */
"eyJ1c2VySWQiOiJhYmNkMTIzNDVnaGlqayIsInVzZXJuYW1lIjoiYmV6a29kZXIiLCJlbWFpbCI6ImNvbnRhY3RAYmV6a29kZXIuY29tIn0"

const data = encodedHeader + "." + encodedPayload;
const hashedData = Hash(data, secret);
const signature = base64urlEncode(hashedData);
/* Result */
"crrCKWNGay10ZYbzNG3e0hfLKbL7ktolT7GqjUMwi3k"

// header.payload.signature
const JWT = encodedHeader + "." + encodedPayload + "." + signature;
/* Result */
"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VySWQiOiJhYmNkMTIzNDVnaGlqayIsInVzZXJuYW1lIjoiYmV6a29kZXIiLCJlbWFpbCI6ImNvbnRhY3RAYmV6a29kZXIuY29tIn0.5IN4qmZTS3LEaXCisfJQhrSyhSPXEgM1ux-qXsGKacQ"
```

### User Authentication flow with JWT

1. **User Registration**
   `POST` api/auth/signup -> Check existing and save User to database {username,email,role,password} -> return Message("Registered successfully")

2. **User Login**
   `POST` api/auth/signin -> Authenticate User, Create JWT string w/ 'secret' -> return {token, user info, authorities}

3. **Access Resource**
   Request data with JWT on x-access-token Header -> Check JWT Signature, Get user info & authenticate/authorize -> return Content based on authorities
