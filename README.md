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
#include <math.h>

long int p, q, n, t, e, d;
long int temp[100], m[100], en[100];
int i, j;
char msg[100];

int prime(long int);
long int cd(long int);
void encrypt();
void decrypt();

int main() {
    printf("Enter first prime number (p): ");
    scanf("%ld", &p);

    if (!prime(p)) {
        printf("p is not a prime number.\n");
        return 0;
    }

    printf("Enter second prime number (q): ");
    scanf("%ld", &q);

    if (!prime(q)) {
        printf("q is not a prime number.\n");
        return 0;
    }

    printf("Enter the message: ");
    scanf("%s", msg);

    n = p * q;
    t = (p - 1) * (q - 1);

    // Find e
    for (e = 2; e < t; e++) {
        if (t % e != 0 && prime(e))
            break;
    }

    d = cd(e);

    printf("\nPublic Key: (%ld, %ld)", e, n);
    printf("\nPrivate Key: (%ld, %ld)\n", d, n);

    encrypt();
    decrypt();

    return 0;
}

int prime(long int pr) {
    int i;
    j = sqrt(pr);
    for (i = 2; i <= j; i++) {
        if (pr % i == 0)
            return 0;
    }
    return 1;
}

long int cd(long int x) {
    long int k = 1;
    while (1) {
        k = k + t;
        if (k % x == 0)
            return (k / x);
    }
}

void encrypt() {
    long int pt, ct, key = e, k;
    i = 0;
    while (msg[i] != '\0') {
        pt = msg[i];
        pt = pt - 96;
        k = 1;
        for (j = 0; j < key; j++) {
            k = (k * pt) % n;
        }
        temp[i] = k;
        en[i] = k + 96;
        i++;
    }
    en[i] = -1;
    printf("\nEncrypted Message: ");
    for (i = 0; en[i] != -1; i++)
        printf("%c", en[i]);
}

void decrypt() {
    long int pt, ct, key = d, k;
    i = 0;
    while (en[i] != -1) {
        ct = temp[i];
        k = 1;
        for (j = 0; j < key; j++) {
            k = (k * ct) % n;
        }
        m[i] = k + 96;
        i++;
    }
    m[i] = -1;
    printf("\nDecrypted Message: ");
    for (i = 0; m[i] != -1; i++)
        printf("%c", m[i]);
    printf("\n");
}
```

## Output:
<img width="1628" height="893" alt="Screenshot 2025-10-24 091316" src="https://github.com/user-attachments/assets/8f8edae3-2b84-4581-86d1-451687f3721b" />


## Result:
 The program is executed successfully.
