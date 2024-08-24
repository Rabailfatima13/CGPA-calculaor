# CGPA-calculaor

#include <iostream>
using namespace std;
class Course {
public:
    string courseName;
    int credits;
    double gradePoint;
};

class Student {
public:
    Course* courses;
    int numberOfCourses;

    Student(int numCourses) {
        numberOfCourses = numCourses;
        courses = new Course[numberOfCourses];
    }

    ~Student() {
        delete[] courses;
    }

    void addCourse(int index, string courseName, int credits, double gradePoint) {
        courses[index].courseName = courseName;
        courses[index].credits = credits;
        courses[index].gradePoint = gradePoint;
    }

    double calculateGPA() {
        double totalGradePoints = 0.0;
        int totalCredits = 0;

        for (int i = 0; i < numberOfCourses; ++i) {
            totalGradePoints += courses[i].gradePoint * courses[i].credits;
            totalCredits += courses[i].credits;
        }

        return totalCredits ? totalGradePoints / totalCredits : 0.0;
    }

    void showCourseGrades() {
        cout << "Course Grades:\n";
        for (int i = 0; i < numberOfCourses; ++i) {
            cout << "Course: " << courses[i].courseName
                 << ", Credits: " << courses[i].credits
                 << ", Grade: " << courses[i].gradePoint << "\n";
        }
    }
};

int main() {
    int numberOfCourses;

    cout << "Enter the number of courses: ";
    cin >> numberOfCourses;

    Student student(numberOfCourses);

    for (int i = 0; i < numberOfCourses; ++i) {
        string courseName;
        int credits;
        double gradePoint;

        cout << "\nEnter the name of course " << i + 1 << ": ";
        cin >> courseName;
        cout << "Enter the credits for " << courseName << ": ";
        cin >> credits;
        cout << "Enter the grade point for " << courseName << ": ";
        cin >> gradePoint;

        student.addCourse(i, courseName, credits, gradePoint);
    }

    student.showCourseGrades();
    double gpa = student.calculateGPA();
    cout << "\nOverall GPA: " << gpa << endl;

    return 0;
}

