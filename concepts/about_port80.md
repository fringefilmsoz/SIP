# About the HTTP port number

The HTTP port number is part of the system's URL.

Port 80 is the default number for web sites and as such does not need to be included when the URL is entered into a browser's address bar. Many web servers use port 80 by default.

If you are running another server on the same Raspberry Pi as SIP and using the same port number there will be a conflict and SIP may not start.

You can avoid the conflict by changing SIP's port number on the Options page to something like 8080. If you change the port number SIP uses you will need to include that number, preceded by a colon, in the URL for SIP's web interface. For example:

```
[URL of the Raspberry pi]:8080
```

