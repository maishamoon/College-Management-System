#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_STUDENTS 1000

struct Student {
    int id;
    char name[50];
    char password[50];
    char dob[20]; 
};

struct Student students[MAX_STUDENTS];
int numStudents = 0;

void studentRegistration();
void studentLogin();
int isPasswordCorrect(const char *inputPassword, const char *storedPassword);

int main() {
    int choice;

    while(1) {
        printf("\n\nCollege Management System\n");
        printf("1. Student Registration\n");
        printf("2. Student Login\n");
        printf("3. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch(choice) {
            case 1:
                studentRegistration();
                break;
            case 2:
                studentLogin();
                break;
            case 3:
                printf("Exiting program...\n");
                exit(0);
            default:
                printf("Invalid choice. Please try again.\n");
        }
    }

    return 0;
}

void studentRegistration() {
    struct Student newStudent;

    printf("\nStudent Registration\n");
    printf("Enter student ID: ");
    scanf("%d", &newStudent.id);
    printf("Enter student name: ");
    scanf("%s", newStudent.name);
    printf("Enter password: ");
    scanf("%s", newStudent.password);
    printf("Enter date of birth (DD/MM/YYYY): ");
    scanf("%s", newStudent.dob);
    students[numStudents++] = newStudent;
    printf("Student registered successfully.\n");
}

int isPasswordCorrect(const char *inputPassword, const char *storedPassword) {
    return strcmp(inputPassword, storedPassword) == 0;
}

void studentLogin() {
    int id;
    char password[50];
    int found = 0;

    printf("\nStudent Login\n");
    printf("Enter student ID: ");
    scanf("%d", &id);
    printf("Enter password: ");
    scanf("%s", password);

    for (int i = 0; i < numStudents; i++) {
        if (students[i].id == id) {
            if (isPasswordCorrect(password, students[i].password)) {
                printf("Login successful! Welcome, %s!\n", students[i].name);
                found = 1;
                break;
            } else {
                printf("Incorrect password. Please try again.\n");
                return;
            }
        }
    }

    if (!found) {
        printf("Student with ID %d not found.\n", id);
    }
}
