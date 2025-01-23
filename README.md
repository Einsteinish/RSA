# How Prime Numbers Are Used in RSA
---
Here’s a step-by-step explanation of RSA encryption for $\( p = 3 \), \( q = 11 \)$, and the message $\( M = 5 \)$:

### **Step 1: Choose Two Prime Numbers**

We choose two primes:  

$p = 3 \quad \text{and} \quad q = 11$

### **Step 2: Calculate $n$ (the modulus)**  

$n = p \times q = 3 \times 11 = 33$

This $\( n \)$ will be part of both the public and private keys.

### **Step 3: Calculate $\( \phi(n) \)$ (Euler’s Totient Function)**  

$\phi(n) = (p - 1) \times (q - 1)$

$\phi(n) = (3 - 1) \times (11 - 1) = 2 \times 10 = 20$

### **Step 4: Choose the Public Exponent $\( e \)$**  
Choose an $\( e \)$ such that:
1. $\( 1 < e < \phi(n) \)$  
2. $\( \text{gcd}(e, \phi(n)) = 1 \)$ (relatively prime to $\( \phi(n) \))$  

Let’s select $\( e = 3 \)$, which satisfies these conditions.

### **Step 5: Calculate the Private Key $\( d \)$**  
The private key $\( d \)$ is the modular multiplicative inverse of $\( e \)$ modulo $\( \phi(n) \)$, meaning:  
 
$e \times d \equiv 1 \ (\text{mod} \ \phi(n))$
 

To find $\( d \)$, solve:

$3 \times d \equiv 1 \ (\text{mod} \ 20)$
 

Using the Extended Euclidean Algorithm:
 
$d = 7$
 
Now we have:  
- **Public Key**: $\( (e, n) = (3, 33) \)$
- **Private Key**: $\( (d, n) = (7, 33) \)$

### **Step 6: Encrypt the Message $\( M = 5 \)$**  
The encryption formula is:
 
$C = M^e \ (\text{mod} \ n)$
 
Substitute $\( M = 5 \)$, $\( e = 3 \)$, and $\( n = 33 \)$:

$C = 5^3 \ (\text{mod} \ 33)$

1. Calculate $\( 5^3 \)$:  $5^3 = 5 \times 5 \times 5 = 125$
 
2. Reduce modulo $\( 33 \)$:  $C = 125 \ (\text{mod} \ 33) = 125 - 3 \times 33 = 125 - 99 = 26$

So, the encrypted message is:
 
$C = 26$   

### **Step 7: Decrypt the Ciphertext $\( C = 26 \)$**  
The decryption formula is:

$M = C^d \ (\text{mod} \ n)$

Substitute $\( C = 26 \)$, $\( d = 7 \)$, and $\( n = 33 \)$:
 
$M = 26^7 \ (\text{mod} \ 33)$


Instead of directly calculating $\( 26^7 \)$, use modular exponentiation for efficiency:
1. $\( 26^2 \ (\text{mod} \ 33) = 26 \times 26 = 676 \ (\text{mod} \ 33) = 16 \)$
2. $\( 26^4 \ (\text{mod} \ 33) = 16 \times 16 = 256 \ (\text{mod} \ 33) = 25 \)$
3. $\( 26^7 \ (\text{mod} \ 33) = 26^4 \times 26^2 \times 26 \ (\text{mod} \ 33) = 25 \times 16 \times 26 \ (\text{mod} \ 33) \)$
   - $\( 25 \times 16 = 400 \ (\text{mod} \ 33) = 4 \)$
   - $\( 4 \times 26 = 104 \ (\text{mod} \ 33) = 5 \)$

Thus, the decrypted message is:

$M = 5$

### **Final Result**
- **Original Message**: $\( M = 5 \)$  
- **Encrypted Message**: $\( C = 26 \)$  
- **Decrypted Message**: $\( M = 5 \)$

This demonstrates how RSA ensures secure encryption and decryption using prime numbers. 
