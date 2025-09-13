
https://getpocket.com/read/1832967692

## Secure Shell

The information is encrypted

## Symmetrical encryption
Uses one key to decrypt and encrypt, called shared key or shared secret.
Is SSH a shared key is used to encrypt the communication. It is retrieved using some agreed method. This method is called a **key exchange algorithm**.
The key is never transmitted via the network. Both client and host apply a secret algorithm to a public data.
Host and client share the list of cyphers that they want to use in preferred order and agree on most mutually preferred.
### *But if I know the lists I can determine the algorithm. Is there any protection on this level?*
An example of such algorithm is AES123-ctr. So is this a way to attack against it?

## Asymmetric encryption 
Uses a key pair - public and private.
In SSH asymmetric is used to exchange the information about shared key generation method.

## Hashing
Function that generates a code from the input. It is impossible to reverse, so it is useful for a specific stuff like safe comparing of the values.
The hashing algorithm is picked alongside the symmetrical encryption algorithm.


These stuff is used in an SSH connection, but more details in an article

---
status: #⚙️ 
tags: 
related: 