# Our-project-Hospital-management-
#include <iostream>
#include <string>
using namespace std;

// Structure for patient data
struct Patient {
    int id;
    string name;
    int age;
    string disease;
    Patient* next;
};

// Class for hospital management
class Hospital {
private:
    Patient* head;

public:
    Hospital() {
        head = NULL;
    }

    // Add new patient
    void addPatient(int id, string name, int age, string disease) {
        Patient* newPatient = new Patient();
        newPatient->id = id;
        newPatient->name = name;
        newPatient->age = age;
        newPatient->disease = disease;
        newPatient->next = NULL;

        if (head == NULL) {
            head = newPatient;
        } else {
            Patient* temp = head;
            while (temp->next != NULL) {
                temp = temp->next;
            }
            temp->next = newPatient;
        }
        cout << "Patient added successfully!\n";
    }

    // Display all patients
    void displayPatients() {
        if (head == NULL) {
            cout << "No patients in the record.\n";
            return;
        }

        Patient* temp = head;
        cout << "\n--- Patient List ---\n";
        while (temp != NULL) {
            cout << "ID: " << temp->id << endl;
            cout << "Name: " << temp->name << endl;
            cout << "Age: " << temp->age << endl;
            cout << "Disease: " << temp->disease << endl;
            cout << "----------------------\n";
            temp = temp->next;
        }
    }

    // Search patient by ID
    void searchPatient(int id) {
        Patient* temp = head;
        while (temp != NULL) {
            if (temp->id == id) {
                cout << "\nPatient Found!\n";
                cout << "ID: " << temp->id << endl;
                cout << "Name: " << temp->name << endl;
                cout << "Age: " << temp->age << endl;
                cout << "Disease: " << temp->disease << endl;
                return;
            }
            temp = temp->next;
        }
        cout << "Patient not found!\n";
    }

    // Delete patient by ID
    void deletePatient(int id) {
        if (head == NULL) {
            cout << "No records to delete.\n";
            return;
        }

        if (head->id == id) {
            Patient* temp = head;
            head = head->next;
            delete temp;
            cout << "Patient deleted successfully!\n";
            return;
        }

        Patient* prev = NULL;
        Patient* curr = head;
        while (curr != NULL && curr->id != id) {
            prev = curr;
            curr = curr->next;
        }

        if (curr == NULL) {
            cout << "Patient not found!\n";
            return;
        }

        prev->next = curr->next;
        delete curr;
        cout << "Patient deleted successfully!\n";
    }
};

// Main function
int main() {
    Hospital h;
    int choice, id, age;
    string name, disease;

    do {
        cout << "\n====== Hospital Management System ======\n";
        cout << "1. Add Patient\n";
        cout << "2. Display All Patients\n";
        cout << "3. Search Patient\n";
        cout << "4. Delete Patient\n";
        cout << "5. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            cout << "Enter ID: ";
            cin >> id;
            cout << "Enter Name: ";
            cin >> name;
            cout << "Enter Age: ";
            cin >> age;
            cout << "Enter Disease: ";
            cin >> disease;
            h.addPatient(id, name, age, disease);
            break;
        case 2:
            h.displayPatients();
            break;
        case 3:
            cout << "Enter ID to search: ";
            cin >> id;
            h.searchPatient(id);
            break;
        case 4:
            cout << "Enter ID to delete: ";
            cin >> id;
            h.deletePatient(id);
            break;
        case 5:
            cout << "Exiting program...\n";
            break;
        default:
            cout << "Invalid choice!\n";
        }
    } while (choice != 5);

    return 0;
}
