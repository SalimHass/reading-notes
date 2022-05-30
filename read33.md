
# JWT Authentication

## What is JWT?

JSON Web Token (JWT) is a means of representing claims to be transferred between two parties. The claims in a JWT are encoded as a JSON object that is digitally signed using JSON Web Signature (JWS) and/or encrypted using JSON Web Encryption (JWE).

In simple terms, it is just another way of encoding JSON object and use that encoded object as access tokens for authentication from the server.


## When should you use JSON Web Tokens?
Here are some scenarios where JSON Web Tokens are useful:
* Authorization: This is the most common scenario for using JWT. Once the user is logged in, each subsequent request will include the JWT, allowing the user to access routes, services, and resources that are permitted with that token. Single Sign On is a feature that widely uses JWT nowadays, because of its small overhead and its ability to be easily used across different domains.

* Information Exchange: JSON Web Tokens are a good way of securely transmitting information between parties. Because JWTs can be signed—for example, using public/private key pairs—you can be sure the senders are who they say they are. Additionally, as the signature is calculated using the header and the payload, you can also verify that the content hasn't been tampered with.

## What is the JSON Web Token structure?
In its compact form, JSON Web Tokens consist of three parts separated by dots (.), which are:

* Header
* Payload
* Signature
Therefore, a JWT typically looks like this `xxxxx.yyyyy.zzzzz`


## Let’s break JWT

There are generally three parts in JWTs as shown in the above picture.
1st part is HEADER:
```json
{
 "alg": "HS256",
 "typ": "JWT"
}
```

**alg:** We have two main algorithms(HS256/RS256) to sign our JWT 3rd part (Signature) which we mention in the headers so that the producer and consumer(you will understand this soon in the next section) both should use the same algorithm to verify the token on each end. HS256 indicates that this token is signed using HMAC-SHA256.
**typ:** Define the type of the token which is JWT obviously in our case.

When we base64UrlEncode the above header data we will get eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9 the first part of our JWT token.

## 2nd part is PAYLOAD:
It mostly contains the claims (custom data) and some standard claims as well. We can use standard claims to identify a lot of things i.e exp: the expiry of the token,iat: time at which token issued etc.
```json
{
 "email": "John Doe",
 "xyz": "abc"
}
```
When we base64UrlEncode the above payload data we will get eyJuYW1lIjoiSm9obiBEb2UiLCJhbW91bnQiOjUwMCwieHl6IjoiYWJjIn0 the second part of our JWT token.

## 3rd part is SIGNATURE:

It is calculated by base64url encoding of header and payload and concatenating them with a period as a separator. Then encrypt it with HMAC-SHA256 along with the secret key and the result of the first step.
```
key           = 'secretkey';
unsignedToken = encodeBase64Url(header) + '.' + encodeBase64Url(payload);
signature     = HMAC-SHA256(key, unsignedToken) // As mentioned in header section.
```
When we perform the above steps we will get 54W-Y-Xz6xKgSnbQ7Se7tK5hcbXIvjsZ47u6CnQxjag the third part of our JWT token

## How do JSON Web Tokens work?
In authentication, when the user successfully logs in using their credentials, a JSON Web Token will be returned. Since tokens are credentials, great care must be taken to prevent security issues. In general, you should not keep tokens longer than required.

Whenever the user wants to access a protected route or resource, the user agent should send the JWT, typically in the Authorization header using the Bearer schema.


## Why should we use JSON Web Tokens?
Let's talk about the benefits of JSON Web Tokens (JWT) when compared to Simple Web Tokens (SWT) and Security Assertion Markup Language Tokens (SAML).

As JSON is less verbose than XML, when it is encoded its size is also smaller, making JWT more compact than SAML. This makes JWT a good choice to be passed in HTML and HTTP environments.

Security-wise, SWT can only be symmetrically signed by a shared secret using the HMAC algorithm. However, JWT and SAML tokens can use a public/private key pair in the form of a X.509 certificate for signing. Signing XML with XML Digital Signature without introducing obscure security holes is very difficult when compared to the simplicity of signing JSON.

JSON parsers are common in most programming languages because they map directly to objects. Conversely, XML doesn't have a natural document-to-object mapping. This makes it easier to work with JWT than SAML assertions.

## How to Use JWT Authentication with Django REST Framework

The JWT is acquired by exchanging an username + password for an access token and an refresh token.

The access token is usually short-lived (expires in 5 min or so, can be customized though).

The refresh token lives a little bit longer (expires in 24 hours, also customizable). It is comparable to an authentication session. After it expires, you need a full login with username + password again.

Why is that?

It’s a security feature and also it’s because the JWT holds a little bit more information


