# Backend: HTTP(s)

You can enable or disable sending data to Ruuvi Cloud:

<figure><img src="../../../.gitbook/assets/Screenshot from 2023-12-13 08-56-59.png" alt=""><figcaption></figcaption></figure>

Or configure to send data to your own server via HTTP/HTTPS (it is possible to send data to both destinations, Ruuvi Cloud and your own server, at the same time):

<figure><img src="../../../.gitbook/assets/Screenshot from 2023-12-19 21-32-09.png" alt=""><figcaption></figcaption></figure>

For your own server, you can choose the data format and decode data from Ruuvi sensors on the Gateway side:

<figure><img src="../../../.gitbook/assets/Screenshot from 2023-12-19 21-32-54.png" alt=""><figcaption></figcaption></figure>

Configure sending interval:

<figure><img src="../../../.gitbook/assets/Screenshot from 2023-12-13 09-02-17.png" alt=""><figcaption></figcaption></figure>

### Use different types of authentication

#### Configuring Basic Authentication

When using "Basic" authentication, the gateway adds an authorization header to the HTTPS request. This header contains the credentials encoded in Base64 format.

<figure><img src="../../../.gitbook/assets/Screenshot from 2024-05-08 15-45-19.png" alt=""><figcaption></figcaption></figure>

HTTP Header Example:\
`Authorization: Basic dXNlcjE6cGFzczE=`

Explanation:

* `Basic`: Indicates the authentication method.
* `dXNlcjE6cGFzczE=`: Base64 encoded credentials. For example, 'user1:pass1' encodes to 'dXNlcjE6cGFzczE='.

#### Configuring Bearer Authentication

When using "Bearer" authentication, the gateway adds an authorization header with a token to the HTTPS request. This token is a credential used to access APIs securely.

<figure><img src="../../../.gitbook/assets/Screenshot from 2024-05-08 15-46-10.png" alt=""><figcaption></figcaption></figure>

HTTP Header Example:

`Authorization: Bearer token123`

#### Configuring Token-Based Authentication

Token-based authentication involves securing API requests by sending a token in the HTTP header. The token is a unique identifier that must be included in every request.

<figure><img src="../../../.gitbook/assets/Screenshot from 2024-05-08 15-46-36.png" alt=""><figcaption></figcaption></figure>

HTTP Header Example:

`Authorization: Token token124`

#### Configuring API Key Authentication

API key authentication is a simple method where an API key is used directly as part of the HTTP header to authenticate requests.

<figure><img src="../../../.gitbook/assets/Screenshot from 2024-05-08 15-46-57.png" alt=""><figcaption></figcaption></figure>

HTTP Header Example:

`Authorization: token125`

#### Enhanced Security with SSL Client Authentication

It also supports client authentication via SSL by enabling the upload of a client certificate and its associated private key, ensuring secure and verified client-server communication:

<figure><img src="../../../.gitbook/assets/Screenshot from 2023-12-19 21-33-50.png" alt=""><figcaption></figcaption></figure>

You can use a server SSL Certificate if you want to be independent of public Certificate Authorities (CAs) or if you have deployed a self-signed certificate on the HTTPS server, giving you greater control and customization over your security infrastructure:

<figure><img src="../../../.gitbook/assets/Screenshot from 2023-12-19 21-34-43.png" alt=""><figcaption></figcaption></figure>
