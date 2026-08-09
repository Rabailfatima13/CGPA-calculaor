
Constructor Student(int numCourses) — sets numberOfCourses and heap-allocates a Course array of that size.

Destructor ~Student() — frees that array with delete[] to avoid a memory leak.

addCourse(index, courseName, credits, gradePoint) — fills in one course slot at the given index. No bounds checking, so passing an index outside [0, numberOfCourses) is undefined behavior.

calculateGPA() — computes weighted GPA: sums gradePoint × credits across all courses, divides by total credits. Guards against division by zero (returns 0.0 if totalCredits is 0).

showCourseGrades() — prints each course's name, credits, and grade point.

A couple of things worth knowing if you keep building on this:

addCourse has no bounds check on index — worth adding one since courses is a fixed-size array once constructed.
This class needs a proper copy constructor and copy assignment operator (Rule of Three) since it manages raw heap memory — otherwise copying a Student object will double-free courses when both copies get destructed.
