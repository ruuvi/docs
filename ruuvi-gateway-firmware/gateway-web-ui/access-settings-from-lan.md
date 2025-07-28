# Access Settings from LAN

On this page, you can set access rules to Ruuvi Gateway from the local network. By default, the access is password protected using the default password (unique device ID which is printed on the bottom of Ruuvi Gateway).

<figure><img src="../../.gitbook/assets/Screenshot from 2023-12-13 08-44-00.png" alt=""><figcaption></figcaption></figure>

If you wish, you can set your own username and password:

<figure><img src="../../.gitbook/assets/Screenshot from 2023-12-13 08-45-16.png" alt=""><figcaption></figcaption></figure>

Or disable access by username/password:

<figure><img src="../../.gitbook/assets/Screenshot from 2023-12-13 08-49-56.png" alt=""><figcaption></figcaption></figure>

You can also allow access without a password, but this is not recommended as it is not very secure:

<figure><img src="../../.gitbook/assets/Screenshot from 2023-12-13 08-52-22.png" alt=""><figcaption></figcaption></figure>

It is also possible to access Ruuvi Gateway from LAN using bearer authentication with an API key (token). You can enable read-only access (to retrieve data in [polling-mode.md](../examples/polling-mode.md "mention") via the /history endpoint) or read-write access (to read any data or change the configuration):

<figure><img src="../../.gitbook/assets/Screenshot from 2023-12-13 08-54-18.png" alt=""><figcaption></figcaption></figure>
