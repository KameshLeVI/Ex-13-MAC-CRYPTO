# Ex-13-MAC-CRYPTO
## AIM:

To generate and verify a Message Authentication Code (MAC) for ensuring the integrity and authenticity of a message using a simple XOR operation.

## ALGORITHM:

### Step 1:

Input a secret key and a message from the user.

### Step 2:

Generate the MAC by applying a simple XOR operation between the secret key and the message.

### Step 3:

The MAC is computed by repeating the key or message as necessary.

### Step 4:

The user can input a received MAC, and the program verifies whether the received MAC matches the computed MAC.

### Step 5:

The authenticity of the message is confirmed if the MACs match.

## PROGRAM:

```c
#include <stdio.h>
#include <string.h>

#define MAC_SIZE 32

void computeMAC(const char *key, const char *message, char *mac) {
    int key_len = strlen(key);
    int msg_len = strlen(message);

    for (int i = 0; i < MAC_SIZE; i++) {
        mac[i] = key[i % key_len] ^ message[i % msg_len]; 
    }
    mac[MAC_SIZE] = '\0'; 
}

int main() {
    char key[100], message[100];
    char mac[MAC_SIZE + 1]; 
    char receivedMAC[MAC_SIZE + 1]; 

    printf("Enter the secret key: ");
    scanf("%s", key);

    printf("Enter the message: ");
    scanf("%s", message);

    computeMAC(key, message, mac);

    printf("Computed MAC (in hex): ");
    for (int i = 0; i < MAC_SIZE; i++) {
        printf("%02x", (unsigned char)mac[i]); // Print each byte as hex
    }
    printf("\n");

    printf("Enter the received MAC (as hex): ");
    for (int i = 0; i < MAC_SIZE; i++) {
        scanf("%02hhx", &receivedMAC[i]);
    }

    if (memcmp(mac, receivedMAC, MAC_SIZE) == 0) {
        printf("MAC verification successful. Message is authentic.\n");
    } else {
        printf("MAC verification failed. Message is not authentic.\n");
    }

    return 0;
}
```

## OUTPUT:
![image](https://github.com/user-attachments/assets/86f71cd3-7f17-41e4-ad4c-42b6ee01eae8)


## RESULT:

The program for generating and verifying a Message Authentication Code (MAC) was executed successfully, demonstrating the integrity and authenticity of the message through a simple XOR-based MAC.
