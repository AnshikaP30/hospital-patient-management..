# hospital-patient-management..
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct Patient {
    int id;
    char name[50];
    int age;
    char disease[100];
    struct Patient* next;
} Patient;
Patient* head = NULL;
Patient* createPatient(int id, const char* name, int age, const char* disease) {
    Patient* newPatient = (Patient*)malloc(sizeof(Patient));
    newPatient->id = id;
    strcpy(newPatient->name, name);
    newPatient->age = age;
    strcpy(newPatient->disease, disease);
    newPatient->next = NULL;
    return newPatient;
}
void addPatient() {
    int id, age;
    char name[50], disease[100];

    printf("Enter patient ID: ");
    scanf("%d", &id);
    printf("Enter patient name: ");
    scanf(" %[^\n]", name);  
    printf("Enter patient age: ");
    scanf("%d", &age);
    printf("Enter disease: ");
    scanf(" %[^\n]", disease);

    Patient* newPatient = createPatient(id, name, age, disease);
    newPatient->next = head;
    head = newPatient;

    printf("Patient added successfully!\n");
}
void viewPatients() {
    if (head == NULL) {
        printf("No patients found.\n");
        return;
    }
    Patient* temp = head;
    printf("\n--- Patient List ---\n");
    while (temp != NULL) {
        printf("ID: %d, Name: %s, Age: %d, Disease: %s\n", temp->id, temp->name, temp->age, temp->disease);
        temp = temp->next;
    }
}
void searchPatient() {
    int id;
    printf("Enter patient ID to search: ");
    scanf("%d", &id);

    Patient* temp = head;
    while (temp != NULL) {
        if (temp->id == id) {
            printf("Patient found: ID: %d, Name: %s, Age: %d, Disease: %s\n", temp->id, temp->name, temp->age, temp->disease);
            return;
        }
        temp = temp->next;
    }
   printf("Patient with ID %d not found.\n", id);
}
void dischargePatient() {
    int id;
    printf("Enter patient ID to discharge: ");
    scanf("%d", &id);
    Patient* temp = head;
    Patient* prev = NULL;

    while (temp != NULL && temp->id != id) {
        prev = temp;
        temp = temp->next;
    }
    if (temp == NULL) {
        printf("Patient with ID %d not found.\n", id);
        return;
    }
    if (prev == NULL) {
        head = temp->next;
    } else {
        prev->next = temp->next;}
    free(temp);
    printf("Patient with ID %d discharged.\n", id);
}

int main() {
    int choice;
    do {
        printf("\n--- Hospital Patient Management System ---\n");
        printf("1. Add Patient\n");
        printf("2. View All Patients\n");
        printf("3. Search Patient by ID\n");
        printf("4. Discharge Patient\n");
        printf("5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1: addPatient(); break;
            case 2: viewPatients(); break;
            case 3: searchPatient(); break;
            case 4: dischargePatient(); break;
            case 5: printf("Exiting...\n"); break;
            default: printf("Invalid choice!\n");
        }
    } while (choice != 5);
    return 0;
}
