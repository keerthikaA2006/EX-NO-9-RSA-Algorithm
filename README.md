# EX-NO-9-RSA-Algorithm

## AIM:
To Implement RSA Encryption Algorithm in Cryptography

## Algorithm:


Step 1: Design of RSA Algorithm  
The RSA algorithm is based on the mathematical difficulty of factoring the product of two large prime numbers. It involves generating a public and private key pair, where the public key is used for encryption, and the private key is used for decryption.

Step 2: Implementation in Python or C 
This algorithm can be implemented in languages like Python or C by performing large integer calculations for key generation, encryption, and decryption, utilizing libraries for modular arithmetic if necessary.

Step 3: Algorithm Description  
1. Key Generation:
   - Select two large prime numbers \( p \) and \( q \).
   - Calculate \( n = p \times q \), which will be used as the modulus.
   - Compute the totient \( \phi(n) = (p - 1)(q - 1) \).
   - Choose a public exponent \( e \) such that \( e \) is coprime with \( \phi(n) \).
   - Compute the private key \( d \), which is the modular inverse of \( e \) mod \( \phi(n) \).

2. Encryption:
   - Convert the plaintext message \( M \) into a numerical form \( m \) (such that \( 0 \le m < n \)).
   - Compute the ciphertext \( c \) using the formula: \( c = m^e \mod n \).

3. Decryption:
   - Use the private key \( d \) to recover \( m \) from \( c \) using: \( m = c^d \mod n \).
   - Convert \( m \) back into the original message \( M \).

Step 4: Mathematical Representation  
- Encryption: \( E(m) = m^e \mod n \)
- Decryption: \( D(c) = c^d \mod n \)

Step 5: **Security Foundation  
The security of RSA relies on the difficulty of factoring large numbers; thus, choosing sufficiently large prime numbers for \( p \) and \( q \) is crucial for security.

## Program:
```
#include <stdio.h> 
 
int gcd(int a, int b) { 
    while (b != 0) { 
        int temp = b; 
        b = a % b; 
        a = temp; 
    } 
    return a; 
} 
 
int modInverse(int e, int phi) { 
    int d = 1; 
    while ((d * e) % phi != 1) { 
        d++; 
    } 
    return d; 
} 
 
long long power(long long base, long long exp, long long mod) { 
    long long result = 1; 
    base = base % mod; 
    while (exp > 0) { 
        if (exp % 2 == 1) 
            result = (result * base) % mod; 
        exp = exp / 2; 
        base = (base * base) % mod; 
    } 
    return result; 
} 
 
int main() { 
    int p, q, n, phi, e, d, message; 
    long long ciphertext, decrypted; 
 
    printf ("Enter prime number p: "); 
    scanf("%d", &p); 
    prin ("Enter prime number q: "); 
    scanf("%d", &q); 
 
    n = p * q; 
    phi = (p - 1) * (q - 1); 
 
 
    printf ("Enter public key exponent e (should be coprime with %d): ", phi); 
    scanf("%d", &e); 
 
 
    if (gcd(e, phi) != 1) { 
        printf ("Error: e is not coprime with phi(n). Try again.\n"); 
        return 1; 
    } 
 
    d = modInverse(e, phi); 
 
    printf ("\nPublic Key (e, n): (%d, %d)\n", e, n); 
    printf ("Private Key (d, n): (%d, %d)\n", d, n); 
     
    printf ("\nEnter message (as integer < %d): ", n); 
    scanf("%d", &message); 
 
    ciphertext = power(message, e, n); 
    printf ("Encrypted Message: %lld\n", ciphertext); 
 
    decrypted = power(ciphertext, d, n); 
    printf ("Decrypted Message: %lld\n", decrypted); 
 
    return 0; 
} 
 

```



## Output:

<img width="626" height="452" alt="image" src="https://github.com/user-attachments/assets/2d079f80-ee66-42cf-91f4-dcdd0966f5e5" />


## Result:
 The program is executed successfully.
