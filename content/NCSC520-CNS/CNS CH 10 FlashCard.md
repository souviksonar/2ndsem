
#flashcards/Trapdoor_One_Way_Function
QUESTION: What are the three key properties of a trapdoor one-way function (TOWF)?
OPTIONS:
A) Easy to compute, easy to invert, easy to compute with a trapdoor.
B) Difficult to compute, easy to invert, difficult to compute with a trapdoor.
C) Easy to compute, difficult to invert, difficult to compute with a trapdoor.
D) Easy to compute, difficult to invert, easy to compute with a trapdoor.
??
SOLUTION:
D) A TOWF is: 1. Easy to compute in one direction (given $x$, find $y = f(x)$). 2. Difficult to invert (given $y$, find $x$) without special information. 3. Easy to invert with a trapdoor (given $y$ and the trapdoor, find $x$).
<!--SR:!2025-02-17,4,270-->

#flashcards/Trapdoor_One_Way_Function
QUESTION: In the function $n = p \times q$, where $p$ and $q$ are large primes, what is the trapdoor that makes it easy to find $p$ and $q$ given $n$?
OPTIONS:
A) The value of $n$ itself
B) Knowledge of either $p$ or $q$
C) The value of Euler's totient function, $\phi(n)$
D) There is no trapdoor; it is always difficult.
??
SOLUTION:
B) Knowing either $p$ or $q$ makes it trivial to find the other by dividing $n$ by the known factor.  This knowledge acts as the trapdoor.
<!--SR:!2025-02-17,4,270-->

#flashcards/Trapdoor_One_Way_Function
QUESTION:  For the trapdoor one-way function $y = x^k \mod n$, what constitutes the "trapdoor" that allows easy computation of $x$ given $y$, $k$, and $n$?
OPTIONS:
A) Knowing the value of $n$.
B) Knowing a value $k'$ such that $k \times k' \equiv 1 \pmod{\phi(n)}$.
C) Knowing the value of $k$.
D) Knowing the value of $y$.
??
SOLUTION:
B) The trapdoor is knowing $k'$, the modular multiplicative inverse of $k$ modulo $\phi(n)$. This allows us to compute $x = y^{k'} \mod n$. This is the basis of RSA.
<!--SR:!2025-02-17,4,270-->

#flashcards/RSA_Cryptosystem
QUESTION: In RSA, what are the two main mathematical operations used for encryption and decryption, respectively?
OPTIONS:
A) Modular addition and modular subtraction.
B) Modular multiplication and modular division.
C) Modular exponentiation (both).
D) Factorization and discrete logarithm.
??
SOLUTION:
C) Both encryption and decryption in RSA involve modular exponentiation.  Encryption is $C = P^e \pmod{n}$, and decryption is $P = C^d \pmod{n}$.
<!--SR:!2025-02-17,4,270-->

#flashcards/RSA_Cryptosystem
QUESTION:  In RSA, what is the relationship between the public exponent *e*, the private exponent *d*, and Euler's totient function *φ(n)*?
OPTIONS:
A) $e + d \equiv 1 \pmod{n}$
B) $e \times d \equiv 1 \pmod{\phi(n)}$
C) $e \times d \equiv 1 \pmod{n}$
D) $e + d \equiv 1 \pmod{\phi(n)}$
??
SOLUTION:
B) The public exponent $e$ and the private exponent $d$ are modular multiplicative inverses modulo $\phi(n)$.  That is, $e \times d \equiv 1 \pmod{\phi(n)}$.
<!--SR:!2025-02-17,4,270-->

#flashcards/RSA_Cryptosystem
QUESTION: What is the recommended minimum size (in bits) of the modulus *n* in RSA for secure communication today?
OPTIONS:
A) 128 bits
B) 256 bits
C) 512 bits
D) 1024 bits
??
SOLUTION:
D) 1024 bits is the currently recommended minimum size for the modulus *n* in RSA, though larger sizes (e.g., 2048 bits) are often used for increased security.
<!--SR:!2025-02-17,4,270-->

#flashcards/RSA_Cryptosystem
QUESTION: Explain why revealing the private exponent *d* in RSA compromises the entire system, even if the modulus *n* remains the same.
OPTIONS:
A) Knowing *d* allows direct decryption of any ciphertext.
B) Knowing *d* allows easy calculation of *e*.
C) Knowing *d* and *n* allows efficient factorization of *n*.
D) All of the above.
??
SOLUTION:
D) All of the above. Knowing *d* allows direct decryption. While *e* is public, knowing *d* also compromises future security because *d* and *e* are inverses modulo *φ(n)*, and knowing *d*, *e*, and *n* enables efficient factorization of *n* (finding *p* and *q*), thus completely breaking the system.
<!--SR:!2025-02-17,4,270-->

#flashcards/RSA_Attacks
QUESTION: Name at least three potential attacks on RSA.
OPTIONS:
 A)  Brute-force, birthday, and man-in-the-middle attacks.
 B) Factorization, chosen-ciphertext, and timing attacks.
 C)  Differential, linear, and integral cryptanalysis.
 D) Known-plaintext, replay, and denial-of-service attacks.
??
SOLUTION:
B) Factorization attacks try to find *p* and *q* from *n*. Chosen-ciphertext attacks exploit the multiplicative property of RSA. Timing attacks try to deduce the private key by measuring the time it takes to perform decryption. Other attacks include low encryption/decryption exponent attacks, and implementation attacks.
<!--SR:!2025-02-17,4,270-->

#flashcards/RSA_Attacks
QUESTION: What is the Coppersmith theorem attack, and what parameter of RSA does it target?
OPTIONS:
A) It targets the modulus *n*, aiming to factor it.
B) It targets the private exponent *d*, trying to find it.
C) It targets low encryption exponents *e*.
D) It targets the implementation, exploiting timing differences.
??
SOLUTION:
C) The Coppersmith theorem attack is a major attack targeting low encryption exponents *e*. It states that if a polynomial of degree *e* has a root smaller than *n^(1/e)*, that root can be found efficiently.
<!--SR:!2025-02-17,4,270-->

#flashcards/RSA_Attacks
QUESTION:  Explain the basic principle of a timing attack on RSA.
OPTIONS:
A) It exploits weaknesses in the random number generator.
B) It measures the time taken for encryption to deduce the public key.
C) It measures the time taken for decryption to deduce bits of the private key.
D) It exploits the use of a common modulus among multiple users.
??
SOLUTION:
C) Timing attacks exploit the fact that different operations in the modular exponentiation algorithm (used in RSA decryption) take different amounts of time. By carefully measuring the decryption time for many ciphertexts, an attacker can deduce information about the bits of the private exponent *d*.
<!--SR:!2025-02-17,4,270-->

#flashcards/RSA_Attacks
QUESTION: What is the purpose of Optimal Asymmetric Encryption Padding (OAEP) in RSA?
OPTIONS:
A)  To speed up encryption.
B) To speed up decryption.
C) To prevent certain attacks, such as chosen-ciphertext and short message attacks.
D) To reduce the size of the ciphertext.
??
SOLUTION:
C) OAEP is a padding scheme that adds randomness and structure to the plaintext before encryption. This helps prevent various attacks, including chosen-ciphertext attacks and attacks that exploit short or structured messages.
<!--SR:!2025-02-17,4,270-->

#flashcards/Rabin_Cryptosystem
QUESTION:  The Rabin cryptosystem can be considered a special case of RSA. What are the fixed values of the public exponent *e* and the private exponent *d* in the Rabin cryptosystem?
OPTIONS:
 A) $e = 1$, $d = 1$
 B) $e = 2$, $d = 1/2$
 C) $e = 3$, $d = 1/3$
 D) $e = \phi(n)$, $d = 1$
??
SOLUTION:
B) In the Rabin cryptosystem, encryption is squaring modulo *n* ($e = 2$), and decryption is finding the square root modulo *n* ($d = 1/2$).
<!--SR:!2025-02-17,4,270-->

#flashcards/Rabin_Cryptosystem
QUESTION:  A key characteristic of the Rabin cryptosystem is that decryption is not deterministic. Explain what this means.
OPTIONS:
 A)  Decryption always fails.
 B) Decryption produces a random result.
 C)  Decryption produces multiple possible plaintexts.
 D) Decryption is very slow.
??
SOLUTION:
C) Decryption in the Rabin cryptosystem produces four possible plaintexts. This is because finding the square root modulo *n* (where *n* is the product of two primes) generally has four solutions.
<!--SR:!2025-02-17,4,270-->

#flashcards/Rabin_Cryptosystem
QUESTION: To make decryption easier in Rabin cryptosystem, what form should prime p and q take ?
OPTIONS:
    A) 4k + 1
    B) 4k + 3
    C) 2k + 1
    D) k^2
??
SOLUTION:
    B) 4k + 3
<!--SR:!2025-02-17,4,270-->

#flashcards/ElGamal_Cryptosystem
QUESTION: The ElGamal cryptosystem is based on what hard mathematical problem?
OPTIONS:
A) The integer factorization problem.
B) The discrete logarithm problem.
C) The quadratic residuosity problem.
D) The elliptic curve discrete logarithm problem.
??
SOLUTION:
B) The security of ElGamal relies on the difficulty of solving the discrete logarithm problem in a finite field.
<!--SR:!2025-02-17,4,270-->

#flashcards/ElGamal_Cryptosystem
QUESTION: In ElGamal encryption, what is the role of the random number *r* chosen by the sender (Alice)?
OPTIONS:
 A)  It is used to generate the public key.
 B)  It is used to mask the plaintext.
 C)  It is used to decrypt the message.
 D) It is part of the private key.
??
SOLUTION:
B) The random number *r* is used to create a "mask" ($e_2^r$) that hides the plaintext. This ensures that even if the same message is encrypted multiple times, the ciphertext will be different.
<!--SR:!2025-02-17,4,270-->

#flashcards/ElGamal_Cryptosystem
QUESTION:  In ElGamal, if the public key is $(e_1, e_2, p)$ and the private key is $d$, and Alice sends ciphertext $(C_1, C_2)$, how does Bob decrypt the message to recover the plaintext $P$?
OPTIONS:
A)  $P = C_1 \times (C_2^d)^{-1} \pmod{p}$
B) $P = C_2 \times (C_1^d)^{-1} \pmod{p}$
C) $P = C_1^d \times C_2 \pmod{p}$
D)  $P = C_2^d \times C_1 \pmod{p}$
??
SOLUTION:
B) Bob decrypts by calculating $P = C_2 \times (C_1^d)^{-1} \pmod{p}$.  This effectively removes the mask created by Alice during encryption.
<!--SR:!2025-02-17,4,270-->

#flashcards/Elliptic_Curve_Cryptography
QUESTION: Elliptic Curve Cryptography (ECC) offers a security advantage over RSA and ElGamal for the same level of security. What is this main advantage?
OPTIONS:
 A)  Faster encryption speeds.
 B) Smaller key sizes.
 C)  Simpler implementation.
 D) Resistance to quantum computer attacks.
??
SOLUTION:
B) ECC can achieve the same level of security as RSA and ElGamal with significantly smaller key sizes. This makes it particularly attractive for resource-constrained environments.
<!--SR:!2025-02-17,4,270-->

#flashcards/Elliptic_Curve_Cryptography
QUESTION: The security of ECC relies on the difficulty of which mathematical problem?
OPTIONS:
A) Integer factorization
B) Discrete logarithm
C) Elliptic curve discrete logarithm
D) Quadratic residuosity
??
SOLUTION:
C) Elliptic curve discrete logarithm.  This problem involves finding the scalar multiplier *k* given a point *P* and the result of *kP* (where *kP* represents scalar multiplication of a point on an elliptic curve).
<!--SR:!2025-02-17,4,270-->

Okay, here are 30 more questions, focused specifically on the topics you requested (RSA, RSA Attacks, Rabin, ElGamal, and Elliptic Curve Cryptography), and maintaining the same format:

#flashcards/RSA_Cryptosystem
QUESTION: In RSA, if $p = 11$ and $q = 13$, what is the value of $\phi(n)$?
OPTIONS:
A) 143
B) 120
C) 24
D) 132
??
SOLUTION:
B) $\phi(n) = (p-1)(q-1) = (11-1)(13-1) = 10 \times 12 = 120$.

#flashcards/RSA_Cryptosystem
QUESTION: If Bob chooses $p=7$ and $q=17$ for his RSA keys, and he chooses $e=5$, what is a valid value for his private key, $d$?
OPTIONS:
A) 23
B) 77
C) 5
D) 96
??
SOLUTION:
B) 77

#flashcards/RSA_Attacks
QUESTION: The "Common Modulus Attack" on RSA becomes feasible when:
OPTIONS:
A) The same message is sent to multiple recipients.
B) A small encryption exponent is used.
C) Multiple users share the same modulus *n*, but have different exponent pairs.
D) The private exponent is revealed.
??
SOLUTION:
C) The Common Modulus Attack is possible when different users share the same modulus *n* but have different public/private exponent pairs (e, d). This allows an attacker, who is also a member of the community, to potentially factor *n* and compromise the security of other users.

#flashcards/RSA_Attacks
QUESTION: Explain how "blinding" can be used to mitigate timing attacks on RSA.
OPTIONS:
A) Blinding adds random delays to the encryption process.
B) Blinding involves multiplying the ciphertext by a random number before decryption.
C) Blinding involves using a larger modulus.
D) Blinding encrypts the message twice.
??
SOLUTION:
B) Blinding involves multiplying the ciphertext by a random number before decryption. This randomizes the intermediate values during the modular exponentiation, making it harder for an attacker to correlate timing information with the private key.

#flashcards/RSA_Attacks
QUESTION: Which attack can be mitigated if d >= 1/3 n^(1/4)
OPTIONS:
A) Chosen-ciphertext attack.
B)  Low Decryption Exponent Attack.
C)  Common modulus attack.
D) Revealed Decryption Exponent Attack.
??
SOLUTION:

B) Low Decryption Exponent Attack.

#flashcards/Rabin_Cryptosystem
QUESTION: What is the primary advantage of the Rabin cryptosystem in terms of computational efficiency?
OPTIONS:
A) Decryption is faster than RSA.
B) Key generation is faster than RSA.
C) Encryption is faster than RSA.
D) It uses smaller keys than RSA.
??
SOLUTION:
C) Encryption in the Rabin cryptosystem is very fast, requiring only a single modular squaring operation ($C = P^2 \pmod{n}$).

#flashcards/Rabin_Cryptosystem
QUESTION: If Bob uses the Rabin cryptosystem with $p = 19$ and $q = 23$, what is the public key?
OPTIONS:
A) (19, 23)
B) 437
C) 18
D) 22
??
SOLUTION:
B) The public key in the Rabin cryptosystem is the modulus $n = p \times q = 19 \times 23 = 437$.

#flashcards/Rabin_Cryptosystem
QUESTION: Describe a method Bob can use to select the correct plaintext from the four possible plaintexts produced during Rabin decryption.
OPTIONS:
 A) Bob cannot determine the correct plaintext.
 B) Bob chooses the smallest of the four plaintexts.
 C) Bob uses a pre-shared secret with Alice to identify the correct plaintext.
 D) Bob relies on context, redundancy, or a pre-agreed upon method (like padding) within the message itself.
??
SOLUTION:
D) Because Rabin decryption produces four possible plaintexts, Bob must use additional information to choose the correct one. This could involve examining the context of the message, looking for expected redundancy or padding added before encryption, or using some pre-agreed upon selection criteria.

#flashcards/ElGamal_Cryptosystem
QUESTION: In ElGamal, if $p = 23$, $e_1 = 5$ (a primitive root mod 23), and $d = 6$, what is the public key component $e_2$?
OPTIONS:
A) 15625
B) 17
C) 8
D) 6
??
SOLUTION:
C) $e_2 = e_1^d \pmod{p} = 5^6 \pmod{23} = 15625 \pmod{23} = 8$.

#flashcards/ElGamal_Cryptosystem
QUESTION: If Alice wants to send the message $P = 9$ to Bob using ElGamal, and Bob's public key is $(e_1 = 5, e_2 = 8, p = 23)$, and Alice chooses the random number $r = 3$, what is the ciphertext $(C_1, C_2)$?
OPTIONS:
A) (125, 72)
B) (6, 16)
C) (5, 9)
D) (10, 8)
??
SOLUTION:
(10, 8)
D) is correct

#flashcards/ElGamal_Cryptosystem
QUESTION: How can the ElGamal cryptosystem avoid the computation of a modular multiplicative inverse during decryption?
OPTIONS:
A) By using a different encryption formula.
B) By using Fermat's Little Theorem.
C) By precomputing the inverse.
D) By choosing a different value for *p*.
??
SOLUTION:
B) By using Fermat's Little Theorem, we know that $a^{p-1} \equiv 1 \pmod{p}$ for a prime *p* and *a* not divisible by *p*.  Therefore, $a^{-1} \equiv a^{p-2} \pmod{p}$.  This allows us to replace the inverse calculation with a modular exponentiation:  $P = C_2 \times C_1^{p-1-d} \pmod{p}$.

#flashcards/Elliptic_Curve_Cryptography
QUESTION: What is the general form of the simplified equation used for elliptic curves over real numbers in cryptography?
OPTIONS:
A) $y = x^3 + ax + b$
B) $y^2 = x^3 + ax + b$
C) $y^2 = x^2 + ax + b$
D) $y = x^2 + ax + b$
??
SOLUTION:
B) The simplified form commonly used is $y^2 = x^3 + ax + b$, where $4a^3 + 27b^2 \neq 0$ to ensure it's a non-singular curve.

#flashcards/Elliptic_Curve_Cryptography
QUESTION:  If a point $P = (x, y)$ is on an elliptic curve, what is its inverse, $-P$?
OPTIONS:
A) $(-x, y)$
B) $(x, -y)$
C) $(-x, -y)$
D) $(1/x, 1/y)$
??
SOLUTION:
B) The inverse of a point $P = (x, y)$ on an elliptic curve is simply its reflection across the x-axis, which is $(x, -y)$.

#flashcards/Elliptic_Curve_Cryptography
QUESTION: If we are working with an elliptic curve over GF(p), and we have a point P = (3, 5) and p = 17. What is the additive inverse of the point P ?
OPTIONS:
A) (3,12)
B) (14,5)
C) (14,12)
D) (3,5)
??
SOLUTION:
A) The additive inverse on GF(p) is calculated (x, -y mod p). Here -y=-5, and -5 mod 17 = 12. The additive inverse is therefore (3, 12)

#flashcards/Elliptic_Curve_Cryptography
QUESTION: In elliptic curve cryptography over GF(2^n), what is commonly used to represent the elements of the field?
OPTIONS:
    A) Integers
    B) Rational Numbers
    C) Polynomials with coefficients in GF(2)
    D) Complex Numbers
??
SOLUTION:
    C) Polynomials with coefficients in GF(2)

#flashcards/RSA_Attacks
QUESTION: What vulnerability does OAEP attempt to address in RSA?
A) Factorization of the modulus
B) Small private exponent
C) Small public exponent, chosen-ciphertext, and short-message attacks
D) Timing attacks
??
SOLUTION:
C) Small public exponent, chosen-ciphertext, and short-message attacks

#flashcards/RSA_Attacks
QUESTION: True or False: If the decryption exponent *d* in RSA is compromised, it is sufficient for Bob to simply choose a new *d* while keeping the same modulus *n*.
OPTIONS:
A) True
B) False
??
SOLUTION:
B) False.  If *d* is compromised, an attacker can likely factor *n* and thus derive any new *d* associated with that *n*.  Bob must regenerate *p*, *q*, *n*, *e*, and *d*.

#flashcards/RSA_Attacks
QUESTION: Explain how a chosen-ciphertext attack can work against basic RSA (without padding).
OPTIONS:
A) The attacker chooses random ciphertexts and tries to decrypt them.
B) The attacker intercepts a ciphertext, modifies it in a specific way, and tricks the recipient into decrypting the modified ciphertext.  By observing the result, the attacker can learn the original plaintext.
C) The attacker tries all possible private keys.
D) The attacker measures the power consumption during decryption.
??
SOLUTION:
B) The attacker intercepts a ciphertext $C = P^e \pmod{n}$.  They choose a random value *X*, compute $Y = C \cdot X^e \pmod{n}$, and get the recipient to decrypt *Y*.  The recipient returns $Z = Y^d \pmod{n}$. The attacker can then compute $P = Z \cdot X^{-1} \pmod{n}$.

#flashcards/RSA_Cryptosystem
QUESTION: Explain, in high-level terms, why RSA is considered a "trapdoor one-way function."
OPTIONS:
A) Encryption is easy, and decryption is easy for everyone.
B) Encryption is hard, and decryption is easy.
C) Encryption is easy, and decryption is hard without knowing the private key (the trapdoor).
D) Encryption is hard, and decryption is also hard.
??
SOLUTION:
C) Encryption (using the public key) is computationally easy. Decryption is computationally infeasible without knowing the private key, which serves as the "trapdoor" that makes decryption easy for the legitimate recipient.

#flashcards/Rabin_Cryptosystem
QUESTION: Why is it important for *p* and *q* to be congruent to 3 modulo 4 in the Rabin cryptosystem?
OPTIONS:
A) To ensure that *n* is large enough.
B) To make encryption faster.
C) To simplify the process of finding square roots modulo *p* and *q* during decryption.
D) To make the public key smaller.
??
SOLUTION:
C) When *p* and *q* are congruent to 3 modulo 4, there are efficient formulas for computing square roots modulo *p* and *q*, which simplifies the decryption process in the Rabin cryptosystem.

#flashcards/ElGamal_Cryptosystem
QUESTION: Why is it crucial for Alice to choose a fresh random number *r* for each message she encrypts using ElGamal?
OPTIONS:
A) To prevent the reuse of the same public key.
B) To prevent known-plaintext attacks.
C) To speed up encryption.
D) To simplify decryption.
??
SOLUTION:
B) If Alice reuses the same *r* for different messages, an attacker who knows one plaintext/ciphertext pair can easily decrypt other messages encrypted with the same *r*.

#flashcards/Elliptic_Curve_Cryptography
QUESTION: Describe the "addition" operation for two distinct points P and Q on an elliptic curve over a real field (geometrically).
OPTIONS:
A) Draw a line between P and Q, and the third intersection point with the curve is P+Q.
B) Draw a line between P and Q, find the third intersection point with the curve, and reflect that point across the x-axis. This reflection is P+Q.
C) Add the x-coordinates and y-coordinates of P and Q separately.
D) Multiply the x-coordinates and y-coordinates of P and Q separately.
??
SOLUTION:
B) To add two distinct points P and Q, you draw a line connecting them. This line will intersect the elliptic curve at a third point. Reflect this third point across the x-axis to obtain the result, P+Q.

#flashcards/Elliptic_Curve_Cryptography
QUESTION: What is the identity element (often denoted as "O") in the abelian group defined over an elliptic curve?
OPTIONS:
A) The origin (0, 0).
B) The point at infinity.
C) (1, 1).
D) There is no identity element.
??
SOLUTION:
B) The identity element is the "point at infinity," denoted as O.  It plays the role of the additive identity: P + O = P for any point P on the curve.

#flashcards/RSA_Attacks
QUESTION: What is meant by a "short pad attack" in the context of RSA and how does it work?
OPTIONS:
A) Uses small values for padding, resulting in small plain text values, making easier to attack using bruteforce.
B)  If the same message is encrypted twice with short, different random pads, an attacker might be able to recover the original message.
C) The pad used has a predictable pattern
D)  It shortens attack time by half.
??
SOLUTION:
B) If the same message is encrypted twice with short, different random pads, an attacker might be able to recover the original message.

#flashcards/RSA_Attacks
QUESTION: What is a "related message attack", give an example?
OPTIONS:
A) A birthday attack
B)  If two plaintexts are related by a linear function and encrypted with e=3. Eve, the attacker, can recover P1 and P2 in a feasible computation of time.
C) Use same public exponent for all recipients, to whom the same message has been sent.
D) Measures power consuption during decryption.
??
SOLUTION:
B)  If two plaintexts are related by a linear function and encrypted with e=3. Eve, the attacker, can recover P1 and P2 in a feasible computation of time.

#flashcards/ElGamal_Cryptosystem
QUESTION: In ElGamal encryption, if the public key is (e1,e2,p), what is the formula for the ciphertext, pair (c1,c2) given plain text, P?
OPTIONS:
A) C1 = e1^P mod p, C2= r x e2^P mod p
B) C1 = e2^r mod p, C2 = e1^r x P mod p
C) C1 = e1^r mod p, C2= r x P mod p
D) C1 = e1^r mod p, C2 = e2^r x P mod p
??
SOLUTION:
D) C1 = e1^r mod p, C2 = e2^r x P mod p

#flashcards/ElGamal_Cryptosystem
QUESTION: In ElGamal, given ciphertext (c1,c2) and private key *d* with public prime *p*, what is formula for *P*?
OPTIONS:
A) P =  [c2 * (c1^d)] mod p
B) P = [c1 * (c2)^(-1)] mod p
C)  P = [c2 * (c1^d)^(-1)] mod p
D) P = [c1 * (c2^d)] mod p
??
SOLUTION:
C) P = [c2 * (c1^d)^(-1)] mod p

#flashcards/Elliptic_Curve_Cryptography
QUESTION: What is an elliptic curve over GF(p)?
OPTIONS:
    A)  An elliptic curve using complex numbers.
    B) An elliptic curve using modular arithmetic with a prime modulus *p*.
    C) An elliptic curve where all points have integer coordinates.
    D) Same points but different operations.
??
SOLUTION:
B) An elliptic curve using modular arithmetic with a prime modulus *p*.
