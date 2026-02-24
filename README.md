# online-voting-system

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX 100
struct Voter {
    int voterID;
};
int main() {
    struct Voter voters[MAX];
    int votedIDs[MAX];
    int voteCount = 0;

    int vote1 = 0, vote2 = 0, vote3 = 0;
    int totalVoters, i, j;
    int choice, id;
    int password;
    int duplicate;

    FILE *fp;

    printf("Enter total number of voters: ");
    scanf("%d", &totalVoters);

    for(i = 0; i < totalVoters; i++) {

        printf("\n--- Voter %d ---\n", i+1);

        printf("Enter Voter ID: ");
        scanf("%d", &id);

        // Check duplicate voter ID
        duplicate = 0;
        for(j = 0; j < voteCount; j++) {
            if(votedIDs[j] == id) {
                duplicate = 1;
                break;
            }
        }

        if(duplicate) {
            printf("You have already voted! Access Denied.\n");
            i--;
            continue;
        }

        votedIDs[voteCount++] = id;

        printf("1. Candidate A\n");
        printf("2. Candidate B\n");
        printf("3. Candidate C\n");
        printf("Enter your vote (1-3): ");
        scanf("%d", &choice);

        switch(choice) {
            case 1: vote1++; break;
            case 2: vote2++; break;
            case 3: vote3++; break;
            default:
                printf("Invalid vote! Try again.\n");
                voteCount--;
                i--;
        }
    }

    // Save results to file
    fp = fopen("votes.txt", "w");
    fprintf(fp, "Candidate A: %d\n", vote1);
    fprintf(fp, "Candidate B: %d\n", vote2);
    fprintf(fp, "Candidate C: %d\n", vote3);
    fclose(fp);

    printf("\nVoting Completed Successfully!\n");

    
    printf("\nEnter Admin Password to view results: ");
    scanf("%d", &password);

    if(password == 1234) {
        float total = vote1 + vote2 + vote3;

        printf("\n--- Voting Results ---\n");
        printf("Candidate A: %d votes (%.2f%%)\n", vote1, (vote1*100)/total);
        printf("Candidate B: %d votes (%.2f%%)\n", vote2, (vote2*100)/total);
        printf("Candidate C: %d votes (%.2f%%)\n", vote3, (vote3*100)/total);

        if(vote1 > vote2 && vote1 > vote3)
            printf("Winner: Candidate A\n");
        else if(vote2 > vote1 && vote2 > vote3)
            printf("Winner: Candidate B\n");
        else if(vote3 > vote1 && vote3 > vote2)
            printf("Winner: Candidate C\n");
        else
            printf("It's a Tie!\n");

    } else {
        printf("Wrong Password! Access Denied.\n");
    }

    return 0;
}
