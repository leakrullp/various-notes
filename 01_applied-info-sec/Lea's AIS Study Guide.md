
# Introduction / security principles
bla
# Network Security
bla
# Symmetric Cryptography
bla
# Asymmetric Cryptography
bla
# Secure channels
bla
# Access Control and Authentication
## Authentication
**Authentication** means to *verify a claim of identity*. Authentication has 3 main factors:
- Knowledge (something you *know*)
- Possession (something you *have*)
- Inherence (something you *are*)

It is very common to only use passwords (knowledge) to authenticate yourself, but that is vulnerable to adversaries in these ways:
- **Guessing**: your password is among the most commonly used or otherwise easy to guess.
- **Snooping**: refers to unauthorized access to another person's or organization's data, often through methods like keyloggers or network monitoring tools. It can involve observing communications or ==capturing sensitive information== without consent.
- **Spoofing**: a tactic where attackers ==impersonate== another person or entity to ==deceive== victims, often to gain access to sensitive information or systems. This can involve techniques like email spoofing, where the sender's address is forged, or IP spoofing, where the source address of a message is altered to hide the attacker's identity.
- **Sniffing**: a form of denial-of-service attack which is carried out by sniffing or ==capturing packets== on the network, and then either sending them repeatedly to a victim machine or replaying them back to the sender with modifications. [^1]

[^1]: https://www.geeksforgeeks.org/ethical-hacking/what-is-sniffing-attack-in-system-hacking/ "What is Sniffing Attack in System Hacking?"

![[Pasted image 20251209181536.png]] ![[Pasted image 20251209181542.png]]
- **Server breach**: the data is accessed at the point where it is stored. For instance server side. 

### Passkeys (WebAuthn)

Passkeys (WebAuthn or FIDO) can make password less vulnerable by combining authentication and verification off the system and the user.

**Verification** happens locally on the user's device by ==entering a PIN or reading biometrics== (i.e. FaceID). This unlocks the authenticator – the phone, tablet or computer. Now the authentication device knows, that the user is who they say they are.
>[!important]
>The PIN/biometric never leaves the device. It's only used to unlock the private key stored inside the authenticator.

**Authentication** happens ==between device and server==. The website sends a challenge to the device, which then signs that challenge using the ==private key==, which is stored securely on the device. The signed response is sent back to the server over HTTPS. The server verifies it using the ==public key== it stored during registration.
So the website basically checks, that the signature matches the public key that it knows.

Together then make a strong, phishing resistant login-method.


![[Pasted image 20251209182854.png]]

### Cookie-based authentication

**Cookie-Based Authentication** uses small pieces of data called cookies to keep track of user sessions. When you log in, the server creates a session and sends a cookie with a session ID to your browser. This cookie is sent back to the server with each request, so the server knows who you are.

## Access Control
Authentication is the **prerequisite** for access control. AC is about giving the right privileges to the right user, but first you need to authenticate that user.

**Access control** is a process by which use of system resources are regulated according a security policy.

### Security Policies
#### Discretionary Access Model (DAC)
#### Mandatory Access Model (MAC)
#### Role-Based Access Control (RBAC)
#### Attribute-Based Access Control (ABAC)







# Frameworks for Cybersecurity
bla
# Penetration Testing
bla

# Terminology
| Term | Meaning |
| -------- | ------------ |
| Cross-site scripting (XSS) | blabla |

# Key concepts
Symmetric encryption vs. asymmetric
Digital signatures vs. HMAC