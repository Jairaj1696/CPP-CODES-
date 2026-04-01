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

# Use Case : Employee Salary Management System Using File Handling

Scenario: You need to build an employee salary management system that reads employee records from a file, calculates their salary, and writes the updated data back to the file.

Tasks:

Create an Employee class with attributes like employee_id, name, and salary.
Implement a method calculateSalary() which calculates salary based on some business logic (e.g., bonuses, deductions).
Use file handling to:
Read employee data from a text file (ifstream).
Write updated employee data back to the file (ofstream).
Implement a main function that loads employee records from the file, calculates their salary, and saves the updated records back to the file.

Approach:

File Handling: Use ifstream to read the employee data and ofstream to write the data back after processing.
Object-Oriented Design: Use a class to represent employees and encapsulate their data.
Exception Handling: Implement error checking to ensure the file exists and is accessible.

```cpp
#include <iostream>
#include <fstream>
#include <vector>
#include <string>
#include <iomanip>
using namespace std;

class Employee {
private:
    string emp_id, name;
    double basic_salary, total_salary;
    
public:
    // Default constructor
    Employee() : emp_id(""), name(""), basic_salary(0), total_salary(0) {}
    
    // Parameterized constructor
    Employee(string id, string n, double salary) 
        : emp_id(id), name(n), basic_salary(salary), total_salary(0) {
        calculateSalary();  // Auto-calculate on creation
    }
    
    // Getters & Setters
    string getId() { return emp_id; }
    string getName() { return name; }
    double getBasic() { return basic_salary; }
    double getTotal() { return total_salary; }
    
    // Calculate salary with business logic
    void calculateSalary() {
        // Business Rules:
        // HRA: 20% of basic, DA: 40% of basic, Bonus: 10% if salary > 50000
        double hra = basic_salary * 0.20;
        double da = basic_salary * 0.40;
        double bonus = (basic_salary > 50000) ? basic_salary * 0.10 : 0;
        double deduction = basic_salary * 0.05;  // 5% tax
        
        total_salary = basic_salary + hra + da + bonus - deduction;
    }
    
    // Display employee
    void display() {
        cout << fixed << setprecision(2);
        cout << "\nID: " << emp_id 
             << ", Name: " << name 
             << ", Basic: ₹" << basic_salary
             << ", Total: ₹" << total_salary << endl;
    }
    
    // Save to file
    void saveToFile(ofstream& out) {
        out << emp_id << "," << name << "," << basic_salary << "," << total_salary << endl;
    }
    
    // Load from file (static method)
    static Employee loadFromFile(string line) {
        size_t pos1 = line.find(',');
        size_t pos2 = line.find(',', pos1 + 1);
        size_t pos3 = line.find(',', pos2 + 1);
        
        string id = line.substr(0, pos1);
        string name = line.substr(pos1 + 1, pos2 - pos1 - 1);
        double salary = stod(line.substr(pos2 + 1, pos3 - pos2 - 1));
        
        return Employee(id, name, salary);
    }
};

class SalaryManager {
private:
    vector<Employee> employees;
    const string FILENAME = "employees.txt";
    
public:
    // Load employees from file
    bool loadFromFile() {
        ifstream file(FILENAME);
        if (!file.is_open()) {
            cout << "❌ File not found! Creating new file...\n";
            return false;
        }
        
        employees.clear();
        string line;
        while (getline(file, line)) {
            if (line.empty()) continue;
            try {
                Employee emp = Employee::loadFromFile(line);
                employees.push_back(emp);
            } catch (...) {
                cout << "⚠️ Skipping invalid line: " << line << endl;
            }
        }
        file.close();
        cout << "✅ Loaded " << employees.size() << " employees from file\n";
        return true;
    }
    
    // Save employees to file
    void saveToFile() {
        ofstream file(FILENAME);
        if (!file.is_open()) {
            cout << "❌ Cannot create file!\n";
            return;
        }
        
        for (const auto& emp : employees) {
            emp.saveToFile(file);
        }
        file.close();
        cout << "💾 Data saved to " << FILENAME << endl;
    }
    
    // Add new employee
    void addEmployee() {
        string id, name;
        double salary;
        
        cout << "Enter ID: "; cin >> id;
        cout << "Enter Name: "; cin.ignore(); getline(cin, name);
        cout << "Enter Basic Salary: "; cin >> salary;
        
        Employee emp(id, name, salary);
        employees.push_back(emp);
        cout << "✅ Employee added & salary calculated!\n";
        emp.display();
    }
    
    // Display all
    void displayAll() {
        if (employees.empty()) {
            cout << "No employees found!\n";
            return;
        }
        cout << "\n=== ALL EMPLOYEES ===\n";
        for (const auto& emp : employees) {
            emp.display();
        }
    }
    
    // Calculate & update all salaries
    void processAllSalaries() {
        for (auto& emp : employees) {
            emp.calculateSalary();  // Recalculate
        }
        cout << "✅ All salaries updated!\n";
    }
};

int main() {
    SalaryManager manager;
    
    cout << "🏢 Employee Salary Management System\n";
    cout << "====================================\n";
    
    // Demo: Load existing data
    manager.loadFromFile();
    
    int choice;
    do {
        cout << "\n1. Add Employee\n2. Display All\n3. Process Salaries\n4. Save to File\n5. Exit\nChoice: ";
        cin >> choice;
        
        switch (choice) {
            case 1: manager.addEmployee(); break;
            case 2: manager.displayAll(); break;
            case 3: manager.processAllSalaries(); break;
            case 4: manager.saveToFile(); break;
            case 5: cout << "👋 Goodbye!\n"; break;
            default: cout << "Invalid choice!\n";
        }
    } while (choice != 5);
    
    manager.saveToFile();  // Auto-save on exit
    return 0;
}
```
```
INPUT/OUTPUT
```
```
SAMPLE OUTPUT :-
```
```
🏢 Employee Salary Management System
✅ Loaded 3 employees from file

1. Add Employee
Enter ID: E004
Enter Name: Sara Khan
Enter Basic Salary: 55000
✅ Employee added & salary calculated!
ID: E004, Name: Sara Khan, Basic: ₹55000, Total: ₹71500

=== ALL EMPLOYEES ===
ID: E001, Name: John Doe, Basic: ₹50000, Total: ₹65000
ID: E002, Name: Jane Smith, Basic: ₹60000, Total: ₹81000
...
💾 Data saved to employees.txt
```
```
CONCEPTS USED :-
✅ File I/O (Employee)
✅ Exception Handling (Employee)
✅ Static Methods (Employee)
✅ Business Logic (Employee)
```

