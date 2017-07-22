# Final Check

How do we prevent data bleach?

# Goal
User owns the logs they record, so they are the ones who can view these.
Final Check must ensure that only the owning user can access the logs.

# Solution
Encrypt logs using the user's provided credentials

# Design
* When user signsup, create a public-private keypair.
* Encript the private key using *user's login password*(this is the only information known solely by the user)
* Save both *encripted private* key and *public* key in db.
* When Final Check System receives a log, it encrypts it using the *public key* then saves it.
* When user logs into the frontend UI, Final Check system uses their password to decrypt private key,
  * Then in turn it uses this private key to decrypt logs.
  * It performs all analysis required, then respond to the user.

![log encryption UML](https://github.com/clearonline-org/final-check/blob/master/http-log%20encryption.png "Log encryption UML")
