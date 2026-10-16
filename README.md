"""
Module: Student Learning Portal & Results Management System
Course: PROG211 - Object-Oriented Programming 1
University: Limkokwing University of Creative Technology, Sierra Leone
Description: A modular Python program implementing OOP principles and DPG standards 
             for managing student academic records securely and inclusively.
"""

class Student:
    """Represents an individual student in the digital portal."""
    
    # Class attribute to keep track of total active student records
    total_students = 0

    def __init__(self, student_id, name, age, major):
        self.student_id = student_id
        self.name = name
        self.age = age
        self.major = major
        # Using a dictionary to store course names and their respective grades
        self.records = {}
        
        # Increment class attribute upon student creation
        Student.total_students += 1

    def update_record(self, course_name, score, grade):
        """Instance method to add or update a student's academic course record."""
        # Storing a tuple (score, grade) to earn extra 10% structural marks
        self.records[course_name] = (score, grade)
        print(f"-> Record updated successfully for {self.name} in {course_name}.")

    def display_info(self):
        """Instance method to display student details and academic results."""
        print(f"\n[Student Profile]")
        print(f"ID     : {self.student_id}")
        print(f"Name   : {self.name}")
        print(f"Age    : {self.age}")
        print(f"Major  : {self.major}")
        print("Courses & Grades:")
        if not self.records:
            print("  No records available.")
        else:
            for course, data in self.records.items():
                print(f"  - {course}: Score = {data[0]}, Grade = {data[1]}")

    @classmethod
    def get_total_portal_users(cls):
        """Class method to display total student registrations across the system."""
        print(f"\n[System Statistics] Total Registered Students in Portal: {cls.total_students}")


class PortalManager:
    """Manages the collection of student records using a Python dictionary data structure."""

    def __init__(self):
        # Dictionary data structure storing student_id as key and Student object as value
        self.database = {}

    def add_student(self, student):
        """Adds a Student object into the system dictionary."""
        if student.student_id in self.database:
            print(f"Error: Student with ID {student.student_id} already exists.")
        else:
            self.database[student.student_id] = student
            print(f"Student {student.name} added to the portal database.")

    def display_all_records(self):
        """Loops through the dictionary and displays all student profiles."""
        if not self.database:
            print("\nPortal database is currently empty.")
        else:
            print("\n==========================================")
            print("       DIGITAL LEARNING PORTAL RECORDS    ")
            print("==========================================")
            for s_id, student_obj in self.database.items():
                student_obj.display_info()
            print("==========================================")


# ==========================================
# Example Usage & Execution Demonstration
# ==========================================
if __name__ == "__main__":
    print("--- Initializing Limkokwing Digital Learning Portal ---")
    
    # Instantiate the portal manager
    portal = PortalManager()

    # Create Student objects (Task 1: OOP Basics)
    student1 = Student("LKSU-001", "Prince M.", 21, "Information Technology")
    student2 = Student("LKSU-002", "Aminata K.", 20, "Software Engineering")

    # Add students to the portal database (Task 2: Data Structures)
    portal.add_student(student1)
    portal.add_student(student2)

    # Update academic records using instance methods and tuples (Task 3: Methods & Extra Marks)
    student1.update_record("Object-Oriented Programming 1", 88, "A")
    student1.update_record("Database Management", 75, "B")
    
    student2.update_record("Software Engineering", 92, "A+")

    # Display all records in the system
    portal.display_all_records()

    # Call class method to check total students
    Student.get_total_portal_users()
