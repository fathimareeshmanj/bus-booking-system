# bus-booking-system

**Project Overview**

The Bus Booking System is a console-based Python application developed using Object-Oriented Programming (OOP) concepts.
The system allows users to view available buses, book tickets, cancel bookings, and check passenger details while automatically managing seat availability.

 Objectives of the Project

To simulate a real-world bus reservation system

To understand and apply OOP concepts in Python

To manage bookings using in-memory data structures

To ensure seat availability is updated dynamically

 Technologies Used

Programming Language: Python

Concepts:

Classes & Objects

Dictionaries & Lists

Conditional Statements

Loops

Functions

🔹 System Design

The system is built around a Bus class, where each bus is treated as an object with its own data and behavior.

Key Attributes:

bus_number – Unique bus identifier

source – Starting city

destination – Ending city

total_seats – Total seat capacity

available_seats – Seats currently available

passenger_list – Stores passenger names and seats booked

🔹 Functionalities Implemented
1️⃣ View Available Buses

Displays:

Bus number

Route (source → destination)

Available seats

2️⃣ Ticket Booking

User selects a bus

Enters passenger name and number of seats

System checks seat availability

Seats are deducted after successful booking

✔ Prevents overbooking

3️⃣ Ticket Cancellation

User enters bus number and passenger name

Booking is removed

Seats are restored to availability

4️⃣ View Bookings

Displays all passengers booked for a selected bus

Shows number of seats booked per passenger

5️⃣ Exit System

Terminates the program safely

🔹 Data Handling

Uses dictionary to store passenger bookings:

{"Asha": 2, "Rahul": 1}

Uses list to store multiple bus objects

🔹 Key Programming Concepts Demonstrated

✔ Object-Oriented Programming
✔ Real-time data updates
✔ Menu-driven application
✔ Error handling through condition checks
✔ Code reusability using class methods

🔹 Limitations

Data is not stored permanently (lost after program exits)

No seat-number allocation

No authentication or payment feature

🔹 Future Enhancements

Integrate database (MySQL / SQLite)

Add ticket pricing and payment system

Assign specific seat numbers

Build GUI using Tkinter

Convert into web application using Flask or Django

🔹 Conclusion

This Bus Booking System demonstrates how Python can be used to design a simple yet effective reservation system using OOP principles.




class Bus:
    def __init__(self, bus_number, source, destination, total_seats):
        self.bus_number = bus_number
        self.source = source
        self.destination = destination
        self.total_seats = total_seats
        self.available_seats = total_seats
        self.passenger_list = {}

    def display_info(self):
        """Display bus details."""
        print(f"\nBus No: {self.bus_number}")
        print(f"Route: {self.source} → {self.destination}")
        print(f"Available Seats: {self.available_seats}/{self.total_seats}")

    def book_ticket(self, passenger_name, seats):
        """Book seats for a passenger."""
        if seats > self.available_seats:
            print(f"Only {self.available_seats} seats available. Booking failed!")
        else:
            self.available_seats -= seats
            self.passenger_list[passenger_name] = seats
            print(f"Booking confirmed for {passenger_name}. Seats booked: {seats}")

    def cancel_ticket(self, passenger_name):
        """Cancel a booking."""
        if passenger_name in self.passenger_list:
            seats_to_refund = self.passenger_list.pop(passenger_name)
            self.available_seats += seats_to_refund
            print(f"Booking canceled for {passenger_name}. Seats released: {seats_to_refund}")
        else:
            print(f"No booking found for {passenger_name}.")

    def display_bookings(self):
        """Display all bookings."""
        if not self.passenger_list:
            print("No bookings yet.")
        else:
            print("\nCurrent Bookings:")
            for passenger, seats in self.passenger_list.items():
                print(f"{passenger} - {seats} seat(s)")

# Creating instances of buses
bus1 = Bus("A101", "City A", "City B", 40)
bus2 = Bus("B202", "City X", "City Y", 30)

# Storing buses in a list
buses = [bus1, bus2]

# Function to display all available buses
def show_all_buses():
    print("\nAvailable Buses:")
    for bus in buses:
        bus.display_info()

# Main program loop
while True:
    print("\nBus Booking System")
    print("1. View Buses")
    print("2. Book Ticket")
    print("3. Cancel Ticket")
    print("4. View Bookings")
    print("5. Exit")
    
    choice = input("Enter your choice: ")

    if choice == "1":
        show_all_buses()

    elif choice == "2":
        bus_no = input("Enter Bus Number: ")
        selected_bus = next((bus for bus in buses if bus.bus_number == bus_no), None)
        if selected_bus:
            name = input("Enter Passenger Name: ")
            seats = int(input("Enter Number of Seats: "))
            selected_bus.book_ticket(name, seats)
        else:
            print("Invalid Bus Number.")

    elif choice == "3":
        bus_no = input("Enter Bus Number: ")
        selected_bus = next((bus for bus in buses if bus.bus_number == bus_no), None)
        if selected_bus:
            name = input("Enter Passenger Name: ")
            selected_bus.cancel_ticket(name)
        else:
            print("Invalid Bus Number.")

    elif choice == "4":
        bus_no = input("Enter Bus Number: ")
        selected_bus = next((bus for bus in buses if bus.bus_number == bus_no), None)
        if selected_bus:
            selected_bus.display_bookings()
        else:
            print("Invalid Bus Number.")

    elif choice == "5":
        print("Exiting system...")
        break
    else:
        print("Invalid choice! Please enter a valid option.")
The project improves understanding of real-world application logic, data management, and user interaction through a menu-driven interface.





