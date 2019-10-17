---
date: 2019-10-12 15:13:22 +0000
title: JWT Authentication in Python
image: "/images/jwt_05.jpg"
tags:
- Python
- JWT
- Authentication

---
[JSON Web Token](https://jwt.io/) (JWT) provide a means of transmitting information from the client to the server in a secured way.

<!-- excerpt -->

Since there are 3 parts separated by a ., each section is created differently. We have the 3 parts which are:

* header
* payload
* signature

![](/images/jwt.jpg)

#### Generation JSON Web Token:

* An API endpoint that accepts `username` and `password` via JSON payload and returns `access_token` which is the JSON Web Token we can use.
* We must pass the token as part of the `Authorization` header, like – `JWT <token>`.

One of the most popular library for JSON web token generation is `PyJWT`

> $ pip install pyjwt

### Creating a JWT in Python:

Here the user details are encoded for obtaining the JSON Web Token. Always try to store the encrypted password not the original one for security purpose. Here **sha256** library is used for password encryption and decryption. The token which is generated is usually not in **UTF-8** format. So .decode(‘utf-8) is used for the conversion.

    if sha256_crypt.verify(password, hashed_password):
      # Encoding user details
      access_token = jwt.encode({'username' : username, 'hashed_password' : hashed_password}, 'secret', algorithm='HS256')
      token = access_token.decode('utf-8')
      return jsonify({
        'auth_token' : token
        })

Decoding of the JSON Web token provides the user details as previously the user details were encoded to make the token some sense.

    token = request.headers['token']
    access_token = token.encode('utf-8')
    user_details = jwt.decode(access_token, 'secret')
    return jsonify(user_details)

For any queries ping me at [Twitter](https://twitter.com/vigneshwar1998).