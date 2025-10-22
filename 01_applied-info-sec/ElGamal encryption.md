---
course:
  - Applied Information Security
---
## Quick recap
Sender computes a ciphertext $(c1,c2)$ for message $m$ with ephemeral random $r$:
- $c_1 = g^r \bmod p$
- $c_2 = m \cdot PK^r$ where $PK = g^x$ is the recipients public key.

Decryption (by holder of private key $x$) does:
- $s = c_1^x = g^{rx} = PK^r \bmod p$
- $m = c_2 \cdot s^{-1} \bmod p$
### 🔑 Recall how ElGamal encryption works

When the **sender** encrypts a message `m`:

1. They choose a random **one-time random key** `r`.
    - This is a one-time random number.
    - It changes every time a message is encrypted, even if the recipient and the plaintext are the same.
2. They compute:
    - $c_1 = g^r \bmod p$
    - $c_2 = m \cdot PK^r \bmod p$
3. They send `(c1, c2)` as the ciphertext.

### 🧮 What happens in decryption?

The recipient knows:

- Their **private key** `x`
- The ciphertext `(c1, c2)`

They compute the **shared secret**:

$s = {c_1}^x \bmod p$

Substitute `c1 = g^r`:

$$ s = (g^r)^x \bmod p = g^{rx} \bmod p $$

But recall the sender also computed `PK^r = (g^x)^r = g^{xr}` during encryption.

So both sides end up with the **same shared secret `s`** without ever revealing `r` or `x`.