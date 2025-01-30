# How Prime Numbers Are Used in RSA

Prime numbers are used in RSA (Rivest–Shamir–Adleman) encryption, a cornerstone of the Public Key Infrastructure (PKI) system, because they enable the creation of a large modulus ($n = p \times q$) that is computationally infeasible to factor into its prime components. This underpins the security of PKI by ensuring that public and private key pairs remain secure for encrypting, decrypting, and authenticating sensitive data.

Here’s a step-by-step explanation of RSA encryption for $\( p = 3 \), \( q = 11 \)$, and the message $\( M = 5 \)$:

### Step 1: Choose Two Prime Numbers

We choose two primes:  

$p = 3 \quad \text{and} \quad q = 11$

### Step 2: Calculate $n$ (the modulus) 

$n = p \times q = 3 \times 11 = 33$

This $n$ will be part of both the public and private keys.

### Step 3: Calculate $\phi(n)$ (Euler’s Totient Function)

$\phi(n) = (p - 1) \times (q - 1)$

$\phi(n) = (3 - 1) \times (11 - 1) = 2 \times 10 = 20$

### Step 4: Choose the Public Exponent $e$ which must be relatively prime to $\phi(n)$  

Choose an $e$ such that:
1. $1 < e < \phi(n)$  
2. $\text{gcd}(e, \phi(n)) = 1$ (relatively prime to $\phi(n)$, meaning $e$ and $\phi(n)$ have no common factors other than $1$).

We need to find a value for $e$ that satisfies:
1. $1 < e < 20$  
2. $\text{gcd}(e, 20) = 1$

Start testing small integers for $e$:
- $e =  2$:
  
   $gcd(2,20)=2$ (not relatively prime, so not valid).
  
- $e =  3$:
  
   $gcd(3,20)=1$ (relatively prime, so valid).

Let’s select $e = 3$, which satisfies these conditions.  

The public key would be represented as a pair:

$$(e,n) = (3,33)$$  

(Note) Two numbers are relatively prime (also called coprime) if they share no common factors other than 1. 
This means their greatest common divisor (GCD) is 1.  

### Step 5: Calculate the Private Key $d$  
The private key $d$ is the modular multiplicative inverse of $e$ modulo $\phi(n)$, meaning:  
 
$$e \times d \equiv 1 \ (\text{mod} \ \phi(n))$$
 

To find $d$, solve:

$$3 \times d \equiv 1 \ (\text{mod} \ 20)$$
 

Using the Extended Euclidean Algorithm:
 
$$d = 7$$
 
Now we have:  
- **Public Key**: $(e, n) = (3, 33)$
- **Private Key**: $(d, n) = (7, 33)$

### Step 6: Encrypt the Message $M = 5$  
The encryption formula is:
 
$$C = M^e \ (\text{mod} \ n)$$
 
Substitute $M = 5$, $e = 3$, and $n = 33$:

$$C = 5^3 \ (\text{mod} \ 33)$$

1. Calculate $5^3$:

   $$5^3 = 5 \times 5 \times 5 = 125$$

2. Reduce modulo $33$:  
   
   $$C = 125 \ (\text{mod} \ 33) = 125 - 3 \times 33 = 125 - 99 = 26$$
   

So, the encrypted message is:
 
   $$C = 26$$   

### Step 7: Decrypt the Ciphertext $C = 26$ 
The decryption formula is:

$$M = C^d \ (\text{mod} \ n)$$

Substitute $C = 26$, $d = 7$, and $n = 33$:
 
$$M = 26^7 \ (\text{mod} \ 33)$$


Instead of directly calculating $26^7$, use modular exponentiation for efficiency:
1. $26^2 \ (\text{mod} \ 33) = 26 \times 26 = 676 \ (\text{mod} \ 33) = 16$
2. $26^4 \ (\text{mod} \ 33) = 16 \times 16 = 256 \ (\text{mod} \ 33) = 25$
3. $26^7 \ (\text{mod} \ 33) = 26^4 \times 26^2 \times 26 \ (\text{mod} \ 33) = 25 \times 16 \times 26 \ (\text{mod} \ 33)$
   - $25 \times 16 = 400 \ (\text{mod} \ 33) = 4$
   - $4 \times 26 = 104 \ (\text{mod} \ 33) = 5$

Thus, the decrypted message is:

$$M = 5$$

### Final Result
- **Original Message**: $M = 5$  
- **Encrypted Message**: $C = 26$  
- **Decrypted Message**: $M = 5$

This demonstrates how RSA ensures secure encryption and decryption using prime numbers. 

---

## How This Works in PKI  

### **Key Distribution:**
You publish your **public key** $(e,n) = (3, 33)$ so that anyone can send you encrypted messages. When sending a public key in RSA, you typically send the two numbers 
$e$ (the public exponent) and $n$ (the modulus), so the public key would be represented as a pair $(e,n)$:

$$(e,n) = (3,33)$$

Your **private key** $(d, n) = (7, 33)$ is kept secret.  
**(Note 1)**  
However, the numbers $e=3$ and $n=33$ are very small and not secure for real-world RSA encryption. These numbers are simply for illustration, and actual RSA keys used for secure communication have much larger values (typically hundreds of bits long for both $e$ and $n$).
In practice, $n$ is usually the product of two large prime numbers $p$ and $q$, and $e$ is a smaller number, often $65537$, but it can be any number that is coprime with $(p - 1)(q - 1)$.  
**(Note 2: More realistic example)**  
$e=65537$ (common choice for the public exponent)  
$n=3233$ (product of two prime numbers, 61 and 53, for example)  
So, the **public key** would be something like:

$$(e,n) = (65537,3233)$$


### **Secure Communication:**
A sender **encrypts** $M=5$ using your **public key**, producing ciphertext 
$C=26$.  
Only **you** can **decrypt** it using your **private key**, recovering $M=5$.    
  
### **Digital Signatures (Authentication):**
You can **sign** messages using your **private key**, and anyone can **verify** the signature with your **public key**.  

