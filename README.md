# RSA-Encryption-Algorithm:
## Aim:
To Implement RSA Encryption Algorithm in C Program
## Algorithm:
1.Select Primes: Choose two large prime numbers, p and q

2.Compute n and φ(n): Calculate n=p×q and ϕ(n)=(p−1)×(q−1).

3.Select e: Choose an integer e such that 1<e<ϕ(n) and gcd(e, φ(n)) = 1.

4.Compute d: Calculate d such that d≡e−1 mod ϕ(n).

5.Encrypt: Compute ciphertext c ≡ me mod n for a message m.

6.Decrypt: Recover the message using m ≡ cd mod n.
## Program:
```
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <time.h>

int gcd(int a, int b) {
    while (b != 0) {
        int t = b;
        b = a % b;
        a = t;
    }
    return a;
}

int modInverse(int a, int m) {
    a = a % m;
    for (int x = 1; x < m; x++) {
        if ((a * x) % m == 1)
            return x;
    }
    return -1;
}

int modExp(int base, int exp, int mod) {
    int result = 1;
    while (exp > 0) {
        if (exp % 2 == 1)
            result = (result * base) % mod;
        exp = exp >> 1;
        base = (base * base) % mod;
    }
    return result;
}

int generatePrime() {
    int primes[] = {61, 53, 47, 41, 37, 31, 29, 23, 19, 17, 13};
    int index = rand() % (sizeof(primes) / sizeof(primes[0]));
    return primes[index];
}

void generateKeys(int *e, int *d, int *n) {
    int p = generatePrime();
    int q = generatePrime();
    while (q == p) {
        q = generatePrime();
    }

    *n = p * q;
    int phi = (p - 1) * (q - 1);

    *e = 17;
    while (gcd(*e, phi) != 1) {
        (*e)++;
    }

    *d = modInverse(*e, phi);
}

int encrypt(int message, int e, int n) {
    return modExp(message, e, n);
}

int decrypt(int ciphertext, int d, int n) {
    return modExp(ciphertext, d, n);
}

int main() {
    srand(time(NULL)); // Initialize random seed

    int e, d, n;
    generateKeys(&e, &d, &n);

    printf("Generated Keys: \n");
    printf("Public Key: (%d, %d)\n", e, n);
    printf("Private Key: (%d, %d)\n", d, n);

    int message = 65; // Example message (A)
    int encrypted = encrypt(message, e, n);
    int decrypted = decrypt(encrypted, d, n);

    printf("Message: %d\n", message);
    printf("Encrypted: %d\n", encrypted);
    printf("Decrypted: %d\n", decrypted);

    return 0;
}
```
## Output:

![rsa](https://github.com/user-attachments/assets/9fb51efe-e94d-4b89-8bb0-456d6edbdc38)

## Result:
Thus to implement the RSA encryption algorithm in C is executed successfully.
