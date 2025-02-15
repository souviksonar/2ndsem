Okay, here are 30 questions based on the provided PDF, formatted as requested for postgraduate students:

#flashcards/Primes_Definition
QUESTION: What are the three groups that positive integers can be divided into?
OPTIONS:
A) Odd, Even, and Zero
B) Prime, Composite, and Unit
C) 1, Primes, and Composites
D) Positive, Negative, and Zero
??
SOLUTION:
C) 1, Primes, and Composites.  The positive integers are divided into the number 1 (which has exactly one divisor), primes (which have exactly two divisors), and composites (which have more than two divisors).
<!--SR:!2025-02-17,4,270-->

#flashcards/Primes_Definition
QUESTION:  A positive integer $p > 1$ is considered prime if its only divisors are:
OPTIONS:
A) 1 and $p$
B) 0 and $p$
C) 1 and 2
D) Only itself
??
SOLUTION:
A) 1 and $p$. This is the definition of a prime number.
<!--SR:!2025-02-17,4,270-->

#flashcards/Primes_Definition
QUESTION: Is the number 1 considered a prime number? Why or why not?
OPTIONS:
A) Yes, because it is only divisible by itself.
B) No, because it only has one divisor, not two distinct divisors.
C) Yes, because it is the smallest positive integer.
D) No, because it is considered a unit.
??
SOLUTION:
B) No, because it only has one divisor, not two distinct divisors. The definition of a prime number requires exactly two distinct positive divisors: 1 and the number itself.
<!--SR:!2025-02-17,4,270-->

#flashcards/Coprimes
QUESTION: Two positive integers $a$ and $b$ are coprime if:
OPTIONS:
A) $gcd(a, b) = a$
B) $gcd(a, b) = b$
C) $gcd(a, b) = 1$
D) $gcd(a, b) = 0$
??
SOLUTION:
C) $gcd(a, b) = 1$. This is the definition of coprime (or relatively prime) numbers.
<!--SR:!2025-02-17,4,270-->

#flashcards/Number_of_Primes
QUESTION: The number of primes is:
OPTIONS:
A) Finite and small
B) Finite and large
C) Infinite
D) Unknown
??
SOLUTION:
C) Infinite.  The provided text gives an informal proof of this.
<!--SR:!2025-02-17,4,270-->

#flashcards/Prime_Approximation
QUESTION: Which mathematician(s) discovered the upper and lower limit approximations for $\pi(n)$, the number of primes less than or equal to $n$?
OPTIONS:
A) Euler
B) Fermat
C) Gauss and Lagrange
D) Eratosthenes
??
SOLUTION:
C) Gauss and Lagrange. Gauss discovered the upper limit, and Lagrange discovered the lower limit.
<!--SR:!2025-02-17,4,270-->

#flashcards/Prime_Approximation
QUESTION: Provide the lower bound approximation for the function  $\pi(n)$, which represents the number of primes less than or equal to $n$.
OPTIONS:
A) $\frac{n}{\ln n}$
B) $\frac{n}{\ln n - 1.08366}$
C) $n \times \ln n$
D) $n!$
??
SOLUTION:
A) $\frac{n}{\ln n}$
<!--SR:!2025-02-17,4,270-->

#flashcards/Prime_Checking
QUESTION:  To check if a number $n$ is prime using the basic divisibility test, you need to check for divisibility by all primes less than or equal to:
OPTIONS:
A) $n$
B) $n/2$
C) $\sqrt{n}$
D) $n-1$
??
SOLUTION:
C) $\sqrt{n}$. This is a fundamental optimization in primality testing.
<!--SR:!2025-02-17,4,270-->

#flashcards/Sieve_of_Eratosthenes
QUESTION:  The Sieve of Eratosthenes is a method for finding:
OPTIONS:
A) The greatest common divisor of two numbers.
B) All prime numbers up to a specified integer.
C) The least common multiple of two numbers.
D) The multiplicative inverse of a number.
??
SOLUTION:
B) All prime numbers up to a specified integer.
<!--SR:!2025-02-17,4,270-->

#flashcards/Euler_Phi_Function
QUESTION: Euler's totient function, $\phi(n)$, calculates:
OPTIONS:
A) The sum of all integers less than $n$.
B) The number of integers less than $n$ that are relatively prime to $n$.
C) The largest prime factor of $n$.
D) The number of divisors of $n$.
??
SOLUTION:
B) The number of integers less than $n$ that are relatively prime to $n$.
<!--SR:!2025-02-17,4,270-->

#flashcards/Euler_Phi_Function
QUESTION: If $p$ is a prime number, what is $\phi(p)$?
OPTIONS:
A) $p$
B) $p - 1$
C) $p + 1$
D) 1
??
SOLUTION:
B) $p - 1$. Because all numbers from 1 to $p-1$ are relatively prime to a prime number $p$.
<!--SR:!2025-02-17,4,270-->

#flashcards/Euler_Phi_Function
QUESTION: Calculate $\phi(35)$.
OPTIONS:
A) 20
B) 24
C) 30
D) 34
??
SOLUTION:
B) 24. $\phi(35) = \phi(5 \times 7) = \phi(5) \times \phi(7) = (5-1) \times (7-1) = 4 \times 6 = 24$.
<!--SR:!2025-02-17,4,270-->

#flashcards/Euler_Phi_Function
QUESTION: Calculate $\phi(2^3)$.
OPTIONS:
A) 2
B) 3
C) 4
D) 8
??
SOLUTION:
C) 4. Using the rule, $\phi(p^e) = p^e - p^{e-1}$. Hence, $\phi(2^3) = 2^3 - 2^2= 8 - 4 = 4$.
<!--SR:!2025-02-17,4,270-->

#flashcards/Fermats_Little_Theorem
QUESTION: State the first version of Fermat's Little Theorem.
OPTIONS:
A) If $p$ is prime and $a$ is any integer, then $a^p \equiv a \pmod{p}$.
B) If $p$ is prime and $p$ does not divide $a$, then $a^{p-1} \equiv 1 \pmod{p}$.
C) If $p$ is prime, then $a^{p-1} \equiv 1 \pmod{p}$ for all integers $a$.
D) $a^{p} \equiv a \pmod p$ if and only if p is a prime.
??
SOLUTION:
B) If $p$ is prime and $p$ does not divide $a$, then $a^{p-1} \equiv 1 \pmod{p}$.
<!--SR:!2025-02-17,4,270-->

#flashcards/Fermats_Little_Theorem
QUESTION: Using Fermat's Little Theorem, find the result of $5^{16} \pmod{17}$.
OPTIONS:
A) 0
B) 1
C) 5
D) 16
??
SOLUTION:
B) 1. Since 17 is prime and doesn't divide 5, according to Fermat's Little Theorem, $5^{17-1} \equiv 5^{16} \equiv 1 \pmod{17}$.
<!--SR:!2025-02-17,4,270-->

#flashcards/Fermats_Little_Theorem
QUESTION: According to Fermat's little theorem, if  `p` is a prime and `p` does not divide `a` then the multiplicative inverse $a^{-1}\pmod{p}$ is equal to:
OPTIONS:
	A) $a^{p-1} \pmod p$
	B) $a^{p-2} \pmod p$
	C) $a^{p} \pmod p$
	D) $a \pmod p$
??
SOLUTION:
B) $a^{p-2} \pmod p$
<!--SR:!2025-02-17,4,270-->

#flashcards/Eulers_Theorem
QUESTION: State the first version of Euler's Theorem.
OPTIONS:
A) If $a$ and $n$ are coprime, then $a^n \equiv 1 \pmod{n}$.
B) If $a$ and $n$ are coprime, then $a^{\phi(n)} \equiv 1 \pmod{n}$.
C) $a^{\phi(n)} \equiv 1 \pmod{n}$ for all integers $a$ and $n$.
D) If $n$ is prime, then $a^{\phi(n)} \equiv 1 \pmod{n}$.
??
SOLUTION:
B) If $a$ and $n$ are coprime, then $a^{\phi(n)} \equiv 1 \pmod{n}$.
<!--SR:!2025-02-17,4,270-->

#flashcards/Eulers_Theorem
QUESTION: Compute $7^{12} \pmod{15}$ using Euler's Theorem
OPTIONS:
A) 1
B) 7
C) 8
D) 112
??
SOLUTION:
A) 1. Because $\phi(15) = \phi(3) \times \phi(5) = 2 \times 4 = 8$. Since gcd(7,15)=1. Thus using Euler's Theorem, $7^8 \equiv 1 \pmod{15}$. $7^{12} \equiv 7^{8} \times 7^4 \equiv 1 \times 7^4  \pmod{15}$. Also, $7^2 \equiv 49 \equiv 4 \pmod{15}$, then $7^4 \equiv 4^2 \equiv 16 \equiv 1\pmod{15}$.
<!--SR:!2025-02-17,4,270-->

#flashcards/Mersenne_Primes
QUESTION: A Mersenne prime is a prime number of the form:
OPTIONS:
A) $2^p + 1$, where $p$ is prime.
B) $2^p - 1$, where $p$ is prime.
C) $p^2 - 1$, where $p$ is prime.
D) $p^2 + 1$, where $p$ is prime.
??
SOLUTION:
B) $2^p - 1$, where $p$ is prime.
<!--SR:!2025-02-17,4,270-->

#flashcards/Fermat_Primes
QUESTION: A Fermat number is of the form:
OPTIONS:
A) $2^n + 1$
B) $2^{2^n} + 1$
C) $2^n - 1$
D) $2^{2^n} - 1$
??
SOLUTION:
B) $2^{2^n} + 1$
<!--SR:!2025-02-17,4,270-->

#flashcards/Primality_Testing
QUESTION: What are the two broad categories of primality testing algorithms?
OPTIONS:
A) Fast and Slow
B) Simple and Complex
C) Deterministic and Probabilistic
D) Integer and Floating-Point
??
SOLUTION:
C) Deterministic and Probabilistic
<!--SR:!2025-02-17,4,270-->

#flashcards/Primality_Testing_Divisibility
QUESTION:  The bit-operation complexity of the divisibility algorithm for primality testing is:
OPTIONS:
A) Polynomial
B) Exponential
C) Logarithmic
D) Linear
??
SOLUTION:
B) Exponential
<!--SR:!2025-02-17,4,270-->

#flashcards/AKS_Algorithm
QUESTION: The AKS primality test has a bit-operation time complexity of:
OPTIONS:
A) $O(\sqrt{n})$
B) $O(n^2)$
C) $O((\log n)^{12})$
D) $O(2^n)$
??
SOLUTION:
C) $O((\log n)^{12})$.  This is a simplified representation; refinements can lower the exponent.
<!--SR:!2025-02-17,4,270-->

#flashcards/Probabilistic_Algorithms
QUESTION: In a probabilistic primality test, if the integer being tested is actually prime, the algorithm will return:
OPTIONS:
A) Composite
B) Prime
C) Maybe Prime
D) Unknown
??
SOLUTION:
B) Prime
<!--SR:!2025-02-17,4,270-->

#flashcards/Probabilistic_Algorithms
QUESTION: If a probabilistic primality test returns "composite", what is the probability range with which the input number is composite?
OPTIONS:
	A) 0
	B) 1
	C) 1-$\epsilon$
	D) $\epsilon$
??
SOLUTION:
C) 1-$\epsilon$
<!--SR:!2025-02-17,4,270-->

#flashcards/Fermat_Test
QUESTION: The Fermat primality test is based on:
OPTIONS:
A) Euler's Totient Function
B) Fermat's Little Theorem
C) The Sieve of Eratosthenes
D) The Chinese Remainder Theorem
??
SOLUTION:
B) Fermat's Little Theorem
<!--SR:!2025-02-17,4,270-->

#flashcards/Square_Root_Test
QUESTION: In modular arithmetic, if $n$ is prime, the square roots of 1 modulo $n$ are:
OPTIONS:
A) Only 1
B) Only -1
C) 1 and -1
D) 1, -1, and other values
??
SOLUTION:
C) 1 and -1
<!--SR:!2025-02-17,4,270-->

#flashcards/Miller_Rabin_Test
QUESTION: The Miller-Rabin primality test combines which two tests?
OPTIONS:
A) Fermat test and Divisibility test
B) Fermat test and Square Root test
C) Square Root test and Divisibility test
D) Euler's test and Fermat test
??
SOLUTION:
B) Fermat test and Square Root test
<!--SR:!2025-02-17,4,270-->

#flashcards/Miller_Rabin_Test
QUESTION:  In the Miller-Rabin test, $n-1$ is written in the form:
OPTIONS:
A) $m \times 2^k$ where *m* is odd
B) $m \times k^2$
C) $2m + k$
D) $m^2 + k$
??
SOLUTION:
A) $m \times 2^k$ where *m* is odd
<!--SR:!2025-02-17,4,270-->

#flashcards/Fundamental_Theorem_of_Arithmetic

QUESTION:  The Fundamental Theorem of Arithmetic states that every integer greater than 1 can be represented uniquely as:
OPTIONS:
    A) A sum of prime numbers.
    B) A product of prime numbers raised to certain powers.
    C) A difference of prime numbers.
	D) A sum of distinct primes.
??
SOLUTION:
B) A product of prime numbers raised to certain powers.
<!--SR:!2025-02-17,4,270-->

#flashcards/Euler_Phi_Function_Properties
QUESTION: If *m* and *n* are relatively prime, then $\phi(m \times n)$ is equal to:
OPTIONS:
A) $\phi(m) + \phi(n)$
B) $\phi(m) \times \phi(n)$
C) $\phi(m) - \phi(n)$
D) $\phi(m) / \phi(n)$
??
SOLUTION:
B) $\phi(m) \times \phi(n)$
<!--SR:!2025-02-17,4,270-->

#flashcards/Euler_Phi_Function_Properties
QUESTION:  For $n > 2$, the value of $\phi(n)$ is always:
OPTIONS:
A) Odd
B) Even
C) Prime
D) A power of 2
??
SOLUTION:
B) Even
<!--SR:!2025-02-17,4,270-->

#flashcards/Euler_Phi_Function_Calculation
QUESTION: What is the value of $\phi(100)$ ?
OPTIONS:
A) 20
B) 40
C) 50
D) 99
??
SOLUTION:
B) 40.
$100 = 2^2 * 5^2$.
$\phi(100) = \phi(2^2) * \phi(5^2) = (2^2 - 2^1) * (5^2 - 5^1) = (4-2) * (25-5) = 2 * 20 = 40$.
<!--SR:!2025-02-17,4,270-->

#flashcards/Fermats_Little_Theorem_Application
QUESTION:  What is the multiplicative inverse of 7 modulo 11?
OPTIONS:
A) 3
B) 5
C) 8
D) 10
??
SOLUTION:
C) 8. Using Fermat's Little Theorem, $7^{-1} \pmod{11} \equiv 7^{11-2} \pmod{11} \equiv 7^9 \pmod{11}$.
$7^2 \equiv 49 \equiv 5 \pmod{11}$
$7^4 \equiv 5^2 \equiv 25 \equiv 3 \pmod{11}$
$7^8 \equiv 3^2 \equiv 9 \pmod{11}$
$7^9 \equiv 7^8 * 7 \equiv 9 * 7 \equiv 63 \equiv 8 \pmod{11}$.
<!--SR:!2025-02-17,4,270-->

#flashcards/Eulers_Theorem_Application
QUESTION: Find $3^{24} \pmod{35}$.
OPTIONS:
A) 1
B) 3
C) 24
D) 34
??
SOLUTION:
A) 1. $\phi(35) = \phi(5) * \phi(7) = 4 * 6 = 24$. Since 3 and 35 are relatively prime, $3^{24} \equiv 3^{\phi(35)} \equiv 1 \pmod{35}$.
<!--SR:!2025-02-17,4,270-->

#flashcards/Eulers_Theorem_Multiplicative_Inverse
QUESTION:  Using Euler's theorem, if *n* and *a* are coprime, the multiplicative inverse of  `a` mod `n` is:
OPTIONS:
    A)  $a^{\phi(n)} \pmod n$
    B)  $a^{\phi(n)-1} \pmod n$
    C)  $a^{n-1} \pmod n$
    D)  $a \pmod n$
??
SOLUTION:
B) $a^{\phi(n)-1} \pmod n$
<!--SR:!2025-02-17,4,270-->

#flashcards/Checking_for_Primeness_Computational_Cost
QUESTION: What makes the naive divisibility algorithm for checking primeness inefficient for very large numbers?
OPTIONS:
	A) It needs too much memory
	B) Its time complexity is exponential
	C) It can only check even numbers
	D) It is very difficult to implement
??
SOLUTION:
B) Its time complexity is exponential
<!--SR:!2025-02-17,4,270-->

#flashcards/Primality_Testing_AKS_vs_Divisibility
QUESTION: How does the time complexity of the AKS primality test compare to the divisibility test?
OPTIONS:
A) AKS is also exponential, but with a smaller base.
B) AKS is polynomial, while divisibility is exponential.
C) AKS is logarithmic, while divisibility is linear.
D) They have the same time complexity.
??
SOLUTION:
B) AKS is polynomial, while divisibility is exponential.
<!--SR:!2025-02-17,4,270-->

#flashcards/Probabilistic_Algorithms_Error_Reduction
QUESTION: How can the probability of error in a probabilistic primality test be reduced?
OPTIONS:
A) By running the algorithm only once.
B) By running the algorithm multiple times with different parameters.
C) By using a larger input number.
D) By using only even numbers as bases.
??
SOLUTION:
B) By running the algorithm multiple times with different parameters.
<!--SR:!2025-02-17,4,270-->

#flashcards/Square_Root_Test_Composite
QUESTION: If *n* is composite, what can be said about the square roots of 1 modulo *n*?
OPTIONS:
A) They are always only +1 and -1.
B) They can be +1, -1, and possibly other values.
C) There are no square roots of 1 modulo a composite number.
D) They are always complex numbers.
??
SOLUTION:
B) They can be +1, -1, and possibly other values.
<!--SR:!2025-02-17,4,270-->

#flashcards/Miller_Rabin_Initialization
QUESTION: In the Miller-Rabin test, after choosing a base *a*, what value *T* is initially calculated?
OPTIONS:
A) $T = a^n \pmod{n}$
B) $T = a^m \pmod{n}$, where $n - 1 = m \times 2^k$
C) $T = a^{n-1} \pmod{n}$
D) $T = \sqrt{a} \pmod{n}$
??
SOLUTION:
B) $T = a^m \pmod{n}$, where $n - 1 = m \times 2^k$
<!--SR:!2025-02-17,4,270-->

#flashcards/Miller_Rabin_Stopping_Condition
QUESTION:  In the Miller-Rabin test, if at any step, $T^2 \equiv 1 \pmod{n}$ and the previous value of $T$ was *not* $\pm 1$, what is the conclusion?
OPTIONS:
A) *n* is prime.
B) *n* is composite.
C) The test is inconclusive.
D) Continue to the next step.
??
SOLUTION:
B) *n* is composite. This is because the square root test has failed.
<!--SR:!2025-02-14,1,230-->

#flashcards/Recommended_Primality_Test_Steps
QUESTION:  What is the first recommended step in the combined primality test described in the text?
OPTIONS:
A) Perform the Miller-Rabin test.
B) Choose an odd integer.
C) Choose a set of bases.
D) Calculate Euler's totient function.
??
SOLUTION:
B) Choose an odd integer.
<!--SR:!2025-02-17,4,270-->

#flashcards/GCD_and_Factorization
QUESTION:  Knowing the prime factorization of two numbers, *a* and *b*, how can their greatest common divisor (GCD) be determined?
OPTIONS:
A) By multiplying all prime factors together.
B) By taking the minimum exponent for each common prime factor and multiplying the results.
C) By taking the maximum exponent for each common prime factor and multiplying the results.
D) By adding the exponents of all prime factors.
??
SOLUTION:
B) By taking the minimum exponent for each common prime factor and multiplying the results.
<!--SR:!2025-02-17,4,270-->

#flashcards/LCM_and_Factorization
QUESTION: Knowing the prime factorization of two numbers, *a* and *b*, how can their least common multiple (LCM) be found?
OPTIONS:
A)  Take product of all distinct prime factors of *a* and *b*
B)  By taking the minimum exponent for each prime factor present in either *a* or *b*
C)  By taking the maximum exponent for each prime factor present in either *a* or *b*
D) Take product of all prime factors of *a* and *b*
??
SOLUTION:
C) By taking the maximum exponent for each prime factor present in either *a* or *b*.
<!--SR:!2025-02-17,4,270-->

#flashcards/Number_Theory_and_Cryptography
QUESTION: Why is the study of prime numbers and related concepts important in cryptography?
OPTIONS:
	A) It is only important for symmetric key cryptography.
	B) It forms the foundation for many asymmetric-key cryptosystems.
	C) It helps in creating faster hashing algorithms.
	D) It is not relevant to modern cryptography.
??
SOLUTION:
B) It forms the foundation for many asymmetric-key cryptosystems.
<!--SR:!2025-02-17,4,270-->

#flashcards/Euler_Phi_Function_Prime_Power
QUESTION: What is the general formula for calculating $\phi(p^k)$ where p is a prime and k is a positive integer?
OPTIONS:
A) $p^k$
B) $p^k - 1$
C)  $p^k - p^{k-1}$
D) $k(p-1)$
??
SOLUTION:
C) $p^k - p^{k-1}$
<!--SR:!2025-02-17,4,270-->

#flashcards/Miller-Rabin_Probability
QUESTION: What is the maximum probability that a *composite* number will pass a *single* iteration of the Miller-Rabin test with a randomly chosen base?
OPTIONS:
A) 1/2
B) 1/4
C) 1/8
D) 1/16
??
SOLUTION:
B) 1/4
<!--SR:!2025-02-17,4,270-->

#flashcards/Primality_Test_Selection
QUESTION:  Why might one choose to use a probabilistic primality test over a deterministic one, despite the chance of error?
OPTIONS:
A) Probabilistic tests are always more accurate.
B) Probabilistic tests are generally much faster for large numbers.
C) Deterministic tests are not available for large numbers.
D) Probabilistic tests require less memory.
??
SOLUTION:
B) Probabilistic tests are generally much faster for large numbers.
<!--SR:!2025-02-17,4,270-->

#flashcards/Number_of_Primes_Estimate
QUESTION: Using the approximation for $\pi(n)$, estimate the *range* for the number of primes less than 100.
OPTIONS:
    A) 10 to 50
    B) 20 to 30
	C) 21 to 45
    D) 5 to 10
??
SOLUTION:
B) 20 to 30
Lower Bound: $100 / ln(100)  \approx 100/4.605 \approx 21.7$
Upper Bound: $100/(ln(100) - 1.08366) \approx 100/(4.605 - 1.08366) \approx 100/3.52 \approx 28.4$
The range is approximately 21.7 to 28.4. The option closest to this calculated range is 20 to 30
<!--SR:!2025-02-17,4,270-->

#flashcards/Coprimes_and_Phi_Function
QUESTION:  If gcd(a,n) = 1, we say a and n are coprime, which of the following also defines the coprimality of a and n?
OPTIONS:
A) a and n have common prime factors.
B) n divides a
C) Euler's totient applies to a and n
D) a divides n
??
SOLUTION:
C) Euler's totient applies to a and n. The premise of Euler's theorem is the coprimality of the two integers involved.
<!--SR:!2025-02-17,4,270-->

#flashcards/Fermat_Number_Composites
QUESTION: Have any Fermat numbers greater than $F_4$ been proven to be prime?
OPTIONS:
A) Yes, many.
B) Yes, a few.
C) No.
D) It is still an open question.
??
SOLUTION:
C) No.
<!--SR:!2025-02-17,4,270-->

#flashcards/Divisibility_Test_Optimization
QUESTION: In the divisibility test for primality, what optimization can be made beyond checking only odd numbers?
OPTIONS:
A) Only check numbers that are multiples of 3.
B) Only check numbers that are perfect squares.
C) Only check divisibility by known prime numbers less than or equal to the square root of the number.
D) There are no further optimizations.
??
SOLUTION:
C) Only check divisibility by known prime numbers less than or equal to the square root of the number.
<!--SR:!2025-02-17,4,270-->

#flashcards/AKS_Algorithm_Significance
QUESTION:  What was the significant breakthrough achieved by the AKS algorithm?
OPTIONS:
A) It provided the first probabilistic primality test.
B) It provided a deterministic primality test with polynomial time complexity.
C) It proved that there are infinitely many Mersenne primes.
D) It provided a faster way to calculate Euler's totient function.
??
SOLUTION:
B) It provided a deterministic primality test with polynomial time complexity.
<!--SR:!2025-02-17,4,270-->

#flashcards/Miller_Rabin_Base
QUESTION: In the Miller-Rabin primality test, what does 'a' represent?
Options:
   A) Number to be tested
   B) Modulus
   C) Base
   D) An exponent
??
Solution:
C) Base
<!--SR:!2025-02-17,4,270-->

#flashcards/Factorization_Importance
QUESTION: Factorization is crucial for the security of which type of cryptosystems?
OPTIONS:
A) Symmetric-key cryptosystems
B) Public-key cryptosystems
C) Hash functions
D) Block ciphers
??
SOLUTION:
B) Public-key cryptosystems
<!--SR:!2025-02-17,4,270-->

#flashcards/Fermat_Pseudoprime
QUESTION: A composite number that passes the Fermat primality test for a specific base is called a:
OPTIONS:
A) Strong prime
B) Weak prime
C) Pseudoprime (to that base)
D) Fermat prime
??
SOLUTION:
C) Pseudoprime (to that base)
<!--SR:!2025-02-17,4,270-->

#flashcards/Euler_Theorem_Generalization
QUESTION: Euler's theorem is a generalization of which theorem?
OPTIONS:
A) Chinese Remainder Theorem
B) Fermat's Little Theorem
C) Wilson's Theorem
D) Pythagorean Theorem
??
SOLUTION:
B) Fermat's Little Theorem
<!--SR:!2025-02-17,4,270-->

#flashcards/Sieve_Limit
QUESTION: To find all primes less than 1000 using the Sieve of Eratosthenes, you would need to check for divisibility by primes up to approximately:
OPTIONS:
	A) $\sqrt{1000}$
	B) 500
	C) 100
	D) 1000
??
SOLUTION:
	A) $\sqrt{1000}$
<!--SR:!2025-02-17,4,270-->

#flashcards/Miller_Rabin_Composite_Declaration

QUESTION:
In the Miller-Rabin test, if the number is declared composite, is it possible for it to actually be prime?
OPTIONS:

    A) Yes
    B) No
    C) Only if the base is 2
    D) Only if the base is odd
??
SOLUTION:
B) No
	