import customtkinter as ctk
# Initialize the custom tkinter appearance
ctk.set_appearance_mode("System")  # Modes: "System", "Dark", "Light"
ctk.set_default_color_theme("blue")  # Themes: "blue", "green", "dark-blue"

# Global dictionary to store student data
students = {}

# Functions to manage the student data
def student_add(roll_no, name, marks):
    total = sum(marks)
    percentage = (total / 500) * 100
    grade = calculate_grade(total)
    students[roll_no] = {"name": name, "marks": marks, "total": total, "percentage": percentage, "grade": grade}
    update_student_list()

def update_stu(roll_no, name, marks):
    if roll_no in students:
        total = sum(marks)
        percentage = (total / 500) * 100
        grade = calculate_grade(total)
        students[roll_no] = {"name": name, "marks": marks, "total": total, "percentage": percentage, "grade": grade}
        update_student_list()
        result_label.configure(text=f"Student Roll No {roll_no} updated successfully.", text_color="green")
    else:
        result_label.configure(text=f"Roll No {roll_no} not found!", text_color="red")

def del_stu(roll_no):
    if roll_no in students:
        del students[roll_no]
        update_student_list()
        result_label.configure(text=f"Student Roll No {roll_no} deleted successfully.", text_color="green")
    else:
        result_label.configure(text=f"Roll No {roll_no} not found!", text_color="red")

def view_stu():
    if students:
        result_text = "\n".join(
            [f"Roll No: {roll_no}, Name: {data['name']}, Marks: {data['marks']}, Total: {data['total']}, Percentage: {data['percentage']:.2f}%, Grade: {data['grade']}" 
             for roll_no, data in students.items()]
        )
        display_window = ctk.CTkToplevel()
        display_window.title("View All Students")
        display_window.geometry("600x400")
        display_window.configure(bg="#f5f5f5")
        display_label = ctk.CTkLabel(display_window, text=result_text, justify="left", wraplength=550)
        display_label.pack(pady=20)
    else:
        result_label.configure(text="No students found.", text_color="red")

def search_student(roll_no_or_name):
    for roll_no, data in students.items():
        if roll_no == roll_no_or_name or data['name'].lower() == roll_no_or_name.lower():
            result_text = (f"Roll No: {roll_no}\n"
                           f"Name: {data['name']}\n"
                           f"Marks: {data['marks']}\n"
                           f"Total: {data['total']}\n"
                           f"Percentage: {data['percentage']:.2f}%\n"
                           f"Grade: {data['grade']}")
            search_result_label.configure(text=result_text, text_color="black")
            return
    search_result_label.configure(text="Student not found.", text_color="red")

def update_student_list():
    if students:
        result_text = "\n".join(
            [f"Roll No: {roll_no}, Name: {data['name']}, Total: {data['total']}, Percentage: {data['percentage']:.2f}%, Grade: {data['grade']}" 
             for roll_no, data in students.items()]
        )
        result_label.configure(text=result_text, text_color="black", wraplength=400)
    else:
        result_label.configure(text="No students found.", text_color="red")

def calculate_grade(total):
    if total >= 450:
        return "A"
    elif total >= 400:
        return "B"
    elif total >= 350:
        return "C"
    elif total >= 300:
        return "D"
    else:
        return "F"

# GUI Setup
root = ctk.CTk()
root.title("Students Result Management System")
root.geometry("600X700")
root.configure(bg="#e0f7fa")

header_label = ctk.CTkLabel(root, text="Students Result Management System\n By Roll No: 14 17 28 29", font=("Arial", 24, "bold"), text_color="#0d47a1")
header_label.pack(pady=20)

tab_view = ctk.CTkTabview(root, width=650, height=700)
tab_view.pack(pady=10, padx=20)

# Add tabs
manage_tab = tab_view.add("Manage Students")
search_tab = tab_view.add("Search Student")

# Manage Students Tab
details_frame = ctk.CTkFrame(manage_tab, width=650, height=350, corner_radius=10, fg_color="#ffffff")
details_frame.pack(pady=10, padx=20)

# Input fields for Manage Tab
roll_no_label = ctk.CTkLabel(details_frame, text="Enter Roll Number:", font=("Arial", 14))
roll_no_label.grid(row=0, column=0, padx=10, pady=10, sticky="w")

roll_no_entry = ctk.CTkEntry(details_frame, width=300)
roll_no_entry.grid(row=0, column=1, padx=10, pady=10)

name_label = ctk.CTkLabel(details_frame, text="Enter Student Name:", font=("Arial", 14))
name_label.grid(row=1, column=0, padx=10, pady=10, sticky="w")

name_entry = ctk.CTkEntry(details_frame, width=300)
name_entry.grid(row=1, column=1, padx=10, pady=10)

subject_names = ["English", "Applied Calculus", "Programming Fundamentals", "IICT", "Discrete Structures"]
marks_entries = []

for i, subject_name in enumerate(subject_names):
    subject_label = ctk.CTkLabel(details_frame, text=f"{subject_name} Marks:", font=("Arial", 14))
    subject_label.grid(row=i + 2, column=0, padx=10, pady=5, sticky="w")
    marks_entry = ctk.CTkEntry(details_frame, width=300)
    marks_entry.grid(row=i + 2, column=1, padx=10, pady=5)
    marks_entries.append(marks_entry)

# Button Functions
def add_student():
    roll_no = roll_no_entry.get()
    name = name_entry.get()
    try:
        marks = [int(entry.get()) for entry in marks_entries]
        if not roll_no or not name:
            result_label.configure(text="Roll Number and Name cannot be empty.", text_color="red")
            return
        if all(0 <= mark <= 100 for mark in marks):
            if roll_no not in students:
                student_add(roll_no, name, marks)
                result_label.configure(text=f"Student Roll No {roll_no} added successfully.", text_color="green")
                roll_no_entry.delete(0, 'end')
                name_entry.delete(0, 'end')
                for entry in marks_entries:
                    entry.delete(0, 'end')
            else:
                result_label.configure(text=f"Roll No {roll_no} already exists.", text_color="red")
        else:
            result_label.configure(text="Please enter valid marks (0-100).", text_color="red")
    except ValueError:
        result_label.configure(text="Please enter numeric values for marks.", text_color="red")

def update_student():
    roll_no = roll_no_entry.get()
    name = name_entry.get()
    try:
        marks = [int(entry.get()) for entry in marks_entries]
        if not roll_no or not name:
            result_label.configure(text="Roll Number and Name cannot be empty.", text_color="red")
            return
        if all(0 <= mark <= 100 for mark in marks):
            update_stu(roll_no, name, marks)
            roll_no_entry.delete(0, 'end')
            name_entry.delete(0, 'end')
            for entry in marks_entries:
                entry.delete(0, 'end')
        else:
            result_label.configure(text="Please enter valid marks (0-100).", text_color="red")
    except ValueError:
        result_label.configure(text="Please enter numeric values for marks.", text_color="red")

def delete_student():
    roll_no = roll_no_entry.get()
    if roll_no:
        del_stu(roll_no)
        roll_no_entry.delete(0, 'end')
        name_entry.delete(0, 'end')
        for entry in marks_entries:
            entry.delete(0, 'end')
    else:
        result_label.configure(text="Please enter a valid Roll Number.", text_color="red")

def view_all_students():
    view_stu()

# Buttons for Manage Tab
button_frame = ctk.CTkFrame(manage_tab, width=650, height=100, corner_radius=10, fg_color="#ffffff")
button_frame.pack(pady=20, padx=20)

add_button = ctk.CTkButton(button_frame, text="Add Student", command=add_student, width=150)
add_button.grid(row=0, column=0, padx=20, pady=10)

update_button = ctk.CTkButton(button_frame, text="Update Student", command=update_student, width=150)
update_button.grid(row=0, column=1, padx=20, pady=10)

delete_button = ctk.CTkButton(button_frame, text="Delete Student", command=delete_student, width=150)
delete_button.grid(row=0, column=2, padx=20, pady=10)

view_button = ctk.CTkButton(button_frame, text="View All Students", command=view_all_students, width=150)
view_button.grid(row=1, column=1, padx=20, pady=10)

result_label = ctk.CTkLabel(manage_tab, text="Welcome to the Students Result Management System!", font=("Arial", 14), text_color="#1b5e20", wraplength=600)
result_label.pack(pady=20)

# Search Tab
search_label = ctk.CTkLabel(search_tab, text="Search Student by Roll Number or Name", font=("Arial", 16, "bold"))
search_label.pack(pady=20)

search_entry = ctk.CTkEntry(search_tab, width=400, placeholder_text="Enter Roll Number or Name")
search_entry.pack(pady=10)

def search_student_handler():
    query = search_entry.get()
    if query:
        search_student(query)
    else:
        search_result_label.configure(text="Please enter a valid Roll Number or Name.", text_color="red")

search_button = ctk.CTkButton(search_tab, text="Search", command=search_student_handler)
search_button.pack(pady=10)

search_result_label = ctk.CTkLabel(search_tab, text="", font=("Arial", 14), wraplength=500)
search_result_label.pack(pady=20)

root.mainloop()
