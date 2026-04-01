# CPP-CODES-

# Use Case : Student Record System with Classes and Objects

Scenario: You need to develop a student record management system for a college. The system should allow the addition of student records, modification, and display of records, as well as calculations like average grades.

Tasks:

Class Design: Create a Student class with data members like roll_number, name, and marks.
Implement a constructor to initialize student records when an object is created and a destructor to clean up resources if needed.
Include methods like addStudent(), modifyStudent(), displayStudent(), and calculateAverage().
Use overloaded constructors to initialize students with different data (e.g., full info vs just roll number).

Approach:

Class and objects: Use a class to represent the student, encapsulating the details of each student.
Inheritance: You could extend this to have subclasses like GraduateStudent or UndergraduateStudent, which inherit from Student and add more specialized data.
Polymorphism: Use method overloading for various operations like addStudent() (with different types of arguments).

```cpp
include <iostream>
using namespace std;

class Student {
private:
    int roll_number;
    string name;
    float marks[5];

public:
    // Default Constructor
    Student() {
        roll_number = 0;
        name = "Unknown";
        for(int i = 0; i < 5; i++) {
            marks[i] = 0;
        }
    }

    // Overloaded Constructor (full info)
    Student(int r, string n, float m[]) {
        roll_number = r;
        name = n;
        for(int i = 0; i < 5; i++) {
            marks[i] = m[i];
        }
    }

    // Overloaded Constructor (only roll number)
    Student(int r) {
        roll_number = r;
        name = "Not Assigned";
        for(int i = 0; i < 5; i++) {
            marks[i] = 0;
        }
    }

    // Destructor
    ~Student() {
        cout << "Destructor called for Roll No: " << roll_number << endl;
    }

    // Add Student
    void addStudent() {
        cout << "Enter Roll Number: ";
        cin >> roll_number;
        cout << "Enter Name: ";
        cin >> name;

        cout << "Enter marks for 5 subjects:\n";
        for(int i = 0; i < 5; i++) {
            cin >> marks[i];
        }
    }

    // Modify Student
    void modifyStudent() {
        cout << "Modify Name: ";
        cin >> name;

        cout << "Modify marks:\n";
        for(int i = 0; i < 5; i++) {
            cin >> marks[i];
        }
    }

    // Display Student
    void displayStudent() {
        cout << "\nRoll Number: " << roll_number;
        cout << "\nName: " << name;
        cout << "\nMarks: ";
        for(int i = 0; i < 5; i++) {
            cout << marks[i] << " ";
        }
        cout << "\nAverage: " << calculateAverage() << endl;
    }

    // Calculate Average
    float calculateAverage() {
        float sum = 0;
        for(int i = 0; i < 5; i++) {
            sum += marks[i];
        }
        return sum / 5;
    }
};


// ---------------- Inheritance Example ----------------

class GraduateStudent : public Student {
private:
    string research_topic;

public:
    void setResearchTopic() {
        cout << "Enter Research Topic: ";
        cin >> research_topic;
    }

    void displayGraduate() {
        displayStudent();
        cout << "Research Topic: " << research_topic << endl;
    }
};


// ---------------- Main Function ----------------

int main() {
    Student s1;
    s1.addStudent();
    s1.displayStudent();

    cout << "\n--- Modify Student ---\n";
    s1.modifyStudent();
    s1.displayStudent();

    cout << "\n--- Using Overloaded Constructor ---\n";
    float marks[5] = {80, 85, 90, 75, 88};
    Student s2(101, "Rahul", marks);
    s2.displayStudent();

    cout << "\n--- Graduate Student ---\n";
    GraduateStudent g1;
    g1.addStudent();
    g1.setResearchTopic();
    g1.displayGraduate();

    return 0;
}
```
```
INPUT/OUTPUT
```
```
Enter Roll Number: 1
Enter Name: Jairaj
Enter marks for 5 subjects:
89 96 99 85 88

Roll Number: 1
Name: Jairaj
Marks: 89 96 99 85 88 
Average: 91.4

--- Modify Student ---
Modify Name: Jairaj Bisht
Modify marks:

Roll Number: 1
Name: Jairaj
Marks: 0 96 99 85 88 
Average: 73.6

--- Using Overloaded Constructor ---

Roll Number: 101
Name: Rahul
Marks: 80 85 90 75 88 
Average: 83.6

--- Graduate Student ---
Enter Roll Number: Enter Name: Enter marks for 5 subjects:
Enter Research Topic: 
Roll Number: 0
Name: Unknown
Marks: 0 0 0 0 0 
Average: 0
Research Topic: 
Destructor called for Roll No: 0
Destructor called for Roll No: 101
Destructor called for Roll No: 1
```
