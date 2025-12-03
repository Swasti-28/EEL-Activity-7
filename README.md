# EEL-Activity-7
#include <stdio.h>

int main() {
    FILE *fp;
    char quote[200];
    int choice;

    while (1) {
        printf("\n--- Motivational Quote Saver ---\n");
        printf("1. Write a new quote (overwrite file)\n");
        printf("2. Display all quotes\n");
        printf("3. Exit\n");
        printf("Enter choice: ");
        scanf("%d", &choice);

        if (choice == 1) {
            fp = fopen("quotes.txt", "w"); // overwrite file
            if (fp == NULL) {
                printf("Error opening file!\n");
                return 1;
            }

            printf("Enter your quote: ");
            scanf(" %199[^\n]", quote);   // read full line without fgets
            fprintf(fp, "%s\n", quote);   // write with newline

            fclose(fp);
            printf("Quote written to file.\n");
        }

        else if (choice == 2) {
            fp = fopen("quotes.txt", "r");
            if (fp == NULL) {
                printf("No file found or no quotes saved yet.\n");
                continue;
            }

            printf("\n--- Saved Quotes ---\n");
            while (fscanf(fp, " %199[^\n]", quote) == 1) {
                printf("%s\n", quote);
            }

            fclose(fp);
        }

        else if (choice == 3) {
            printf("Exiting program...\n");
            break;
        }

        else {
            printf("Invalid choice. Try again.\n");
        }
    }

    return 0;
}
