Below are **clean, student-facing C++ notes** on **`switch–case` and `break`**, written **exactly at beginner level**, suitable for **school students** and **classroom teaching**.

You can **read this aloud**, **share as notes**, or **print** it.

---

# C++ Notes

## Switch–Case Statement & Break Statement

---

## 1. Why do we need switch–case?

When a program has **many fixed choices**, writing multiple `if–else` statements becomes **long and confusing**.

`switch–case` is used to:

* Make programs **clean**
* Handle **menu-based choices**
* Improve **readability**

---

## 2. What is a switch–case?

`switch–case` is a **decision-making statement** used when:

* We compare **one variable**
* With **multiple fixed values**

---

## 3. Syntax of switch–case

```cpp
switch(variable) {
    case value1:
        statements;
        break;

    case value2:
        statements;
        break;

    default:
        statements;
}
```

---

## 4. Important Rules

1. The `variable` inside `switch` must be:

   * `int`
   * `char`
2. Each `case` must have:

   * A **constant value**
3. `default` is:

   * Optional
   * Runs when no case matches
4. `break` is used to:

   * Stop execution of the switch block

---

## 5. Simple Example – Menu Program

```cpp
#include <iostream>
using namespace std;

int main() {
    int choice;

    cout << "1. Tea" << endl;
    cout << "2. Coffee" << endl;
    cout << "3. Juice" << endl;
    cout << "Enter your choice: ";
    cin >> choice;

    switch (choice) {
        case 1:
            cout << "You selected Tea";
            break;

        case 2:
            cout << "You selected Coffee";
            break;

        case 3:
            cout << "You selected Juice";
            break;

        default:
            cout << "Invalid choice";
    }

    return 0;
}
```

---

## 6. How switch–case Works (Step-by-Step)

1. Program reads `choice`
2. `switch(choice)` checks the value
3. Matching `case` is executed
4. `break` stops further checking
5. If no case matches → `default` runs

---

## 7. What is the break Statement?

The `break` statement:

* **Immediately exits** the switch block
* Prevents execution of other cases

---

## 8. What happens if break is NOT used?

This is called **fall-through**.

### Example (Without break):

```cpp
switch(choice) {
    case 1:
        cout << "Tea";
    case 2:
        cout << "Coffee";
    case 3:
        cout << "Juice";
}
```

### Output if choice = 1:

```
TeaCoffeeJuice
```

👉 All cases below the match are executed.

---

## 9. Correct Example (With break)

```cpp
switch(choice) {
    case 1:
        cout << "Tea";
        break;

    case 2:
        cout << "Coffee";
        break;

    case 3:
        cout << "Juice";
        break;
}
```

---

## 10. When to use switch–case vs if–else

| switch–case           | if–else             |
| --------------------- | ------------------- |
| Fixed values          | Conditions & ranges |
| Cleaner menu programs | Complex logic       |
| Faster execution      | Flexible            |
| No range checks       | Supports range      |

---

## 11. Common Mistakes by Students

❌ Forgetting `break`
❌ Using float or string in switch
❌ Missing `default`
❌ Writing conditions like `case x > 5`

---

## 12. Practice Questions

### Q1.

Create a menu:

* 1 → Add
* 2 → Subtract
* 3 → Multiply
* Else → Invalid

### Q2.

Accept a character:

* `A` → Apple
* `B` → Ball
* `C` → Cat

### Q3.

What happens if `break` is removed?

---

## 13. Key Takeaways

* `switch–case` is used for **multiple fixed choices**
* `break` prevents **fall-through**
* `default` handles **invalid inputs**
* Ideal for **menu-based programs**

---

## 14. What’s Next?

➡️ **Loops**

* `for`
* `while`
* `do–while`

> “Now the computer will repeat decisions automatically.”

---
