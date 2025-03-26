# Caeser Cipher
Caeser Cipher using with different key values



# Reg no : 212223043001
# Name :   GOPIKRISHNAN M

# AIM:

To encrypt and decrypt the given message by using Ceaser Cipher encryption algorithm.

## DESIGN STEPS:
Step 1: Design of Caeser Cipher algorithnm

Step 2: Implementation using C or pyhton code

Step 3: In Ceaser Cipher each letter in the plaintext is replaced by a letter some fixed number of positions down the alphabet.
For example, with a left shift of 3, D would be replaced by A, E would become B, and so on.
The encryption can also be represented using modular arithmetic by first transforming the letters into numbers, according to the
scheme, A = 0, B = 1, Z = 25.
Encryption of a letter x by a shift n can be described mathematically as, En(x) = (x + n) mod26
Decryption is performed similarly, Dn (x)=(x - n) mod26

## PROGRAM:
```
#include <stdio.h>
#include <string.h>
#include <ctype.h> 
int keymat[3][3] = {
    { 1, 2, 1 },
    { 2, 3, 2 },
    { 2, 2, 1 }
};

int invkeymat[3][3] = {
    { -1, 0, 1 },
    { 2, -1, 0 },
    { -2, 2, -1 }
};

char key[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";


char* encode(char a, char b, char c) {
    static char ret[4]; 
    int x, y, z;
    int posa = (int) a - 65;
    int posb = (int) b - 65;
    int posc = (int) c - 65;
    
    x = posa * keymat[0][0] + posb * keymat[1][0] + posc * keymat[2][0];
    y = posa * keymat[0][1] + posb * keymat[1][1] + posc * keymat[2][1];
    z = posa * keymat[0][2] + posb * keymat[1][2] + posc * keymat[2][2];
    
    ret[0] = key[x % 26];
    ret[1] = key[y % 26];
    ret[2] = key[z % 26];
    ret[3] = '\0';  
    
    return ret;
}


char* decode(char a, char b, char c) {
    static char ret[4];  
    int x, y, z;
    int posa = (int) a - 65;
    int posb = (int) b - 65;
    int posc = (int) c - 65;
    
    x = posa * invkeymat[0][0] + posb * invkeymat[1][0] + posc * invkeymat[2][0];
    y = posa * invkeymat[0][1] + posb * invkeymat[1][1] + posc * invkeymat[2][1];
    z = posa * invkeymat[0][2] + posb * invkeymat[1][2] + posc * invkeymat[2][2];
    
    ret[0] = key[(x % 26 < 0) ? (26 + x % 26) : (x % 26)];
    ret[1] = key[(y % 26 < 0) ? (26 + y % 26) : (y % 26)];
    ret[2] = key[(z % 26 < 0) ? (26 + z % 26) : (z % 26)];
    ret[3] = '\0'; 
    
    return ret;
}

int main() {
    char msg[1000];
    char enc[1000] = "";  
    char dec[1000] = "";  
    int n;

    
    printf(" ");
    fgets(msg, sizeof(msg), stdin);
    msg[strcspn(msg, "\n")] = '\0'; 

    printf("Simulation of Hill Cipher\n");
    printf("Input message : %s\n", msg);

    // Convert the message to uppercase
    for (int i = 0; i < strlen(msg); i++) {
        msg[i] = toupper(msg[i]);
    }

    // Remove spaces and padding
    n = strlen(msg) % 3;
    if (n != 0) {
        for (int i = 1; i <= (3 - n); i++) {
            strcat(msg, "X");
        }
    }

    printf("Padded message : %s\n", msg);

    // Encode the message in blocks of 3 characters
    for (int i = 0; i < strlen(msg); i += 3) {
        char a = msg[i];
        char b = msg[i + 1];
        char c = msg[i + 2];
        strcat(enc, encode(a, b, c));
    }

    printf("Encoded message : %s\n", enc);

    // Decode the message in blocks of 3 characters
    for (int i = 0; i < strlen(enc); i += 3) {
        char a = enc[i];
        char b = enc[i + 1];
        char c = enc[i + 2];
        strcat(dec, decode(a, b, c));
    }

    printf("Decoded message : %s\n", dec);

    return 0;
}

```




## OUTPUT:

![Screenshot (78)](https://github.com/user-attachments/assets/6e6afbb0-1705-4d99-a3f7-65d3a1d124c2)



## RESULT:
The program is executed successfully
