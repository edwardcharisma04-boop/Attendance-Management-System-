#include <iostream>
#include <vector>
#include <fstream>
using namespace std;

// ---------- Student Management ----------
class Student {
private:
    int id;
    string name;

public:
    Student(int studentId, string studentName) {
        id = studentId;
        name = studentName;
    }

    int getId() { return id; }
    string getName() { return name; }

    void display() {
        cout << "ID: " << id << " | Name: " << name << endl;
    }
};

vector<Student> students;

void addStudent() {
    int id;
    string name;

    cout << "Enter Student ID: ";
    cin >> id;
    cin.ignore();

    cout << "Enter Student Name: ";
    getline(cin, name);

    students.push_back(Student(id, name));
    cout << "Student added successfully!\n";
}

void viewStudents() {
    for (Student s : students) {
        s.display();
    }
}

// ---------- Attendance Sessions ----------
class AttendanceSession {
private:
    string date;

public:
    AttendanceSession(string sessionDate) {
        date = sessionDate;
    }

    string getDate() { return date; }

    void displaySession() {
        cout << "Session Date: " << date << endl;
    }
};

vector<AttendanceSession> sessions;
vector<vector<bool>> attendance; // Week 3

void createSession() {
    string date;
    cin.ignore();
    cout << "Enter Session Date: ";
    getline(cin, date);

    sessions.push_back(AttendanceSession(date));
    vector<bool> sessionAttendance(students.size(), false);
    attendance.push_back(sessionAttendance);

    cout << "Session created successfully!\n";
}

void viewSessions() {
    for (AttendanceSession s : sessions) {
        s.displaySession();
    }
}

// ---------- Load Students from File ----------
void loadFromFile() {
    ifstream file("attendance.txt");

    if (!file) {
        cout << "File not found!\n";
        return;
    }

    int count;
    file >> count;
    file.ignore();

    students.clear();

    for (int i = 0; i < count; i++) {
        int id;
        string name;
        file >> id;
        file.ignore();
        getline(file, name);

        students.push_back(Student(id, name));
    }

    file.close();
    cout << "Data loaded successfully!\n";
}

// ---------- Main Menu ----------
int main() {
    int choice;

    do {
        cout << "\nAttendance Management System\n";
        cout << "1. Add Student\n";
        cout << "2. View Students\n";
        cout << "3. Load Students from File\n";
        cout << "4. Create Attendance Session\n";
        cout << "5. View Attendance Sessions\n";
        cout << "6. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1: addStudent(); break;
            case 2: viewStudents(); break;
            case 3: loadFromFile(); break;
            case 4: createSession(); break;
            case 5: viewSessions(); break;
            case 6: cout << "Exiting program.\n"; break;
            default: cout << "Invalid choice! Try again.\n";
        }

    } while (choice != 6);

    r
