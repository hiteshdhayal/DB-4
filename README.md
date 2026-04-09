# Event Parking Management System (Database Design)

## Overview

Large events such as **Comic-Con India** attract thousands of visitors who arrive using different types of vehicles including bikes, cars, SUVs, cabs, and electric vehicles. Managing parking for such events requires an organized system that can track vehicles, allocate parking spots, monitor entry and exit times, and handle payments.

This project focuses on designing a **database architecture for a multi-zone event parking system**. The system models vehicles, parking zones, parking spots, tickets, parking sessions, payments, and EV charging infrastructure.

The goal of this design is to support a **realistic event parking environment** where multiple visitors arrive across several days and parking spots are reused over time.

---

# System Features

The database design supports the following capabilities:

* Vehicle registration and tracking
* Multiple vehicle categories (bike, car, SUV, cab, EV)
* Reserved parking categories (VIP, staff, exhibitors, etc.)
* Multi-zone and multi-level parking areas
* Automatic parking spot allocation
* Parking ticket generation
* Entry and exit tracking
* Parking fee calculation
* Payment recording
* EV charging infrastructure
* Tracking currently parked vehicles
* Multiple visits from the same vehicle across different days

---

# Database Structure

The system consists of several interconnected entities that represent the real-world parking operations.

## Core Entities

### Vehicle

Stores information about vehicles entering the parking facility.

**Key Attributes**

* vehicle_id (Primary Key)
* license_plate
* vehicle_category_id
* access_category_id
* manufacturer
* model
* color
* is_ev

---

### Vehicle Category

Defines the type of vehicle.

Examples include:

* Bike
* Car
* SUV
* Cab
* Electric Vehicle

---

### Access Category

Represents special access permissions for vehicles.

Examples include:

* VIP
* Exhibitor
* Staff
* General Visitor

This allows the system to assign **reserved parking spots** when required.

---

### Parking Zone

The venue parking area is divided into zones and levels.

Example zones:

* Zone A – Ground Level
* Zone B – Basement
* VIP Parking Zone
* EV Charging Zone

Each zone contains multiple parking spots.

---

### Spot Category

Defines different types of parking spots.

Examples include:

* Regular parking
* VIP reserved parking
* Staff parking
* EV charging spots

---

### Parking Spot

Represents an individual parking slot within a zone.

Each parking spot belongs to a zone and has a specific category.

Attributes include:

* spot number
* zone location
* spot size
* availability status
* EV charging capability

---

### Parking Session

A parking session begins when a vehicle enters the facility and ends when the vehicle exits.

This table records:

* entry time
* exit time
* parking spot used
* session status

A single vehicle can have **multiple parking sessions** across different days.

---

### Parking Ticket

When a vehicle enters the facility, the system generates a parking ticket.

The ticket stores:

* ticket number
* session reference
* issue time
* ticket status

This ticket is used when exiting the parking area.

---

### Parking Rate

Parking prices can vary depending on:

* vehicle type
* parking spot category

For example:

| Vehicle | Spot Type     | Price/Hour |
| ------- | ------------- | ---------- |
| Car     | Regular       | ₹50        |
| SUV     | Regular       | ₹70        |
| EV      | Charging Spot | ₹30        |

---

### Payment

When a vehicle exits the parking facility, the system calculates the parking charges and records the payment.

Payment records store:

* amount paid
* payment method (UPI, card, cash)
* transaction reference
* payment status
* payment time

---

### EV Charging Station

Some parking spots contain electric vehicle charging stations.

This entity stores information about the charging hardware.

Attributes include:

* charger type
* power capacity (kW)
* connector type
* charging status

---

### EV Charging Session

When an EV connects to a charging station, a charging session is recorded.

Information stored includes:

* charging start time
* charging end time
* energy consumed (kWh)
* charging cost

---

# System Workflow

The system operates in the following sequence:

### 1. Vehicle Entry

When a vehicle enters the venue parking facility:

1. The system identifies the vehicle.
2. A suitable parking spot is assigned based on availability and vehicle type.
3. A parking session is created.
4. A parking ticket is issued.

---

### 2. Parking Spot Allocation

The system checks:

* vehicle category
* reserved spot availability
* zone capacity

Then assigns an available parking spot.

---

### 3. Optional EV Charging

If the vehicle is an electric vehicle and the parking spot supports charging:

* the vehicle may connect to an EV charging station
* an EV charging session is recorded

---

### 4. Parking Duration Tracking

During the parking session, the system tracks:

* entry time
* duration
* parking spot occupancy

---

### 5. Vehicle Exit

When the vehicle leaves:

1. Exit time is recorded.
2. Parking duration is calculated.
3. Parking fees are calculated based on the rate rules.

---

### 6. Payment Processing

The system records payment details including:

* payment amount
* payment method
* transaction reference
* payment timestamp

---

# Key Design Advantages

This database design ensures:

* scalable multi-zone parking management
* support for different vehicle types
* reusable parking spots across sessions
* reserved parking categories
* EV charging support
* detailed payment tracking
* real-time monitoring of parked vehicles

---

# Use Cases

This database design can be used for:

* convention centers
* large event venues
* stadium parking systems
* mall parking infrastructure
* smart city parking management

---

# Technologies Used

* SQL (PostgreSQL compatible syntax)
* ER Modeling
* Database Normalization
* Relational Database Design

---

# Conclusion

This project demonstrates how a structured database design can efficiently manage a **large-scale event parking system**. By separating vehicles, parking spots, sessions, tickets, payments, and EV charging infrastructure into dedicated entities, the system remains scalable, maintainable, and capable of handling real-world event traffic.

The design also supports future enhancements such as:

* automated parking spot recommendation
* mobile ticketing systems
* real-time parking dashboards
* smart parking analytics

---

# Author

Hitesh Dhayal
Database Design Project – Event Parking Management System
