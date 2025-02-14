[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/_Y4t8UXw)
# dgl104-programming-article-repo
# CODE REVIEW

## Introduction
In an academic context, code review is done with the purpose of allowing the student to improve their understanding when performing tests and improve their programming techniques. This is achieved by early detection of errors in the program code or more efficient alternatives to the initial implementation. It is also “used as a technique to improve the qualities of the developers involved in the practice” (Sadowski et al., 2018, p. 8). , through open discussion of possible improvements to the program.

Code review is not only used in academic settings. When the programmer is in a work environment, he must develop plans for software development in which code review is one of the points that must be addressed in all documentation to comply with the health and quality of the applications.

Software companies are constantly looking to improve their products. An essential element in these companies are software engineers, where each engineer produces a series of modules or components that are integrated to form a functional software system. If these companies wish to maintain a high level of competitiveness, it is extremely important to improve the efficiency, productivity and quality of the software products produced by each of their engineers.

It is important to keep in mind that the development process that each developer follows is essential for the construction and improvement of applications, since although it is known that a developer will not be in the same job for a long time, it is important that his work is very well documented and with the required standards so that the next developer who works on it can do the code review appropriately and quickly.


## Aspects to consider in A code review

### DESIGN
When evaluating the design of a code change, it is critical to analyze the overall architecture and determine whether the new modifications remain consistent with the existing system. This involves reviewing the interaction between the different modules and ensuring that the new functionality is integrated without creating unnecessary coupling or breaking principles such as separation of responsibilities. To do so, it is important to verify that the implementation follows the design guidelines established by the team, including appropriate architectural patterns and correct code organization. 

It should also be considered whether the solution is scalable and flexible for future modifications. “Good design is crucial because it ensures the long-term maintainability of the system, prevents the generation of technical debt, and allows other developers to understand and interact with the code efficiently.” (Myers, 2018). A well-designed system minimizes the possibility of errors, facilitates debugging, and reduces the cost of future development.

### Good Code Design
```python
class User:
    def __init__(self, username: str, email: str):
        self.username = username
        self.email = email

    def __str__(self):
        return f"User: {self.username} - Email: {self.email}"

    def send_email(self, subject: str, message: str) -> None:
        print(f"Sending email to {self.email}\nSubject: {subject}\nMessage: {message}")

# Usage
user = User("john_doe", "john@example.com")
print(user)
user.send_email("Welcome!", "Thanks for joining our platform!")
```
#### Reasons
1. Clarity: The class is easy to read and understand.
2. Encapsulation: All user-related functionality is encapsulated within the `User` class this means that It is related exclusive.
3. Reusability and Extensibility: If you need more functionality later, you can add methods and it wont be complex.
4. Type Annotations: Helps prevent errors and improves readability giving context.

### Bad Code Design
```python
class User:
    def __init__(self, name_email):
        self.name_email = name_email

    def print_user(self):
        print("User details:", self.name_email)

    def send_email(self, message):
        print("Sending:", message)

# Usage
user = User("john_doe;john@example.com")
user.print_user()
user.send_email("Welcome!")
```
#### Reasons
1. Ambiguous Attributes: name_email is a single string containing both username and email then you will add another kind of method to separate.
2. Lack of Type Annotations: There is not explanation of the method.
3. Tight Coupling and Low Cohesion: The send_email method lacks context about the email recipient, potentially causing confusion.
4. Hard to Extend: Any future changes would require modifying existing code, and it could take to many time because probably you should do it again.

### FUNCTIONALITY
When evaluating the functionality of the code, it is essential to ensure that it meets the defined requirements and that its behavior is as expected in all possible circumstances. This involves reviewing the implemented logic to detect possible errors, omissions or misunderstandings in the requirements. An effective way to do this is to test the code in different scenarios, including extreme cases and unusual conditions that could cause failures. In addition, it is essential to verify that there are automated tests, such as unit and integration tests, that validate the correct functioning of the functionality both in isolation and in conjunction with the rest of the system. 

Ensuring functionality is crucial because it prevents the introduction of errors into the code base, improves the user experience and reduces the time needed for future corrections. “The ultimate goal of code review is to enhance code quality. Reviewers should prioritize aspects like readability, maintainability, and performance.” (Verdi, 2024).

### Good Functional
```python
class Calculator:
    def add(self, a: float, b: float) -> float:
        return a + b

    def subtract(self, a: float, b: float) -> float:
        return a - b

    def multiply(self, a: float, b: float) -> float:
        return a * b

    def divide(self, a: float, b: float) -> float:
        if b == 0:
            raise ValueError("Cannot divide by zero.")
        return a / b

# Usage
calc = Calculator()
print(calc.add(5, 3))        # 8
print(calc.divide(10, 2))    # 5
```

#### Reasons
1. lear and Predictable Behavior: Each method performs exactly one operation.
2. Input Validation: Division checks for division by zero, preventing runtime errors.
3. Error Handling: The program raises a meaningful exception rather than crashing unpredictably.

### Bad Functional 
```python
class Calculator:
    def calculate(self, a, b, op):
        if op == '+':
            return a + b
        elif op == '-':
            return a - b
        elif op == '*':
            return a * b
        elif op == '/':
            return a / b
        else:
            return "Invalid operation"

# Usage
calc = Calculator()
print(calc.calculate(5, 3, '+'))  # 8
print(calc.calculate(10, 0, '/')) # ZeroDivisionError
print(calc.calculate(5, 3, '%'))  # Invalid operation
```

#### Reasons
1. No Input Validation: Dividing by zero throws an unhandled exception.
2. Weak Error Feedback: Returns "Invalid operation" for unsupported operations instead of raising an exception and ends the process.
3. Overloaded Method: The calculate method does everything.
4. Reduced Readability: Using op strings requires remembering valid operation symbols, means more tasks for the user.

### TEST
Testing is an essential part of software development, ensuring that code works as expected and that future changes do not introduce errors. To assess the quality of testing, it is necessary to verify that the appropriate types of tests are in place, such as unit tests to validate individual functions and methods, integration tests to check the interaction between different modules, and end-to-end tests to simulate the behavior of the system. “Reviewers should test the code changes whenever possible. This includes running the code locally, testing edge cases, and verifying that the changes solve the problem”(Felice, 2023).

It is also important to assess the clarity and maintainability of the tests, ensuring that they are understandable and easy to update when the code changes. Implementing appropriate tests is critical because it allows errors to be detected before they reach production, reduces debugging time and effort, and provides confidence in the stability of the software as it evolves.

###  Good Test: Clean, Focused, and Maintainable
```python
import unittest

def add(a, b):
    """Simple function to add two numbers."""
    return a + b

class TestAddFunction(unittest.TestCase):
    def test_add_two_positive_numbers(self):
        # Clear and descriptive test name
        result = add(3, 5)
        self.assertEqual(result, 8, "3 + 5 should equal 8")

    def test_add_negative_and_positive_number(self):
        result = add(-2, 5)
        self.assertEqual(result, 3, "-2 + 5 should equal 3")

    def test_add_two_negative_numbers(self):
        result = add(-4, -6)
        self.assertEqual(result, -10, "-4 + -6 should equal -10")

if __name__ == "__main__":
    unittest.main()
```

#### Reasons
1. Descriptive Test Names: Each test name clearly states what it is testing.
2. Focused Tests: Each test checks one specific case, making it easy to identify what went wrong if a test fails.
3. Clear Assertions: The `assertEqual` statements include descriptive messages to clarify failures.
4. Readable and Maintainable: The code is simple to read and modify.

###  Bad Test: Unclear, Fragile, and Hard to Maintain
```python
import unittest

def add(a, b):
    return a + b

class TestAdd(unittest.TestCase):
    def test_add(self):
        # Testing multiple cases in one test — hard to debug failures
        self.assertEqual(add(2, 3), 5)
        self.assertEqual(add(-1, 1), 0)
        self.assertEqual(add(-2, -2), -4)
        self.assertEqual(add(0, 0), 0)
        # No descriptive messages and unclear intent

if __name__ == "__main__":
    unittest.main()
```

#### Reasons
1. Generic Test Name: `test_add` is too vague — what exactly is being tested here, this doesn't mean anything.
2. Multiple Assertions in One Test: If one assertion fails, the rest might not run, making debugging more difficult.
3. No Failure Messages: If a test fails, the output won’t give clear context of the errors or crashes.
4. Poor Readability: The test is less readable and harder to extend later.

### NAMING
Good code nomenclature is key to ensuring clarity, comprehensibility, and maintainability. To assess it, “it is important to check that the names of variables, functions, classes, and other elements are descriptive and accurately reflect their purpose within the system”(Mosalla, 2023). A good name should avoid ambiguity, be specific enough to indicate its function without the need for additional comments, and follow established project conventions, such as the use of camelCase, snake_case, or PascalCase, as appropriate. 

Names should also be verified to be consistent throughout the code, avoiding unnecessary abbreviations or unintuitive terms. Maintaining clear and structured nomenclature is essential, as it makes the code easier for other developers to read, reduces the time needed to understand it, and minimizes the possibility of errors caused by misinterpretations. Code with well-defined names is easier to maintain and modify in the long term, which contributes to the quality and scalability of the project.

### Good Naming Practices
```python
class BankAccount:
    def __init__(self, account_holder: str, initial_balance: float = 0.0):
        self.account_holder = account_holder
        self.balance = initial_balance

    def deposit(self, amount: float) -> None:
        if amount > 0:
            self.balance += amount
        else:
            raise ValueError("Deposit amount must be positive.")

    def withdraw(self, amount: float) -> None:
        if 0 < amount <= self.balance:
            self.balance -= amount
        else:
            raise ValueError("Insufficient funds or invalid amount.")

    def get_balance(self) -> float:
        return self.balance

# Usage
account = BankAccount("Alice", 1000)
account.deposit(200)
print(account.get_balance())  # 1200
```
#### Reasons
1. Descriptive Class Name: `BankAccount` clearly indicates the purpose of the class.
2. Clear Method Names: Methods like `deposit`, `withdraw`, and `get_balance` are intuitive.
3. Meaningful Variables: `account_holder`, `balance`, and `amount` make the code easy to read.
4. Consistency: Follows Python's naming conventions (e.g., snake_case for methods and variables, PascalCase for classes).

### Bad Naming Practices
```python
class BA:
    def __init__(self, n, b=0.0):
        self.n = n
        self.b = b

    def d(self, a):
        self.b += a

    def w(self, a):
        if a <= self.b:
            self.b -= a

    def gb(self):
        return self.b

# Usage
acc = BA("Alice", 1000)
acc.d(200)
print(acc.gb())  # 1200
```
#### Reasons
1. Cryptic Class Name: `BA` is vague and unclear.
2. Unclear Variable Names: `n`, `b`, `a` provide no context about their purpose and there is no meaning.
3. Unintuitive Method Names: `d`, `w`, and `gb` are hard to decipher without reading the implementation, so what happen if you dont know it, you are not going to understand it.
4. Lack of Consistency: Abbreviations and single-letter names make the code hard to maintain because you don't know what are you changing.

### COMMENTS
Comments in code should be clear, concise, and bring real value to understanding the software. To evaluate them, it is important to check that they explain the “why” behind an implementation rather than simply describing what the code does, as the latter should be understandable on its own if it is well written. Comments should be used to clarify complex design decisions, highlight potential limitations or warnings about parts of the code that might not be immediately apparent. It is also critical to avoid unnecessary or redundant comments that only repeat what is already obvious in the implementation, as they can create noise and make the code difficult to read. 

“Check if the code has sufficient comments that explain the purpose of the code, how it works, and any assumptions or limitations. Ensure that the comments are accurate, up-to-date, and easy to understand”(Mosalla, 2023). This is especially useful in long-term projects or in large development teams, where different people will be working on the same code at different times.

### Good Commenting Practices
```python
class Invoice:
    def __init__(self, client_name: str, amount: float):
        # Initialize the invoice with client name and amount
        self.client_name = client_name
        self.amount = amount
        self.paid = False

    def mark_as_paid(self) -> None:
        """Mark the invoice as paid."""
        self.paid = True

    def generate_summary(self) -> str:
        """
        Generate a summary of the invoice.
        - Includes client name, amount, and payment status.
        """
        status = "Paid" if self.paid else "Unpaid"
        return f"Invoice for {self.client_name}: ${self.amount:.2f} - {status}"

# Usage
invoice = Invoice("Acme Corp", 500)
invoice.mark_as_paid()
print(invoice.generate_summary())
```

#### Reasons
1. Explains Intent: The `generate_summary` docstring explains the purpose, not the implementation details.
2. Concise and Relevant: Comments are short and relevant without restating obvious code.
3. Docstrings for Public Methods: Docstrings describe the behavior and expected output of key methods.

### Bad Commenting Practices
```python
class Inv:
    def __init__(self, cn, a):
        # This sets the name
        self.cn = cn  # name
        self.a = a    # amount
        self.p = False # payment

    def pay(self):
        # changes p to True
        self.p = True

    def sum(self):
        # makes a string
        return f"{self.cn}: {self.a} - {'Paid' if self.p else 'Unpaid'}"

# Usage
inv = Inv("Acme", 500)
inv.pay()
print(inv.sum())
```

#### Reasons
1. Obvious Comments: `# This sets the name` adds no value; the code already makes it clear.
2. Unhelpful Abbreviations: `cn`, `a`, and `p` are cryptic and require the comments to decipher.
3. Lack of Context: No explanation for why certain methods exist or how they should be used.
4. Misleading Comments: `# makes a string `is technically true but doesn't explain that it creates an invoice summary.

### COMMENTS
Documentation is an essential element of software development, providing clear guidance on how different parts of the code work and how they should be used. To evaluate it, it is important to ensure that functions, classes, and modules include detailed descriptions of their purpose, parameters, return values, and possible exceptions. “By checking for code documentation during a code review, you can ensure that the code is well-documented and easy to understand, reducing the time and effort required for future maintenance and development” (Mosalla, 2023).   

Documentation should be accurate and up to date, avoiding outdated information that could lead to errors. Good documentation is essential because it makes it easier for new developers to join the project, speeds up problem resolution, and allows code to be picked up more quickly after a period of not working on it. It also improves team collaboration by providing a clear reference on how the different components of the system interact.


## References

Hejderup, J. (2018). Code review analytics: Assessing the performance of code review practices in modern software development [Conference paper]. Proceedings of the 40th International Conference on Software Engineering: Software Engineering in Practice, 106–115. https://doi.org/10.1145/3183519.3183525

Bosu, A., Greiler, M., & Bird, C. (2013). Characteristics of useful code reviews: An empirical study at Microsoft [Conference paper]. 2013 35th International Conference on Software Engineering (ICSE), 1–11. IEEE. https://doi.org/10.1109/ICSE.2013.6606617

Hejderup, J. (2018). Code review analytics: Assessing the performance of code review practices in modern software development [Conference paper]. Proceedings of the 40th International Conference on Software Engineering: Software Engineering in Practice, 106–115. https://doi.org/10.1145/3183519.3183525

Torazaburo. (2022, March 11). Let’s do program design reviews, not just code reviews. Medium. https://torazaburo.medium.com/lets-do-program-design-reviews-not-just-code-reviews-dcb5788925ef

Graphite. (n.d.). Code review principles: A guide to effective code reviews. https://graphite.dev/guides/code-review-principles

BrowserStack. (2023, March 15). What is code review? A comprehensive guide. https://www.browserstack.com/guide/what-is-code-review

Mosalla, H. (2023, March 11). Code review: The ultimate guide. https://hamidmosalla.com/2023/03/11/code-review-the-ultimate-guide/
