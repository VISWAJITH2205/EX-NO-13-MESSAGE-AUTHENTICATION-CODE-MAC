# NAME : VISWAJITH LALITHRAM R.V

# REG.NO : 212224240187

# EX-NO-13-MESSAGE-AUTHENTICATION-CODE-MAC

## AIM:
To implement MESSAGE AUTHENTICATION CODE(MAC)

## ALGORITHM:

1. Message Authentication Code (MAC) is a cryptographic technique used to verify the integrity and authenticity of a message by using a secret key.

2. Initialization:
   - Choose a cryptographic hash function \( H \) (e.g., SHA-256) and a secret key \( K \).
   - The message \( M \) to be authenticated is input along with the secret key \( K \).

3. MAC Generation:
   - Compute the MAC by applying the hash function to the combination of the message \( M \) and the secret key \( K \): 
     \[
     \text{MAC}(M, K) = H(K || M)
     \]
     where \( || \) denotes concatenation of \( K \) and \( M \).

4. Verification:
   - The recipient, who knows the secret key \( K \), computes the MAC using the received message \( M \) and the same hash function.
   - The recipient compares the computed MAC with the received MAC. If they match, the message is authentic and unchanged.

5. Security: The security of the MAC relies on the secret key \( K \) and the strength of the hash function \( H \), ensuring that an attacker cannot forge a valid MAC without knowledge of the key.

## Program:

```



#include <stdio.h>
#include <string.h>

#define KEY "secretkey"   // Shared secret key

// Simple MAC function using XOR
unsigned int calculate_mac(const char *msg, const char *key)
{
    unsigned int mac = 0;

    // XOR all characters of the message
    for (int i = 0; msg[i] != '\0'; i++)
        mac ^= msg[i];

    // XOR all characters of the key
    for (int i = 0; key[i] != '\0'; i++)
        mac ^= key[i];

    return mac;
}

int main()
{
    char message[256];
    unsigned int mac_sent, mac_received;

    // Take input
    printf("Enter the message: ");
    fgets(message, sizeof(message), stdin);

    // Remove newline
    message[strcspn(message, "\n")] = '\0';

    // Sender side
    mac_sent = calculate_mac(message, KEY);
    printf("Generated MAC (sent): %u\n", mac_sent);

    // Receiver side
    mac_received = calculate_mac(message, KEY);
    printf("Calculated MAC (received): %u\n", mac_received);

    // Compare
    if (mac_sent == mac_received)
        printf("Message is authentic.\n");
    else
        printf("Message integrity check failed.\n");

    return 0;
}




```


## Output:


<img width="1080" height="682" alt="Screenshot 2025-11-15 082410" src="https://github.com/user-attachments/assets/86884acc-27ae-499d-81db-18b1ead345b7" />



## Result:
The program is executed successfully.
