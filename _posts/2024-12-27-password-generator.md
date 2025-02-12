---
title: "Password Generator"
date: 2024-12-27 00:00:00 +0800
categories: [SCRIPTS]
tags: [PYHTON]
---


# Password Generator
This Python script generates a random password based on user input. It validates the input to ensure the length is between 8 and 16 characters. If the length is too short or too long, it displays an error message. Otherwise, it generates and displays a password of the specified length using letters, digits, and punctuation.

# generate_password.py

I am going to create a short python project that will generate a password that meets the standard provided by NIST.

- Length Over Complexity
	- NIST recommends that passwords be at least **8 characters** long, with longer passwords (e.g., 12-16 characters) being even better for security.

- Password Complexity
	- No specific requirements for using uppercase, lowercase, numbers, or symbols.
	- Focus on **password length** and **entropy** (randomness) instead.

- Avoid Common Passwords
	- Don’t use easy-to-guess passwords like "password123" or "123456".

# Why use this?

- **Input Validation**: This ensures that the password length is within the valid range (8 to 16 characters). If the user tries to enter a value outside this range, the program notifies them.

- **Guidance**: By capping the password length to 16 characters, it prevents users from requesting excessively long passwords, which might not be practical or necessary in most cases.

- **User Experience**: It ensures that the program works with reasonable parameters, guiding users towards the expected input.

# Code Breakdown

## How will it work:

- **If the user enters a password length less than 8**:
    - The message "Desired password must be at least 8 characters." is shown.

- **If the user enters a password length greater than 16**:
    - The message "Password length is capped at 16 characters." is shown.

- **If the user enters a valid length (between 8 and 16 characters)**:
    - A random password of the specified length is generated and displayed.


```python
import random
import string
```

These are **import statements** in Python, which allow you to use functionality from two standard Python libraries: `random` and `string`. Here's what they mean:

### 1. **`import random`**:

- This imports the **random module**, which provides functions for generating random numbers and performing random operations.
- For example, it allows you to pick random items from a list, generate random numbers, or shuffle sequences randomly.

### 2. **`import string`**:

- This imports the **string module**, which contains a collection of string constants that are useful for string manipulation.
- For example, `string.ascii_letters` contains all the lowercase and uppercase English letters (`'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'`).
- Example usage:

```python
def generate_password(length=12):
```

The statement `def generate_password(length=12):` in Python defines a **function** called `generate_password` with a **parameter** named `length`, which has a default value of `12`.

Here’s a breakdown of each part:

1. **`def`**: This is the keyword used to define a function in Python.
    
2. **`generate_password`**: This is the **name** of the function. When you call this function later in your code, you will use this name.
    
3. **`length=12`**:
    
    - **`length`** is the **parameter** of the function, which allows you to specify how long you want the password to be when you call the function.
    - **`=12`** means that **12 is the default value** for `length`. This means that if you call the function without specifying a value for `length`, it will default to 12 characters.
    - If you want a password of a different length, you can pass that length when you call the function, like `generate_password(16)`, which would generate a password with 16 characters.

```python
characters = string.ascii_letters + string.digits + string.punctuation
```

```python
password = ''.join(random.choice(characters) for _ in range(length))
```

```python
return password
```

- The code defines a set of characters (letters, digits, and punctuation). It then generates a random password by randomly selecting characters from that set, repeating for the desired length. The generated password is returned as a string.

- **`characters = string.ascii_letters + string.digits + string.punctuation`**:
    
    - This line creates a string called `characters`, which contains a combination of:
        - **`string.ascii_letters`**: All lowercase and uppercase English letters (`'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'`).
        - **`string.digits`**: All digits (`'0123456789'`).
        - **`string.punctuation`**: All punctuation marks (`'!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~'`).
    - So, `characters` will include all letters, numbers, and special characters.

- **`password = ''.join(random.choice(characters) for _ in range(length))`**:
    
    - **`random.choice(characters)`**: This picks a random character from the `characters` string (which now contains letters, digits, and punctuation).

    - **`for _ in range(length)`**: This is a **loop** that repeats the process of selecting a random character, `length` times (e.g., if `length` is 12, it picks 12 random characters).

    - **`''.join()`**: The `join()` method takes all the randomly chosen characters (which are in the form of a list) and joins them together into a single string. The `''` means the characters are joined without any spaces or other separators between them.

    - As a result, this line creates a random password with the specified **`length`** using characters from the `characters` set.

- **`return password`**:
    
    - This returns the generated password from the function.

```python
if __name__ == "__main__":

    password_length = int(input("Enter desired password length: "))
```

#### What Happens:

1. The program starts by checking if it is run directly (`if __name__ == "__main__":`).
2. It prompts the user to enter the password length: `Enter desired password length:`.
3. The user inputs a number (e.g., `8`).
4. The script generates a password with the specified length (in this case, 8 characters) and prints it.

```python
if password_length < 8:

        print("Desired password must be at least 8 characters.")
```

This is a conditional statement that checks if the user-provided password length is **less than 8** characters. Here's a breakdown of how it works:

### 1. **`if password_length < 8:`**

- This checks whether the value stored in the variable `password_length` is **less than 8**.
- **`password_length`** is expected to be an integer that represents the length of the password the user wants to generate (e.g., 12, 5, 15).
- If `password_length` is indeed less than 8, the code inside the `if` block will be executed.

### 2. **`print("Desired password must be at least 8 characters.")`**

- If the condition (`password_length < 8`) is **true**, the program will print the message `"Desired password must be at least 8 characters."`.
- This serves as a **validation message**, informing the user that the password length they entered is too short, and the program is enforcing a minimum password length of 8 characters.

```python
elif password_length > 16:

        print("Password length is capped at 16 characters.")
```

- **`elif password_length > 16:`**:
    - **`elif`** stands for "else if," which is used in a chain of conditions to check if the previous condition(s) weren't met and this one is true.

    - In this case, it checks if the **password length** is greater than 16 characters.

    - If the user enters a number greater than 16 (e.g., 18 or 20), this condition will be **true**.


- **`print("Password length is capped at 16 characters.")`**:
    - If the condition `password_length > 16` is **true**, this message will be printed, informing the user that the maximum password length is limited to 16 characters.

```python
else:

        generated_password = generate_password(password_length)

        print("Here is your password:",generated_password)
```

- **`else:`**:
    
    - The `else` block is executed **if none of the previous conditions** (`password_length < 8` and `password_length > 16`) are true.

    - This means that the **password length is between 8 and 16 characters**, which is acceptable.

- **`generated_password = generate_password(password_length)`**:
    
    - If the password length is valid (between 8 and 16 characters), this line calls the `generate_password()` function, passing the `password_length` as an argument.

    - The function will generate a random password of the specified length and store it in the variable `generated_password`.

- **`print("Here is your password:", generated_password)`**:
    
    - Finally, the program prints the generated password to the user.

# Full Code Example

```python
import random
import string

def generate_password(length=12):
    characters = string.ascii_letters + string.digits + string.punctuation
    password = ''.join(random.choice(characters) for _ in range(length))
    return password

if __name__ == "__main__":
    password_length = int(input("Enter desired password length: "))

    # Check if the entered password length is less than 8
    if password_length < 8:
        print("Desired password must be at least 8 characters.")
    # Check if the entered password length is greater than 16
    elif password_length > 16:
        print("Password length is capped at 16 characters.")
    else:
        # Generate and display the password if it's between 8 and 16 characters
        generated_password = generate_password(password_length)
        print("Here is your password:", generated_password)

```

## Scenarios

#### Scenario 1: User enters a password length less than 8:

```
Enter desired password length: 5
Desired password must be at least 8 characters.

```

#### Scenario 2: User enters a password length greater than 16:

```
Enter desired password length: 20
Password length is capped at 16 characters.

```

#### Scenario 3: User enters a valid password length between 8 and 16:

```
Enter desired password length: 12
Here is your password: h3#9bLx!yF2k

```
