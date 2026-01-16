#NSE4 

### Overview

Phase 1 Process:

1. **Authenticate peers.**
	This can be done with one of two methods: Pre Shared Key or a Digital Signature. XAuth can be enabled for greater security.
2. **Negotiate one bidrectional SA.**
	There are 2 possible modes - Main or aggressive. These settings must be configured the same on both ends or the tunnel wont form.
3. **Negotiate Diffie-Hellman (DH) keys.**
	These are used to create the P2 tunnels. DH uses the public key and a mathematical factor called a nonce. This is used to generate a common private key.

### XAuth
XAuth sometimes called phase 1.5 forces remote users to authenticate additionally with their credentials.

When you set Remote Gateway to Dialup User, FortiGate acts as the authentication server. The XAuth section shows the authentication server type options: **PAP Server**, **CHAP Server**, and **Auto Server**. 

When Auto Server is selected, which means that FortiGate automatically detects the authentication protocol used by the client.

When Remote Gateway is set to Static IP Address or Dynamic DNS, FortiGate acts as the client, and the XAuth section shows the Client option as Type. You can then set the credentials that FortiGate uses to authenticate against the remote peer through XAuth.