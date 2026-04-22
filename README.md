# metro-booking-system-
A Python Tkinter-based desktop application for metro ticket booking. The system enables users to select stations, ticket quantity, and optional cab service, with automated fare calculation and a detailed bill summary.
This project was developed as part of a college assignment to demonstrate practical skills in Python programming and GUI development. It is a Metro Ticket Booking System built using the Tkinter library, showcasing the ability to design interactive user interfaces, handle user input, perform validations, and implement fare calculation logic. By publishing it here, I aim to highlight my proficiency in Python, problem-solving, and application development, while also maintaining a portfolio of academic and personal projects.

This way, it looks professional, acknowledges the college context, and still positions you as someone with real skills.
# Metro Ticket Booking GUI

A Python Tkinter-based desktop application for metro ticket booking.  
The system enables users to select stations, ticket quantity, and optional cab service, with automated fare calculation and a detailed bill summary.

## 🚀 Features
- User-friendly GUI built with **Tkinter**
- Select **FromStation** and **ToStation**
- Choose number of **tickets**
- Optional **cab service** with drop location entry
- Automated **fare calculation**:
  - Metro fare: ₹40 per ticket
  - Cab fare: ₹150 (if selected)
- Error handling for invalid inputs (e.g., same station selection)
- Detailed bill displayed via **messagebox**

## 🛠️ Tech Stack
- **Python 3.x**
- **Tkinter** (standard GUI library in Python)
from tkinter import *
from tkinter import messagebox

a = Tk()
a.title("Metro Ticket Booking")

# Title
Label(a, text="Metro Ticket Booking", font=("Arial Bold", 20)).grid(column=1, row=0)

# Name
Label(a, text="Name", font=("Arial Bold", 15)).grid(column=0, row=1)
e1 = Entry(a, width=20)
e1.grid(column=1, row=1)

# From and To Stations
Label(a, text="FromStation", font=("Arial Bold", 15)).grid(column=0, row=2)
Label(a, text="ToStation", font=("Arial Bold", 15)).grid(column=0, row=3)

stations = ["LBNagar", "KPHB", "Nagole"]
v1 = StringVar(value="select")
OptionMenu(a, v1, *stations).grid(column=1, row=2)

v2 = StringVar(value="select")
OptionMenu(a, v2, *stations).grid(column=1, row=3)

# Tickets
Label(a, text="Tickets", font=("Arial Bold", 15)).grid(column=0, row=4)
ticket = [1, 2, 3, 4, 5]
v3 = IntVar(value=1)
OptionMenu(a, v3, *ticket).grid(column=1, row=4)

# Cab Option
Label(a, text="Do You Need a cab?", font=("Arial Bold", 15)).grid(column=0, row=5)
cab_choice = StringVar(value="No")

def toggle_cab():
    if cab_choice.get() == "Yes":
        Label(a, text="Drop Location", font=("Arial Bold", 15)).grid(column=0, row=6)
        global e2
        e2 = Entry(a, width=20)
        e2.grid(column=1, row=6)

Radiobutton(a, text="Yes", variable=cab_choice, value="Yes", command=toggle_cab).grid(column=1, row=5)
Radiobutton(a, text="No", variable=cab_choice, value="No").grid(column=2, row=5)

# Booking Logic
def book():
    name = e1.get()
    f = v1.get()
    to = v2.get()
    tickets = int(v3.get())
    total = tickets * 40

    if f == to:
        messagebox.showerror("Error", "Please select different stations")
        return

    if cab_choice.get() == "Yes":
        cbill = 150
        drop = e2.get()
        finalbill = total + cbill
        messagebox.showinfo("Booking Details",
                            f"Name: {name}\n"
                            f"Metro Bill: {f} → {to}\nTickets: {tickets}\nMetro Fare: ₹{total}\n\n"
                            f"Cab Bill: {to} → {drop}\nCab Fare: ₹{cbill}\n\n"
                            f"Final Bill: ₹{finalbill}")
    else:
        messagebox.showinfo("Booking Details",
                            f"Name: {name}\n"
                            f"Metro Bill: {f} → {to}\nTickets: {tickets}\nMetro Fare: ₹{total}")

# Book Button
Button(a, text="Book", command=book).grid(column=1, row=7)

a.mainloop()


## 📂 Project Structure

