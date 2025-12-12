# Grade Classification — C++ (Student-facing)

![Flowchart](/mnt/data/d13da16a-fbe2-4d14-a645-fd48fbcb3760.png)

**Target audience:** School/college beginners learning conditionals in C++.

---

# 1. What is the task? (One-line)
Given a student's numeric marks (0–100), print whether the student has **Distinction**, **1st Class**, **Pass**, or **Fail** following the flowchart decisions.

> **Flowchart logic (read from top):**
> - If `marks > 80` → **Distinction**
> - Else if `marks > 60` → **1st Class**
> - Else if `marks > 50` → **Pass**
> - Else → **Fail**

Note: The flowchart uses strict greater-than (`>`). So `marks = 80` ⇒ *not* Distinction; it will be checked next and become 1st Class.

---

# 2. Concepts you'll use
- `if / else if / else` ladder
- Functions to organize code
- Input validation (numeric range)
- `std::cin`, `std::cout` for I/O

---

# 3. Pseudocode (super short)
```
function classify_marks(marks):
    if marks > 80: return "Distinction"
    else if marks > 60: return "1st Class"
    else if marks > 50: return "Pass"
    else: return "Fail"
```

---

# 4. Complete C++ code (copy, paste, compile)
```cpp
#include <iostream>
#include <stdexcept>
using namespace std;

string classify_marks(double marks) {
    if (marks < 0 || marks > 100) {
        throw invalid_argument("Marks must be between 0 and 100");
    }
    if (marks > 80) return "Distinction";
    else if (marks > 60) return "1st Class";
    else if (marks > 50) return "Pass";
    else return "Fail";
}

int main() {
    string name;
    double marks;

    cout << "Enter student name: ";
    getline(cin, name);

    cout << "Enter marks (0-100): ";
    if (!(cin >> marks)) {
        cout << "Invalid numeric input. Exiting.\n";
        return 1;
    }

    try {
        string result = classify_marks(marks);
        cout << name << ": " << marks << " -> " << result << endl;
    } catch (const exception &e) {
        cout << "Error: " << e.what() << endl;
        return 1;
    }

    return 0;
}
```

**How to run:**
- Save as `grade.cpp` → `g++ -std=c++17 grade.cpp -o grade` → `./grade` (Linux/Mac) or `grade.exe` (Windows).

---

# 5. Sample runs (what students should see)
- Input: `Asha`, `92` → Output: `Asha: 92 -> Distinction`
- Input: `Rohit`, `75` → Output: `Rohit: 75 -> 1st Class`
- Input: `Neha`, `58` → Output: `Neha: 58 -> Pass`
- Input: `Vikas`, `43` → Output: `Vikas: 43 -> Fail`

---

# 6. Classroom tips (teacher → student notes)
- **Order matters:** Start checking from highest mark threshold to lowest. That prevents lower conditions from capturing a mark that actually qualifies for a higher category.
- **Use `else if` not separate `if` statements.** Separate `if`s will allow multiple branches to run.
- **Boundary clarity:** With `>`, the exact numbers 80, 60, 50 go to the lower category. If your school wants 80 → Distinction, change `>` to `>=` and inform the tester.
- **Validation:** Always check for values outside 0–100 and non-numeric input.

---

# 7. Quick exercises for students
1. Change code so `>=` is used (80 and above = Distinction). Test boundary values: 80, 60, 50.
2. Read a list of students (name + marks) from input until EOF and print counts of each category.
3. Save results to a file `results.txt` in the format `name,marks,classification`.
4. Add rounding: accept marks as floats, round to nearest integer before classification—test effect on 80.4 and 79.6.

---

# 8. Common mistakes (and how to fix)
- **Using multiple independent `if`**: causes more than one classification — use `else if`.
- **Incorrect boundary operators:** decide `>` vs `>=` upfront.
- **Not validating input:** handle non-numeric input from `cin`.
- **Hardcoding strings in many places:** return classification from one function so it’s easy to change later.

---

# 9. Mini 10–15 minute lesson plan
1. Show the flowchart and explain each decision (2 min).
2. Write the pseudocode on board (2 min).
3. Type the `classify_marks` function together (5 min).
4. Demonstrate 3 sample runs (3 min).
5. Give exercise #1 and 2 as homework (3 min).

---

If you want, I can now:
- produce a printable PDF of this single-page note, or
- create a single-slide image of the flowchart with the code side-by-side for a class handout.

Which would you like next?

