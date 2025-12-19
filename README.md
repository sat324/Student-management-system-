# Student-management-system-
C programing 
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct Student {
    int roll;
    char name[50];
    float marks;
};

void addStudent() {
    struct Student s;
    FILE *fp = fopen("students.txt", "a");

    if (fp == NULL) {
        printf("File not found!\n");
        return;
    }

    printf("\nEnter Roll Number: ");
    scanf("%d", &s.roll);
    printf("Enter Name: ");
    scanf(" %[^\n]", s.name);
    printf("Enter Marks: ");
    scanf("%f", &s.marks);

    fprintf(fp, "%d %s %.2f\n", s.roll, s.name, s.marks);
    fclose(fp);

    printf("\nStudent record added successfully!\n");
}

void displayStudents() {
    struct Student s;
    FILE *fp = fopen("students.txt", "r");

    if (fp == NULL) {
        printf("\nNo records found!\n");
        return;
    }

    printf("\nRoll\tName\t\tMarks\n");
    printf("---------------------------------\n");

    while (fscanf(fp, "%d %s %f", &s.roll, s.name, &s.marks) != EOF) {
        printf("%d\t%-15s\t%.2f\n", s.roll, s.name, s.marks);
    }

    fclose(fp);
}

void searchStudent() {
    struct Student s;
    int roll, found = 0;
    FILE *fp = fopen("students.txt", "r");

    if (fp == NULL) {
        printf("\nNo records found!\n");
        return;
    }

    printf("\nEnter roll number to search: ");
    scanf("%d", &roll);

    while (fscanf(fp, "%d %s %f", &s.roll, s.name, &s.marks) != EOF) {
        if (s.roll == roll) {
            printf("\nRecord Found!");
            printf("\nRoll: %d\nName: %s\nMarks: %.2f\n",
                   s.roll, s.name, s.marks);
            found = 1;
            break;
        }
    }

    if (!found)
        printf("\nStudent record not found!\n");

    fclose(fp);
}

int main() {
    int choice;

    do {
        printf("\n===== Student Management System =====");
        printf("\n1. Add Student");
        printf("\n2. Display All Students");
        printf("\n3. Search Student");
        printf("\n4. Exit");
        printf("\nEnter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                addStudent();
                break;
            case 2:
                displayStudents();
                break;
            case 3:
                searchStudent();
                break;
            case 4:
                printf("\nExiting program...\n");
                break;
            default:
                printf("\nInvalid choice!\n");
        }
    } while (choice != 4);

    return 0;
}

