# DSA-PROJECT-
#include <stdio.h>

// Initialize the ATM machine with empty notes
int atm_notes[6] = {0}; // Index 0: 10 rupees, Index 1: 20 rupees, and so on

void deposit(int amount, int denomination) {
    // Add the deposited amount to the specified denomination
    atm_notes[denomination / 10 - 1] += amount;
}

void withdraw(int amount) {
    // Initialize an array to store the used denominations
    int used_denominations[6] = {0};

    // Iterate over denominations in descending order
    for (int i = 5; i >= 0; i--) {
        while (amount >= (i + 1) * 10 && atm_notes[i] > 0) {
            // Use the denomination to withdraw the amount
            amount -= (i + 1) * 10;
            atm_notes[i]--;
            used_denominations[i]++;
        }
    }

    if (amount == 0) {
        // Successful withdrawal
        printf("Withdrawal successful. Used denominations:\n");
        for (int i = 0; i < 6; i++) {
            if (used_denominations[i] > 0) {
                printf("%d rupees: %d notes\n", (i + 1) * 10, used_denominations[i]);
            }
        }
    } else {
        // Insufficient funds
        printf("Insufficient funds in the ATM.\n");
    }
}

int main() {
    // Example usage
    deposit(5000, 10);
    deposit(5000, 20);
    deposit(5000, 50);
    deposit(5000, 100);
    deposit(5000, 200);
    deposit(5000, 500);

    withdraw(300); // Should use 100 and 200 rupee notes
    withdraw(700); // Should use 500, 100, and 100 rupee notes
    withdraw(1000); // Should use 500, 200, and 100 rupee notes
    withdraw(1500); // Should use 500, 500, and 500 rupee notes
    withdraw(2000); // Should use 200, 200, and 200 rupee notes
    withdraw(2500); // Insufficient funds

    return 0;
}
