
## **4. Attacks on RSA**

The security of RSA depends mainly on the difficulty of factoring the modulus `n`. If an attacker, Eve, can factor `n` into `p` and `q`, they can calculate $φ(n)$ and then find the private key `d`.

Here's a breakdown of the attacks mentioned:

### **Factorization Attack**
*   **Goal**: Factor `n` to find `p` and `q`.
*   **Defense**: Use a very large `n` (at least 1024 bits, >300 decimal digits).

### **Chosen-Ciphertext Attack**
- **Scenario**: Bob decrypts arbitrary ciphertexts for Eve (except for a specific ciphertext C).
*   **Method**:
        1. Eve chooses random $X \in Z_n^*$.
        2. Eve calculates $Y = C \times X^e \bmod n$.
        3. Eve asks Bob to decrypt Y, getting $Z = Y^d \bmod n$.
        4. Eve computes $P = Z \times X^{-1} \bmod n$.
            *   *Explanation*: $Z = Y^d = (C \times X^e)^d = (P^e \times X^e)^d = P^{ed} \times X^{ed} = P \times X \pmod{n}$
*   **Defense**: Bob should not decrypt arbitrary ciphertexts.

### **Attacks on the Encryption Exponent (e)**
*   **Low Encryption Exponent Attack (e.g., e = 3)**
	*   **Coppersmith Theorem Attack**: If $e$ is small and a significant portion of the bits of $P$ are known, the attacker can find the complete $P$.
	*   **Broadcast Attack**: If the same message is sent to multiple recipients with the same low $e$, an attacker can use the Chinese Remainder Theorem to recover the message. For example, with $e=3$, if Alice sends $C_1 = P^3 \bmod n_1$, $C_2 = P^3 \bmod n_2$, $C_3 = P^3 \bmod n_3$, Eve can find $C' = P^3 \bmod n_1 n_2 n_3$, then since $P^3 < n_1 n_2 n_3$, Eve can find $P = \sqrt[3]{C'}$.
	*   **Related Message Attack**: If two plaintexts are related by a linear function and encrypted with a low $e$, Eve may recover them.
	*   **Short Pad Attack**: If a message is padded with short random values $r_1$ and $r_2$ and encrypted twice, Eve may recover the original message.
    *   **Defense**: Use a larger `e` (e.g., $e = 2^{16} + 1 = 65537$).

### **Attacks on the Decryption Exponent (d)**
*   **Revealed Decryption Exponent Attack**: If `d` is revealed, Eve can decrypt messages and also factor `n`, compromising the entire system.
*   **Low Decryption Exponent Attack**: If $d < \frac{1}{3}n^{\frac{1}{4}}$ and $q < p < 2q$, Eve can factor `n` efficiently.
*   **Defense**: Ensure $d \geq \frac{1}{3}n^{\frac{1}{4}}$, and regenerate all keys if `d` is compromised.

### **Plaintext Attacks**
*   **Short Message Attack**: If the set of possible plaintexts is small, Eve can encrypt them all and compare them to the ciphertext.
*   **Cycling Attack**: Repeatedly encrypting the ciphertext might eventually yield the plaintext, although the complexity is similar to factoring `n`.
*   **Unconcealed Message Attack**: Some messages encrypt to themselves (e.g., $P=0, P=1$).
*   **Defense**: Pad messages with random bits (e.g., using OAEP).

*   **Attacks on the Modulus**
    *   **Common Modulus Attack**: If multiple users share the same `n`, an attacker who is part of the group can potentially factor `n` and find others' private keys.
    *   **Defense**: Each user must have a unique modulus `n`.

*   **Implementation Attacks**
    *   **Timing Attack**: By measuring the time it takes to perform decryption, Eve can deduce the bits of the private key `d`.
    *   **Power Attack**: Similar to the timing attack but based on power consumption.
    *   **Defense**: Use constant-time algorithms or blinding techniques.
