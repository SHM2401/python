# Documentation for the Calculator Python Program

## Overview
This program is a simple **calculator** built using **Python's Tkinter** library for the graphical user interface (GUI). It allows users to perform basic arithmetic operations such as addition, subtraction, multiplication, division, and percentage calculation. The calculator has buttons for digits, operations, and special actions like clear (`C`) and evaluate (`=`).

The program uses the **`eval()`** function to evaluate mathematical expressions entered by the user.

---

## Features
- **Basic Arithmetic Operations**: Support for addition (`+`), subtraction (`-`), multiplication (`*`), division (`/`), and percentage (`%`).
- **Parentheses Handling**: Supports parentheses `(` and `)` to define the order of operations.
- **Clear (`C`) Button**: Clears the current input on the calculator screen.
- **Evaluate (`=`) Button**: Evaluates the mathematical expression entered by the user.
- **Simple and Intuitive GUI**: Buttons arranged in a grid layout for easy interaction.

---

## Project Structure
The project consists of the following components:
1. **Tkinter GUI**: The user interface that includes the input field and buttons.
2. **Main Calculator Logic**: The logic for handling button clicks, performing calculations, and displaying results.

---

## GUI Design
- **Window Title**: "Calculator".
- **Window Size**: 357x420 pixels.
- **Window Background**: Gray.
- **Input Field**: An entry widget at the top to display the current input and results. The input is displayed using a `StringVar`.
- **Buttons**: The calculator consists of buttons for digits (0-9), operations (+, -, *, /), clear (`C`), percentage (`%`), parentheses (`(` and `)`), and evaluate (`=`).

---

## Code Explanation

### 1. Class Definition: `Calculator`

The `Calculator` class contains the entire logic for the calculator, including:
- **`__init__(self, master)`**: This is the constructor method that initializes the GUI. It creates the input field and the buttons for digits and operations.
- **`show(self, value)`**: This method is called when a button is clicked. It appends the clicked value (digit or operator) to the current input (`entry_value`) and updates the display.
- **`clear(self)`**: Clears the input field by resetting `entry_value` to an empty string.
- **`solve(self)`**: This method is called when the "=" button is clicked. It evaluates the current input using Python’s `eval()` function and displays the result in the input field.

### 2. `__init__` Method
This method is responsible for setting up the calculator window, defining button actions, and configuring the entry widget to display the mathematical expression.

```python
def __init__(self, master):
    master.title("Calculator")
    master.geometry('357x420+0+0')
    master.config(bg='gray')
    master.resizable(False, False)
    
    self.equation = StringVar()  # Used to hold the current equation.
    self.entry_value = ''  # Stores the current expression input by the user.
    
    # Entry widget to display the equation or result.
    Entry(width=17, bg='#fff', font=('Arial Bold', 28), textvariable=self.equation).place(x=0, y=0)
    
    # Buttons for digits and operations (positioned using place)
    Button(width=11, height=4, text='(', relief='flat', bg='white', command=lambda: self.show('(')).place(x=0, y=50)
    Button(width=11, height=4, text=')', relief='flat', bg='white', command=lambda: self.show(')')).place(x=90, y=50)
    Button(width=11, height=4, text='%', relief='flat', bg='white', command=lambda: self.show('%')).place(x=180, y=50)
    
    Button(width=11, height=4, text='1', relief='flat', bg='white', command=lambda: self.show(1)).place(x=0, y=125)
    Button(width=11, height=4, text='2', relief='flat', bg='white', command=lambda: self.show(2)).place(x=90, y=125)
    Button(width=11, height=4, text='3', relief='flat', bg='white', command=lambda: self.show(3)).place(x=180, y=125)
    
    Button(width=11, height=4, text='4', relief='flat', bg='white', command=lambda: self.show(4)).place(x=0, y=200)
    Button(width=11, height=4, text='5', relief='flat', bg='white', command=lambda: self.show(5)).place(x=90, y=200)
    Button(width=11, height=4, text='6', relief='flat', bg='white', command=lambda: self.show(6)).place(x=180, y=200)
    
    Button(width=11, height=4, text='7', relief='flat', bg='white', command=lambda: self.show(7)).place(x=0, y=275)
    Button(width=11, height=4, text='8', relief='flat', bg='white', command=lambda: self.show(8)).place(x=180, y=275)
    Button(width=11, height=4, text='9', relief='flat', bg='white', command=lambda: self.show(9)).place(x=90, y=275)
    
    Button(width=11, height=4, text='0', relief='flat', bg='white', command=lambda: self.show(0)).place(x=90, y=350)
    
    # Operation buttons
    Button(width=11, height=4, text='+', relief='flat', bg='white', command=lambda: self.show('+')).place(x=180, y=350)
    Button(width=11, height=4, text='*', relief='flat', bg='white', command=lambda: self.show('*')).place(x=270, y=275)
    Button(width=11, height=4, text='-', relief='flat', bg='white', command=lambda: self.show('-')).place(x=270, y=200)
    Button(width=11, height=4, text='/', relief='flat', bg='white', command=lambda: self.show('/')).place(x=270, y=50)
    Button(width=11, height=4, text='x', relief='flat', bg='white', command=lambda: self.show('*')).place(x=270, y=125)
    
    # Control buttons
    Button(width=11, height=4, text='=', relief='flat', bg='white', command=self.solve).place(x=270, y=350)
    Button(width=11, height=4, text='C', relief='flat', command=self.clear).place(x=0, y=350)
```

### 3. `show(self, value)` Method
The `show` method appends the value (whether it's a number or an operator) to the `entry_value` string and updates the equation shown in the entry widget.

```python
def show(self, value):
    self.entry_value += str(value)
    self.equation.set(self.entry_value)  # Update the equation on the display.
```

### 4. `clear(self)` Method
The `clear` method resets the `entry_value` string to an empty value and clears the equation displayed in the input field.

```python
def clear(self):
    self.entry_value = ''  # Clear the current expression.
    self.equation.set(self.entry_value)  # Update the display.
```

### 5. `solve(self)` Method
The `solve` method evaluates the mathematical expression entered by the user using the `eval()` function and displays the result.

```python
def solve(self):
    try:
        result = eval(self.entry_value)  # Evaluate the entered expression.
        self.equation.set(result)  # Show the result in the display.
    except Exception as e:
        self.equation.set("Error")  # In case of any error (e.g., invalid expression).
```

---

## 6. Running the Application

1. To run the calculator, create an instance of the `Tk` root window and pass it to the `Calculator` class.
   
2. The application will launch with the calculator GUI. The user can click on the buttons to enter numbers and operations, clear the input, or evaluate the result.

```python
root = Tk()  # Create the main window
Calculator(root)  # Initialize the Calculator class with the window
root.mainloop()  # Start the Tkinter event loop
```

---

## 7. Enhancements and Future Work
- **Error Handling**: The program uses `eval()`, which can be risky if the input is not controlled. Adding more robust error handling and input validation can improve safety and reliability.
- **Advanced Features**: Implement additional features such as square roots, trigonometric functions, or memory functionalities.
- **Responsive Design**: Make the calculator more responsive to window resizing or adapt the layout for smaller screens.
