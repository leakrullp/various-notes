# Security Goals and Principles

#### Select the correct statement regarding the three main security goals of Confidentiality, Integrity and Availability.

a) It is not possible to design a system that achieves perfect confidentiality, integrity and availability at the same time.
b) It is not possible to design a secure channel protocol that guarantees both confidentiality and integrity for the transmitted data.
c) Achieving the confidentiality goal automatically implies achieving the integrity goal, because the adversary cannot modify data that it cannot see.
d) Achieving the availability goal automatically implies achieving the integrity goal, because when users are guaranteed access to a system, the adversary cannot modify the data that is being accessed.

#### An update to a proprietary anti-virus software for a certain closed source operating system caused all computers where that combination of operating system and anti-virus was running to freeze, requiring a new update in order to restore normal functionality. What security goal was compromised and what security principles should have been observed to avoid this issue?

a) Availability was compromised and the principles of Open Design and Fail Safe Defaults should have been observed.
b) Integrity was compromised and the principles of Open Design and Minimum Exposure should have been observed.
c) Confidentiality was compromised and the principles of Economy of Mechanism and Minimum Exposure should have been observed.
d) Integrity was compromised and the principle of Complete Mediation should have been observed.

#### An instant messaging service wishes to ensure that messages can only be read by their intended recipients and that messages cannot be tampered with. According to this description, what security goals does this service wish to achieve and how should they be achieved according to security principles?

a) The service wishes to achieve confidentiality and integrity, and it should implement end-to-end encrypted secure channels and user authentication using standardized security protocols.
b) The service wishes to achieve confidentiality and integrity, and it should implement end-to-end encrypted secure channels and user authentication using their own proprietary protocols in order to avoid espionage and tampering by strong adversaries such as States and Corporations.
c) The service wishes to achieve availability and integrity, and it should implement a system where users send their messages via a TLS secure to a central server, who receives the messages and redirects them to the intended recipient via another TLS secure channel.
d) The service wishes to achieve confidentiality and availability, and it should implement a system where users send messages encrypted under a blockcipher to many decentralized servers, which redirects the ciphertexts to the intended recipient.

#### A web server running a standard LAMP (Linux, Apache, MySQL and PHP) stack is directly connected to the Internet via a public IP address and allows direct connections to the MySQL database server, which is running with root privileges on the Linux operating system. What security principles have been violated in this situation?

a) Least Privilege, Minimum Exposure, Complete Mediation.
b) Open Design, Economy of Mechanism.
c) Open Design, Minimum Exposure, Psychological Acceptability.
d) Economy of Mechanism, Psychological Acceptability.

# Network Security

#### Select the correct alternative about the security guarantees of protocols in the TCP/IP stack against Dolev-Yao adversaries.

a) No protocol in the TCP/IP stack offers confidentiality and integrity guarantees.
b) The WiFi networking standard IEEE 802.11g offers stronger confidentiality guarantees than the wired standard 802.3. 
c) The TCP protocol guarantees availability via the sliding window mechanism.
d) The IP protocol guarantees authenticity because it guarantees that packages come from a designated sender.

> [!Info] Dolev-yao adversary (Lecture 2)
> An adversary that has complete control of the network.

#### What security measure can be used to guarantee minimum exposure of computers connected to the internet with the only goal of browsing websites and how should it be configured? 

a) A stateful firewall configured to deny all incoming connections to all ports of all computers in the internal network, while only allowing outgoing connections to the TCP ports commonly used for the HTTP/HTTPS protocols and allowing incoming traffic corresponding to existing connections. 
b) A firewall configured to deny all incoming traffic to all ports of all computers in the internal network, while allowing outgoing connections to the TCP ports commonly used for the HTTP/HTTPS protocols. 
c) A stateful firewall configured to allow all incoming connections to the TCP ports commonly used for the HTTP/HTTPS protocols of all computers in the internal network, while only denying outgoing connections to these TCP ports.
d) An Intrusion Detection System configured to issue an alert when all incoming network traffic is detected, except for traffic directed to the TCP ports commonly used for the HTTP/HTTPS protocols.

#### Select the INcorrect alternative about IP spoofing attacks.

a) In an IP spoofing attack, the adversary uses their own IP address as the source address and fakes the destination address.
b) In an IP spoofing attack, the adversary uses a fake source IP address.
c) An IP spoofing attack can be used to mount a Denial of Service attack.
d) The IP protocol does not offer protection against IP spoofing attacks.

#### Which of the following attack is not aimed at causing Denial of Service

a) TCP sequence prediction attack.
b) TCP reset attack.
c) IP fragmentation attack.
d) TCP syn flood.

# Symmetric Key Cryptography

#### Select the correct statement about symmetric key cryptography.

a) It is possible to construct a symmetric encryption scheme with perfect security against unbounded adversaries.
b) Symmetric ciphers provide integrity guarantees and message authentication codes provide confidentiality guarantees.
c) For any input space, given the output of a cryptographic hash function, it is infeasible to guess the input used to produce that output. Hence, hash functions provide confidentiality guarantees.
d) In order to employ symmetric key cryptographic schemes, users should publicly advertise their keys, so that other users are guaranteed to have access to the same symmetric key.

#### Select the correct statement about message authentication codes.

a) A secure message authentication code can be constructed from cryptographic hash functions.
b) A message authentication code can always be used as an efficient substitute for a digital signature scheme.
c) A cryptographic hash function is a secure message authentication code due to its pre-image resistance, second pre-image resistance and collision resistance properties.
d) Given current standards, the HMAC scheme should be instantiated using the MD5 and SHA1 hash functions.

#### Given a secure block cipher, what happens if the initialization vector in the CBC mode of operation for block ciphers is set to a fixed public string?

a) Two ciphertexts encrypting the same plaintext message under the same key are always identical.
b) The secret key can be trivially extracted by the adversary.
c) The resulting encryption scheme provides confidentiality guarantees for messages of any length.
d) The block cipher yields the same output for every message encrypted under different keys.

#### Select the INcorrect statement about the AES block cipher.

a) According to the standard, this block cipher can operate with any block length.
b) According to the standard, this block cipher can operate with keys of 128, 192 or 256 bits length.
c) The confusion layer based on S-Boxes reduces the correlation between the ciphertext and the key.
d) The diffusion layer based on the ShiftRows and MixCols procedures reduces the correlation between the plaintext message and the ciphertext.

#### A company deploying resource constrained IOT surveillance devices designed a motion sensor that reports the detection of motion to a monitoring station by wirelessly sending a message authentication code tag generated for the fixed message "DETECTED" under a shared symmetric key only known by the sensor and the monitoring station. When no motion is detected, the sensor periodically sends a message authentication code tag generated for the fixed message "NO" under the same symmetric key. A clever group of burglars has been monitoring wireless communications around a house using this system and is now confident that they can rob the house without being detected. Should the burglars be confident and why?

a) They should be confident because by observing the messages sent when there are signs of people in the house they can detect when the house is empty and jam the wireless channel to prevent motion detection transmission.
b) They should be confident because they can extract the key to the message authentication code after observing several messages and tags.
c) They should not be confident because since they can only see the message authentication code tag, they don't know whether the message being sent is "DETECTED" or "NO", so they cannot know if the house is empty or not.
d) They should not be confident because message authentication code tags generated under the same key will always be the same even if the input message is different, so they cannot detect what message is being sent by the sensor.

# Key Exchange and Asymmetric Key Cryptography

#### Select the correct statement about the Diffie-Hellman key exchange protocol. 

a) The Diffie-Hellman key exchange protocol prevents an eavesdropper who can see all messages in the network but cannot modify them from learning the exchanged symmetric key if the computational Diffie-Hellman problem is hard.
b) The Diffie-Hellman key exchange protocol is secure if the discrete logarithm problem is hard.
c)  A Dolev-Yao adversary cannot learn messages encrypted under a symmetric key exchanged using the Diffie-Hellman protocol if the computational Diffie-Hellman problem is hard.
d) The Diffie-Hellman key exchange protocol requires parties to know each other's encryption public keys.

#### Select the Incorrect statement about asymmetric encryption.

a) An asymmetric encryption scheme prevents an adversary who does not know the secret key from modifying an encrypted message.
b) In an asymmetric encryption scheme, a public key can be used to encrypt plaintext messages, while a secret key can be used to decrypt ciphertexts.
c) An asymmetric encryption scheme guarantees that an adversary who does not know the secret key cannot learn anything about a plaintext message from a ciphertext encrypting this message, except for its length.
d) In order to construct a secure asymmetric encryption scheme, it is necessary to assume that a certain computational problem is hard for the adversary, i.e. assuming that the adversary cannot solve said problem in probabilistic polynomial time.

#### A bank who has a secret key sk uses ElGamal encryption to receive encrypted transfer orders from its clients, who all know the banks public key pk, the underlying multiplicative cyclic group G of order q and the generator g of G used as system parameters for this encryption scheme. Transfer orders can be encoded into messages m such that every m is an element of G. Clients encrypt transfer order as ciphertexts (c_1,c_2) where c_1=g^r, c_2=m(pk)^r. Select the correct alternative: 

a) In order to decrypt transfer orders received as a ciphertext (c_1,c_2), the bank computes (c_2)/((c_1)^sk).
b) This scheme provides confidentiality guarantees if the group G is the set of integers modulo 6689 with the integer multiplication operation.
c) This scheme prevents a Dolev-Yao attacker who does not know the secret key sk from modifying transfer orders.
d) The bank can never recover the transfer orders because the encryption procedure has not computed c_1 mod 6689 and c_2 mod 6689.

#### A command and control system encrypts an "ATTACK" or "RETREAT" plaintext message using a public key encryption scheme in order to obtain a ciphertext C and then signs the same  "ATTACK" or "RETREAT" plaintext message to obtain a signature Sig. The command is sent to a general in the field by sending the ciphertext C and the signature Sig over insecure channels in such a way that they are received by the general. Upon receiving the message (C,Sig), the general decrypts the ciphertext to obtain the plaintext message, verifies the signature and decides whether to accept the command. Assuming that the general and commander know each other's public keys for the encryption and signature schemes, select the Incorrect alternative about this scenario.

a) The scheme prevents Dolev-Yao attackers controlling the insecure channels from learning anything about the commands issued by the general.
b) An eavesdropper who sees the messages sent over insecure channels may be able to distinguish whether a command is for "ATTACK" or "RETREAT".
c) The ciphertext should be generated under the general's public key and the signature should be generated under the commander's signing key.
d) The signature scheme ensures that the order has been given by the commander.

#### In order to save resources, a company designing IOT sensors that communicate over insecure channels decided to implement secure channels using a modified ElGamal encryption scheme where the same randomness is used to generate each ciphertext. What is the problem with this approach?

a) It is possible for an eavesdropper to detect when the sensor sends the same message over insecure channels and for a Dolev-Yao adversary to modify the encrypted messages without being detected.
b) It is possible for a Dolev-Yao adversary to detect when the sensor sends the same message over insecure channels but it cannot modify the encrypted messages without being detected.
c) There is no problem with this approach as long as the Decisional Diffie-Hellman problem is hard for the Dolev-Yao adversary.
d) This approach is just as computationally expensive as using the standard ElGamal encryption scheme.

# Secure Channels, PKI and TLS

#### What is the issue with using the textbook Diffie-Hellman key exchange protocol against a Dolev-Yao adversary and how to solve it?

a) The Dolev-Yao adversary can mount a man-in-the-middle attack, where it impersonates each honest party towards the other honest party and executes an instance of the Diffie-Hellman key exchange protocol towards each honest party. This issue can be solved by having each honest party sign their Diffie-Hellman protocol message with digital signature scheme and verify the signature on the message from the other party, provided that both parties know each other's digital signature verification keys.
b) The Dolev-Yao adversary can mount a man-in-the-middle attack, where it impersonates each honest party towards the other honest party and executes an instance of the Diffie-Hellman key exchange protocol towards each honest party. This issue can be solved by having each honest party hash their Diffie-Hellman protocol message using a cryptographic hash function and verify that the message they receive from the other party is accompanied by a hash output that matches the result of hashing the received message.
c) The Dolev-Yao adversary can extract keys exchanged via the Diffie-Hellman protocol by observing the messages exchanged by the honest parties. This issue can be solved by encrypting the Diffie-Hellman protocol messages using a public key encryption scheme.
d) There is issue with using the textbook Diffie-Hellman key exchange protocol against a Dolev-Yao adversary if the protocol is correctly implemented in the computational Diffie-Hellman problem is hard for the adversary.

#### Select the correct alternative about digital certificates.

a) A digital certificate can be validated by obtaining the digital certificate for the certificate authority (CA) that issues it and validating the CA's signature. If the CA is not a root CA, the process is repeated to validate the CA's certificate until a root CA whose certificate is locally available is reached.
b) Client software must store digital certificates for all certificate authorities in order to validate certificates received from web servers.
c) A currently valid certificate cannot be revoked by its owner.
d) A digital certificate contains a public key that can be securely used by any asymmetric cryptographic scheme.

#### What security guarantees does a certificate transparency solution add to a public key infrastructure?

a) A certificate transparency solution guarantees that an attack can be detected when compromised certificate authorities replace a certificate for an honest party with a rogue certificate created by an adversary.
b) A certificate transparency solution replaces Certificate Authorities in the process of certificate revocation, implementing a decentralized certificate revocation list.
c) A certificate transparency solution ensures that no digital certificate can be forged by rogue CAs that become compromised by adversaries.
d) A certificate transparency solution allows for obtaining trusted root CA certificates in a more efficient way.

#### Select the correct alternative about the TLS protocol.

a) In the TLS handshake, client and server securely exchange symmetric keys, which are later used to guarantee confidentiality and integrity for transferred data.
b) The TLS protocol allows for ensuring confidentiality and integrity of transferred data by means of any arbitrary encryption scheme and message authentication code that the client and server choose.
c) When establishing a secure channel using the TLS protocol, it is necessary for a client to present a valid digital certificate to the server, so that the server can verify digital signatures generated by the client.
d) The TLS protocol ensures confidentiality by encrypting all data with public key encryption schemes such as ElGamal or RSA, while integrity is guaranteed by generating digital signatures for each packet that is transferred. 

#### What are the main improvements over TLS 1.2 introduced by TLS 1.3?

a) Removing support for insecure cipher suites, reducing the number of rounds in the Handshake phase and introducing 0-RTT resumption.
b) Introducing security against quantum attacks by means of quantum key distribution, removing insecure cipher suites and introducing a 0-RTT handshake phase.
c) Incorporating strong certificate transparency solutions, adding support to legacy cipher suites for improved backwards compatibility and adding proprietary block ciphers for stronger confidentiality.
d) Reducing the number of rounds in the handshake phase, adding quantum key distribution for security against quantum attacks and removing support for insecure cipher suites.

# GDPR, Privacy and Blockchain

#### Which of the following is NOT a data subject's right according to the GDPR?

a) Being notified by the data processor every time that their data is processed in a manner they have consented to.
b) Being informed by the data processor of how their data will be processed and providing consent to said processing.
c) Requesting that their data is erased.
d) Requesting access to their data held by a data processor.

#### An European company providing Software-as-a-Service solutions processing personal data from costumers uses a datacenter in the United States of America as a backup, storing all of their costumers' plaintext data at this datacenter so that it is readily available in case their main datacenter has availability issues. Since the backup datacenter is managed by a local provider in the USA, the European company has signed a contract with standard contracting clauses (SCC) covering GDPR compliance by the American service provider. What are potential issues with this approach?

a) According to Schrems II, the European company cannot blindly rely on SCCs without taking extra measures to ensure that the American service provider will be GDPR compliant (e.g. understanding how the provider will handle requests by the American government to access personal information).
b) According to current privacy regulations, as long as there is a contract in place binding the American provider to adhere to the GDPR, there is no issue with the approach taken by the European company.
c) If the European company is GDPR compliant, they have no issue in storing their costumers' personal data in any datacenter of their choosing, since the costumers have consented to having their data processed by this company.
d) The GDPR forbids a data processor from storing data subjects' personal data in any datacenter that is not directly owned and managed by the data processor itself.

#### In order to avoid exposing their sensitive information, Alice, Bob and Charlie decided to use a simple protocol to compute the sum total of Christmas parties they have attended without revealing the number of parties they each attended to anyone. Given that A, B and C are the numbers of parties attended by Alice, Bob and Charlie respectively, how can they achieve this goal?

a) Alice, Bob and Charlie can use additive secret sharing to share A, B and C, send one share of their number to each of the other parties, locally add all of their shares of A, B and C, exchange the resulting share among each other and reconstruct the result.
b) Alice, Bob and Charlie can execute the Diffie-Hellman protocol to exchange pairwise symmetric keys, each encrypt their number of parties using a block cipher, exchange the ciphertexts, decrypt the corresponding ciphertext and compute the sum total.
c) Alice, Bob and Charlie can use public key encryption and public keys obtained from a PKI to encrypt their own number of parties under each other's public keys, exchange the ciphertexts, decrypt the ciphertexts obtained from other parties and compute the sum total from the plaintext messages.
d) Alice, Bob and Charlie can use the TLS 1.3 protocol to establish a secure connection to a server running a secure software for validating inputs and computing the addition of all inputs, each send their number of attended parties to the server and receive the result of the addition of their private inputs from the server.


#### What property is NOT provided by a blockchain protocol?

a) All data on the blockchain becomes immutable as soon as it is written.
b) The protocol is permissionless, meaning that parties may join or leave the protocol execution at any time.
c) Honest parties are guaranteed to be able to eventually write their data on the blockchain.
d) The protocol remains secure as long as honest parties control a majority of a constrained resource (e.g. computational power).

# Authentication and Access Control

#### A company is deploying a user authentication system for their employees to access internal systems via their state-of-the-art smartphones. Given the best practices and security principles for authentication systems, what is the best way to design this system?

a) Combining a password serving as knowledge factor with fingerprint biometrics serving as inherence factor.
b) Allowing access only from the company-issued smartphone's MAC address (possession factor) and requiring a simple password (knowledge factor) for better psychological acceptability.
c) Using a one-time password generated by an app on the smartphone as a possession factor. 
d) Using face recognition for better psychological acceptability.

#### What is the recommended method for storing passwords in a database?

a) Storing a hash of the password concatenated with a random string, along with the random string.
b) Storing an encryption of the password using a symmetric key stored elsewhere on the computer.
c) Storing a hash of the password.
d) Storing a digital signature of the password created under a signing key stored elsewhere on the computer.

#### Select the correct statement regarding access control mechanisms.

a) Unix-based systems such as Linux and Mac OS X use discretionary access control and role based access control.
b) In a mandatory access control mechanism, users can mandate arbitrary access rights to objects for each subject.
c) Logging access to objects by different subjects is not part of the responsibilities of an access control system.
d) The SetUID bit in Unix-based systems allows users to assign their user identities to each file.

# Post Quantum Cryptography

#### When a quantum computer capable of running Shor's algorithm is constructed, what is the expected impact on cryptography?

a) Cryptographic schemes that are secure based on the assumed hardness of factoring large integers or computing discrete logarithms (or related problems) will be broken.
b) All current symmetric key and asymmetric key cryptographic schemes will be broken.
c) Such a quantum computer would have no impact on cryptography since known cryptographic schemes are unconditionally secure.
d) Hash functions and block ciphers will be broken but the ElGamal encryption scheme and the Schnorr signature scheme will remain secure.

#### What cryptographic schemes should be adopted for large scale systems deployed on off-the-shelf devices (e.g. current mobile phones) if a quantum computer capable of running Shor's algorithm is constructed?

a) Standardidzed symmetric schemes with appropriately increased key lengths and standardized classical asymmetric schemes based on the hardness of problems not efficiently solvable by Shor's algorithm, such as problems over lattices and error-correcting codes.
b) The ElGamal encryption scheme, the Diffie-Hellman key exchange protocol and the Schnorr signature scheme.
c) Perfectly secure encryption and message authentication codes using symmetric keys obtained by means of quantum key exchange.
d) Proprietary cryptographic algorithms based on chaos theory developed by locally trained artificial intelligence models to thwart Shor's algorithm.

# Pentest

#### Which of the following is a common method for escalating privileges by exploiting a misconfiguration in a Unix-based system?

a) Exploiting SUID files.  
b) Using a weak password. 
c) Phishing attack.
d) Man-in-the-middle attack.

#### Which of the following scenarios is most likely to result in a violation of confidentiality?

a) Performing a SQL injection attack.
b) Performing a network vulnerability scan.
c) Performing a denial-of-service attack on a public-facing web server.
d) Deleting log files to cover tracks.

#### Which of the following statements is TRUE?

a) DNS Spoofing attacks involve redirecting traffic from a legitimate website to a malicious one.
b) SQL Injection attacks are only effective against web applications that use MySQL databases. 
c) Cross-Site Scripting (XSS) attacks can be used to directly modify server-side files.
d) Denial-of-Service (DoS) attacks are primarily used to gain unauthorized access to user accounts.

#### Which of the following statements is FALSE?

a) Cross-Site Scripting (XSS) attacks can be used to execute arbitrary code on the server.
b) SQL Injection attacks can be used to bypass authentication mechanisms.
c) Man-in-the-Middle (MitM) attacks can intercept and alter communication between two parties.
d) Privilege escalation can occur due to misconfigured file permissions. 

#### Given the code snippet below, suggest an adequate fix if necessary
```java
public void getUser(HttpServletRequest request, HttpServletResponse response) throws SQLException, IOException {
	String userId = request.getParameter("id");
	String query = "SELECT * FROM users WHERE id = ?";
	PreparedStatement pstmt = connection.prepareStatement(query);
	pstmt.setString(1, userId);
	ResultSet rs = pstmt.executeQuery();
}
```

a) The code snippet is secure
b) Replace line 3 with `String query = "SELECT * FROM users WHERE id = '" + userId + "'";`
c) Replace line 3 with `String query = "SELECT * FROM users WHERE id = '" + sanitize(userId) + "'";` 
d) Replace line 3 with `String query = "SELECT * FROM users WHERE id = '" + escape(userId) + "'";`

#### The sshd_config file is the configuration file for the SSH daemon (sshd), which handles incoming SSH connections. This file contains various settings that control the behavior and security of the SSH service. The PermitRootLogin option specifies whether the root user is allowed to log in directly via SSH. The PasswordAuthentication option specifies whether password authentication is allowed for SSH connections. The PubkeyAuthentication option specifies whether public key authentication is allowed.
Which of the following SSH configurations reduce the risk of privilege escalation?

a) PermitRootLogin no
  PasswordAuthentication no 
  PubkeyAuthentication yes
b) PermitRootLogin no
  PasswordAuthentication yes 
  PubkeyAuthentication yes
c) PermitRootLogin no
  PasswordAuthentication yes 
  PubkeyAuthentication no
d) PermitRootLogin yes
  PasswordAuthentication yes 
  PubkeyAuthentication yes

#### Consider the directory and file permissions for a web application. Which of the following options offers the best security and ensures the web application’s proper functioning?

a) drwxr-xr-x 2 www-data www-data 4096 Dec  6 09:00 /var/www/html/
  -rw------- 1 www-data www-data 1234 Dec  6 09:00 /var/www/html/config.php
  -rw-r--r-- 1 www-data www-data 5678 Dec  6 09:00 /var/www/html/index.php
b) drwxr-xr-x 2 www-data www-data 4096 Dec  6 09:00 /var/www/html/
  -rw------- 1 www-data www-data 1234 Dec  6 09:00 /var/www/html/config.php
  -r-------- 1 www-data www-data 5678 Dec  6 09:00 /var/www/html/index.php
c) drwxr-xr-x 2 www-data www-data 4096 Dec  6 09:00 /var/www/html/
  -r-------- 1 www-data www-data 1234 Dec  6 09:00 /var/www/html/config.php
  -rw------- 1 www-data www-data 5678 Dec  6 09:00 /var/www/html/index.php
d) drwxrwxrwx 2 www-data www-data 4096 Dec  6 09:00 /var/www/html/
  -rw------- 1 www-data www-data 1234 Dec  6 09:00 /var/www/html/config.php
  -rw------- 1 www-data www-data 5678 Dec  6 09:00 /var/www/html/index.php

#### In a color guessing game, each day is numbered (e.g., today could be Day 15). The server holds a unique secret color for each day, and your objective is to guess the color. The server maintains a SQL table named _answers_ that stores every day’s secret color. The table has two columns: day (an integer) and color (a string).

When you submit a color guess, the server executes the following query, replacing $input with the color you entered:

`SELECT day FROM answers WHERE color = “$input”`

If the query returns a single value that matches today’s day number, the server responds with a webpage displaying a green checkmark. Conversely, the server displays a webpage with a red X.

Now, let’s consider the scenario where today is Day 15 and tomorrow is Day 16. Which of the following inputs would determine whether tomorrow’s color is “blue”?
a) `" UNION SELECT day-1 FROM answers WHERE color = "blue`
b) `" UNION SELECT day FROM answers WHERE color = "blue`
c) `" UNION SELECT "blue" FROM answers WHERE day = 16--`
d) None of the others

# Open Questions

#### A Bitcoin elf called Gammel Nok mined thousands of Bitcoin, which he stored in a hardware wallet left behind in a potato farm in Jutland. Now he wants to leave his Bitcoin wealth to his young friends Fritz, Hansi and Günther. However, since this trio is constantly fighting, Gammel Nok wants to ensure that they can only retrieve the passkey needed to access the hardware wallet if they all come together and collaborate. Gammel Nok is too weak to travel, so he must communicate with the young elves over the Internet. Considering that they all have access to each other's public keys registered in The Big Book, design a solution that allows for Gammel Nok to leave the passkey as inheritance to Fritz, Hansi and Günther in such a way that they can only obtain the passkey if they all collaborate, while preventing Dolev-Yao attackers from learning the passkey. Explain how your solution works and why it achieves the desired goal in terms of security goals and security principles. Tip: consider that the passkey is represented as a random element from a large enough field (so that it is infeasible to guess the passkey).

#### A company has a web shop where each user has a profile containing personal information used for product recommendations. In order to access the web shop a user has to authenticate themselves by means of a password that must be 20 characters long, containing both special characters and numbers. Since users are already logged in when they use the web shop, inputs passed to SQL queries sent to the back end database are not sanitized. Even though the company is based in Europe, it hosts the web shop at datacenter in the United States of America due to lower operational costs. In order to protect data confidentiality and integrity, the company has developed proprietary cryptographic protocols for users to access the web shop. These proprietary protocols allow for complex cipher suites with multiple customizable parameters, which can be chosen by each user according to their privacy needs. In order to facilitate remote access for maintenance, the server is connected directly to the internet, allowing for direct connections to the back end database server, to a back up service and to a web server control panel. Given this scenario, identify the security issues in the web shop solution, the security principles that have been violated and the privacy regulations that have been violated. Propose potential solutions to the issues you have identified.