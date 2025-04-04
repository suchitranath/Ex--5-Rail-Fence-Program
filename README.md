# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE
date: 28/03/2025

# AIM:
To write a C program to implement the rail fence transposition technique.

# ALGORITHM:
1) Read the Plain text.
2) Arrange the plain text in row columnar matrix format.
3) Now read the keyword depending on the number of columns of the plain text.
4) Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
5) Read the characters row wise or column wise in the former order to get the cipher text.

# PROGRAM
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>

// Function to encrypt using Rail Fence Cipher
void encryptRailFence(char text[], int depth, char cipher[]) {
    int len = strlen(text);
    char rail[depth][len];
    memset(rail, '\n', sizeof(rail)); // Initialize with newline characters

    int row = 0, down = 1; // Direction flag

    for (int i = 0; i < len; i++) {
        rail[row][i] = text[i]; // Place character in rail matrix

        // Change row direction
        if (row == 0)
            down = 1;
        else if (row == depth - 1)
            down = 0;

        // Move to next row
        row += (down ? 1 : -1);
    }

    // Read cipher text row-wise
    int k = 0;
    for (int i = 0; i < depth; i++)
        for (int j = 0; j < len; j++)
            if (rail[i][j] != '\n')
                cipher[k++] = rail[i][j];

    cipher[k] = '\0';
}

// Function to decrypt the Rail Fence Cipher
void decryptRailFence(char cipher[], int depth, char plain[]) {
    int len = strlen(cipher);
    char rail[depth][len];
    memset(rail, '\n', sizeof(rail));

    int row = 0, down = 1, index = 0;

    // Mark the rail positions
    for (int i = 0; i < len; i++) {
        rail[row][i] = '*';

        if (row == 0)
            down = 1;
        else if (row == depth - 1)
            down = 0;

        row += (down ? 1 : -1);
    }

    // Fill the rail with cipher text
    for (int i = 0; i < depth; i++)
        for (int j = 0; j < len; j++)
            if (rail[i][j] == '*')
                rail[i][j] = cipher[index++];

    // Read text in the original order
    row = 0, down = 1;
    for (int i = 0; i < len; i++) {
        plain[i] = rail[row][i];

        if (row == 0)
            down = 1;
        else if (row == depth - 1)
            down = 0;

        row += (down ? 1 : -1);
    }
    plain[len] = '\0';
}

// Main function
int main() {
    char text[100], cipher[100], decrypted[100];
    int depth;

    printf("Enter the plaintext: ");
    scanf("%s", text);
    printf("Enter the depth: ");
    scanf("%d", &depth);

    encryptRailFence(text, depth, cipher);
    printf("Encrypted Text: %s\n", cipher);

    decryptRailFence(cipher, depth, decrypted);
    printf("Decrypted Text: %s\n", decrypted);

    return 0;
}

```
# OUTPUT
![image](https://github.com/user-attachments/assets/b3f96851-f813-492c-88d2-9714e33d5afb)

# RESULT
implementation of the rail fence transposition technique using c program has been done successfully
