# Use Case Diagram for Airbnb Clone Backend

This directory contains the use case diagram visualizing the interactions between actors (Guest User, Host, Admin, Payment Gateway, Notification System) and the Airbnb Clone backend system. The diagram captures key functionalities such as user registration, property management, booking, payments, and notifications, as outlined in the project features.

## Diagram Details
- **Actors**:
  - **Guest User**: A user who registers, logs in, manages their profile, searches properties, views property details, books properties, leaves reviews, and receives booking confirmations.
  - **Host**: A user who searches properties, views property details, books properties, leaves reviews, and receives booking confirmations.
  - **Admin**: A user who manages users, manages listings, and views reports.
  - **Payment Gateway**: An external system that handles make payment and refund payment actions.
  - **Notification System**: An external system that supports notification-related actions.
- **Use Cases** (within the "Airbnb System" boundary):
  - **Guest User**:
    - Register/Sign Up
    - Login/Logout
    - Manage Profile
    - Search Properties
    - View Property Details
    - Book Property
    - Leave Review
    - Receive Booking Confirmation
  - **Host**:
    - Search Properties
    - View Property Details
    - Book Property
    - Leave Review
    - Receive Booking Confirmation
  - **Admin**:
    - Manage Users
    - Manage Listings
    - View Reports
  - **Payment Gateway**:
    - Make Payment
    - Refund Payment
  - **Notification System**:
    - Notification System (implied interaction for notifications)
- **Interactions**:
  - Actors are connected to their respective use cases with lines.
  - The Payment Gateway interacts with "Make Payment" and "Refund Payment."
  - The Notification System interacts with "Receive Booking Confirmation" and other notification-related actions.

The diagram is `use-case-diagram.png`, stored in this directory.