# Student Management System Documentation

## Overview
This **Student Management System** is a desktop application built using Python's **Tkinter** library for the graphical user interface (GUI) and **SQLite** for storing student records in a relational database. The system allows users to manage student data with features such as adding, updating, deleting, and displaying student details like ID, name, age, date of birth (DOB), gender, and city.

---

## Features
- **Add New Student**: Insert new student details into the system and database.
- **Delete Student**: Remove a selected student's record from both the system and database.
- **Update Student**: Modify existing student details.
- **Clear Form**: Clear all input fields used for adding or editing student records.
- **Display Student Data**: Display the list of students in a table view, dynamically updated when records are added, updated, or deleted.
- **SQLite Database Integration**: The system uses an SQLite database to persist student records.

---

## 1. Project Structure

The project consists of two main components:
1. **Tkinter GUI**: Provides the interface for users to interact with the system.
   - **Main Frame (Frame_1)**: Contains input fields for student details and buttons for actions.
   - **Table Frame (Frame_2)**: Displays a table view (using Treeview) of all student records.
   
2. **SQLite Database**: Stores student information in a relational database.
   - A table named `Student` with columns for ID, Name, Age, DOB, Gender, and City.

---

## 2. GUI Design

### Title
The title of the application is displayed at the top with the label **"Student Management System"**.

### Form for Input
There are six input fields for entering student details:
- **ID**: Unique identifier for each student.
- **Name**: Name of the student.
- **Age**: Age of the student.
- **DOB**: Date of birth of the student.
- **Gender**: Gender of the student.
- **City**: City of residence of the student.

### Buttons
The system includes four main buttons:
- **Add**: Adds a new student record to the database and updates the table view.
- **Delete**: Deletes the selected student record from both the database and the table view.
- **Update**: Updates the selected student record in the database and the table view.
- **Clear**: Clears the input fields to reset the form.

### Treeview Table
The **Treeview** widget displays student records in a table format with the following columns:
- **ID**
- **Name**
- **Age**
- **DOB**
- **Gender**
- **City**

---

## 3. Database Schema

The **SQLite** database uses a table called `Student` with the following schema:

```sql
CREATE TABLE IF NOT EXISTS Student (
    ID INTEGER,
    NAME VARCHAR(20),
    AGE INTEGER,
    DOB VARCHAR(20),
    GENDER VARCHAR(20),
    CITY VARCHAR(20)
);
```

Columns:
- **ID (INTEGER)**: Unique identifier for each student.
- **NAME (VARCHAR(20))**: The student's name.
- **AGE (INTEGER)**: The student's age.
- **DOB (VARCHAR(20))**: The student's date of birth.
- **GENDER (VARCHAR(20))**: The student's gender.
- **CITY (VARCHAR(20))**: The student's city of residence.

---

## 4. Functions

### a. Add(self)

**Description**: Adds a new student record to the database and the table.

**Procedure**:
1. Retrieves the data entered in the input fields.
2. Inserts the data into the `Student` table in the SQLite database.
3. Updates the Treeview widget to display the newly added record.

```python
def Add(self):
    id = self.id_Entry.get()
    name = self.Name_Entry.get()
    age = self.Age_Entry.get()
    dob = self.DOB_Entry.get()
    gender = self.Gender_Entry.get()
    city = self.City_Entry.get()
    
    c = sqlite3.connect("Student.db")
    cursor = c.cursor()
    cursor.execute("INSERT INTO Student(ID, NAME, AGE, DOB, GENDER, CITY) VALUES(?,?,?,?,?,?)", 
                   (id, name, age, dob, gender, city))
    c.commit()
    c.close()
    
    self.tree.insert("", index=0, values=(id, name, age, dob, gender, city))
```

### b. Delete(self)

**Description**: Deletes a selected student from both the database and the Treeview.

**Procedure**:
1. Selects the student in the Treeview.
2. Deletes the corresponding record from the SQLite database.
3. Removes the record from the Treeview.

```python
def Delete(self):
    item = self.tree.selection()[0]
    selected_item = self.tree.item(item)['values'][0]
    
    c = sqlite3.connect("Student.db")
    cursor = c.cursor()
    cursor.execute("DELETE FROM Student WHERE ID=?", (selected_item,))
    c.commit()
    c.close()
    
    self.tree.delete(item)
```

### c. Update(self)

**Description**: Updates the details of a selected student in both the database and the Treeview.

**Procedure**:
1. Selects the student in the Treeview.
2. Retrieves the updated data from the input fields.
3. Updates the record in the SQLite database.
4. Updates the record in the Treeview widget.

```python
def Update(self):
    id = self.id_Entry.get()
    name = self.Name_Entry.get()
    age = self.Age_Entry.get()
    dob = self.DOB_Entry.get()
    gender = self.Gender_Entry.get()
    city = self.City_Entry.get()
    
    item = self.tree.selection()[0]
    selected_item = self.tree.item(item)['values'][0]
    
    c = sqlite3.connect("Student.db")
    cursor = c.cursor()
    cursor.execute("UPDATE Student SET ID=?, NAME=?, AGE=?, DOB=?, GENDER=?, CITY=? WHERE ID=?", 
                   (id, name, age, dob, gender, city, selected_item))
    c.commit()
    c.close()
    
    self.tree.item(item, values=(id, name, age, dob, gender, city))
```

### d. Clear(self)

**Description**: Clears all input fields for a fresh entry or edit.

```python
def Clear(self):
    self.id_Entry.delete(0, END)
    self.Name_Entry.delete(0, END)
    self.Age_Entry.delete(0, END)
    self.DOB_Entry.delete(0, END)
    self.Gender_Entry.delete(0, END)
    self.City_Entry.delete(0, END)
```

---

## 5. Running the Application

### Database Initialization:
Before running the application, ensure that the SQLite database and the `Student` table exist. If not, uncomment and run the provided database creation code to initialize the database.

### Launching the App:
1. Run the Python script to launch the Tkinter GUI.
2. The application window will open, displaying input fields and buttons to manage student records.

---

## 6. Enhancements and Future Work

- **Search Feature**: Implement a search function to allow users to find students by ID, name, or other attributes.
- **Error Handling**: Improve the application by adding error handling for invalid inputs (e.g., non-numeric values for age or missing fields).
- **Data Validation**: Ensure data is consistent before insertion into the database (e.g., checking that the age is a valid integer).
- **Database Optimization**: Consider indexing the `ID` column for faster queries when dealing with a large number of records.

---

## Conclusion

This **Student Management System** is a simple yet functional application that provides basic CRUD operations for managing student records. Built using Python's Tkinter and SQLite, it allows users to efficiently manage student data with a straightforward interface. The system is extensible and can be enhanced with additional features such as search, validation, and error handling for improved functionality.
