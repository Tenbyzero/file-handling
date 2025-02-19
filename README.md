 // Structure program to store student details choice to write or read
#include <stdio.h>

typedef struct student
{
    char name[20];
    int age;
    char bloodGroup[10];
    char dob[12];
} s;

void writeData();
void readData();

int main()
{
    int choice;
    printf("Enter 1 to write data or 2 to read data: ");
    scanf("%d", &choice);
    getchar(); // Consume the newline character left by scanf

    switch (choice)
    {
        case 1:
            writeData();
            break;
        case 2:
            readData();
            break;
        default:
            printf("Invalid choice\n");
            break;
    }

    return 0;
}

void writeData()
{
    FILE *f;
    f = fopen("temp.txt", "w");
    if (f == NULL)
    {
        perror("Error ");
    }
    else
    {
        int n;
        s zzz[10];
        printf("\nEnter the no of student you need to process : ");
        scanf("%d", &n);
        getchar(); // Consume the newline character left by scanf
        printf("\nEnter %d student details : \n", n);

        for (int i = 0; i < n; i++)
        {
            printf("\nEnter the name student [%d] : ", i + 1);
            fgets(zzz[i].name, sizeof(zzz[i].name), stdin);
            printf("Enter the age student [%d] : ", i + 1);
            scanf("%d", &zzz[i].age);
            getchar(); // Consume the newline character left by scanf
            printf("Enter the Blood group student [%d] : ", i + 1);
            fgets(zzz[i].bloodGroup, sizeof(zzz[i].bloodGroup), stdin);
            printf("Enter the date of birth student [%d] : ", i + 1);
            fgets(zzz[i].dob, sizeof(zzz[i].dob), stdin);
        }

        for (int i = 0; i < n; i++)
        {
            fprintf(f, "%d. Student details \n", i + 1);
            fprintf(f, "---------------------------------------------\n\n");
            fprintf(f, "    Name          : %s", zzz[i].name);
            fprintf(f, "    Age           : %d\n", zzz[i].age);
            fprintf(f, "    Blood group   : %s", zzz[i].bloodGroup);
            fprintf(f, "    Date of birth : %s\n", zzz[i].dob);
            fprintf(f, "---------------------------------------------\n");
        }

        fclose(f);
    }
}

void readData()
{
    FILE *f;
    f = fopen("temp.txt", "r");
    if (f == NULL)
    {
        perror("Error ");
    }
    else
    {
        char buffer[256];
        while ((fgets(buffer, sizeof(buffer), f)) != NULL)
        {
            printf("%s", buffer);
        }
        fclose(f);
    }
}
