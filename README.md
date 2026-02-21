# online-voting-system
#include <stdio.h>

int main() {
    int choice, vote1 = 0, vote2 = 0, vote3 = 0;
    char ch;

    do {
        printf("\n--- Online Voting System ---\n");
        printf("1. Candidate A\n");
        printf("2. Candidate B\n");
        printf("3. Candidate C\n");
        printf("Enter your vote (1-3): ");
        scanf("%d", &choice);

        switch(choice) {
            case 1: vote1++; break;
            case 2: vote2++; break;
            case 3: vote3++; break;
            default: printf("Invalid Vote!\n");
        }

        printf("Another voter? (y/n): ");
        scanf(" %c", &ch);

    } while(ch == 'y');

    printf("\n--- Voting Result ---\n");
    printf("Candidate A: %d votes\n", vote1);
    printf("Candidate B: %d votes\n", vote2);
    printf("Candidate C: %d votes\n", vote3);

    if(vote1 > vote2 && vote1 > vote3)
        printf("Winner: Candidate A\n");
    else if(vote2 > vote1 && vote2 > vote3)
        printf("Winner: Candidate B\n");
    else if(vote3 > vote1 && vote3 > vote2)
        printf("Winner: Candidate C\n");
    else
        printf("It's a Tie!\n");

    return 0;
}
