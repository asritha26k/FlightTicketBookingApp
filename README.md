# FlightTicketBookingApp

This repository contains links to the **frontend** and **backend** repositories
for the Flight Ticket Booking Application, along with the project report
submitted as part of an assignment.

##  Related Repositories

- **Frontend:**  
  https://github.com/asritha26k/frontend-for-flight-booking-app

- **Backend:**  
  https://github.com/asritha26k/backend-flight-booking-app

  #  Flight Ticket Booking Application

---



##  Password Change Policy

### Change password initiated after every 90 days  
(Tested with **15 minutes** for validation)
<img width="845" height="387" alt="image" src="https://github.com/user-attachments/assets/a945f461-cea3-4229-98e1-19fe2a0094a0" />

---

###  Case: Old password is incorrect
<img width="837" height="386" alt="image" src="https://github.com/user-attachments/assets/32fa5e52-12fa-4f76-bdf0-79c7cff17c6a" />

---

###  Case: Old password and New password are similar
<img width="846" height="392" alt="image" src="https://github.com/user-attachments/assets/64e72a52-502b-4f63-9e44-c2ca0ac5cacf" />

---

###  After successful password change
- User is redirected to **Sign In again**
<img width="850" height="392" alt="image" src="https://github.com/user-attachments/assets/c379b8a0-5918-4b17-b0ce-5eef764ddd08" />

---

##  Manual Change Password Feature if user wishes to change
### If user wishes to change password:

- Applicable for **Admin** and **User** roles
- Available **after sign-in**



<img width="846" height="395" alt="image" src="https://github.com/user-attachments/assets/b4b51648-5381-442f-82ae-b82c0e100722" />
<img width="845" height="392" alt="image" src="https://github.com/user-attachments/assets/9863d74c-ba29-4548-bd8a-7ed2445a6a48" />
<img width="847" height="385" alt="image" src="https://github.com/user-attachments/assets/ec6b0e6b-ee33-4b5c-af5e-c0839d797db0" />

---




##  Schema Changes

### User Class – Newly Added Fields

- `password_last_changed` → `LocalDateTime`
- `force_password_change` → `boolean`
<img width="838" height="592" alt="image" src="https://github.com/user-attachments/assets/3cba0911-430e-480d-979f-e8ebce02aaa3" />

---

##  APIs
### Change Password API

http://localhost:8765/auth-service/api/auth/change-password
Password changed successfully (200 ok)
Error: Old password is incorrect (400 Bad Request)



http://localhost:8765/auth-service/api/auth/signin
Sign in api:
After 90 days response
{
    "status": "PASSWORD_EXPIRED",
    "message": "Please change your password",
    "forcePasswordChange": true
}
---

## Admin: 
-Role based access control

.pathMatchers("/flight-service/flight/register").hasRole("ADMIN")

## In API GATEWAY
### Backend handling:

<img width="888" height="391" alt="image" src="https://github.com/user-attachments/assets/b6d67036-5681-4c20-a2d6-b6391890635c" />

### Frontend handling:
With the api:

/auth-service/api/auth/me


<img width="918" height="457" alt="image" src="https://github.com/user-attachments/assets/348e67f4-b7d9-4f3d-bfc8-47009af60b6e" />
<img width="911" height="266" alt="image" src="https://github.com/user-attachments/assets/c49cea1a-753a-4e19-9d32-e47b8b5ef4c7" />


## Flight Inventory feature:
<img width="848" height="396" alt="image" src="https://github.com/user-attachments/assets/05ea29c9-f9e6-4c7d-b264-8d207c31e89a" />

### Add flights here:
<img width="852" height="395" alt="image" src="https://github.com/user-attachments/assets/9e8caca4-b5fc-4c0e-84fd-25f9e5a3e0b1" />

##  Validations

| Field / Feature      | Purpose                          | Validations Applied                                   |
|----------------------|----------------------------------|-------------------------------------------------------|
| Airline              | Selects the airline for the flight | Required field                                        |
| Origin               | Departure city                   | Required, only alphabets and spaces allowed (`^[A-Za-z ]+$`) |
| Destination          | Arrival city                     | Required, only alphabets and spaces allowed (`^[A-Za-z ]+$`) |
| Price                | Ticket price of the flight       | Required, numeric values only (`^[0-9]+$`)            |
| Departure Date       | Flight departure date            | Required                                              |
| Departure Time       | Flight departure time            | Required                                              |
| Arrival Date         | Flight arrival date              | Required                                              |
| Arrival Time         | Flight arrival time              | Required                                              |
| Total Seats          | Total seat capacity of the flight| Required                                              |
| Min Date Constraint  | Prevents selecting past dates    | Minimum date set to current date                      |
| Flight Registration  | Adds a new flight                | Form must be valid before submission                  |
| Flight Listing       | Displays all flights             | Auto-refresh using `BehaviorSubject`                  |
| Flight Deletion      | Deletes a selected flight        | Requires valid flight ID & confirmation               |
| Auto Refresh         | Updates UI after add/delete      | Uses `BehaviorSubject + switchMap`                    |

<img width="846" height="389" alt="image" src="https://github.com/user-attachments/assets/335a500a-5152-4081-b747-5114f22bb988" />


## Drop down for Different airlines selection:

<img width="851" height="363" alt="image" src="https://github.com/user-attachments/assets/5034b9e3-8df3-4b7c-bac1-b9aff45d380f" />

### Flights shown after adding with delete button.
<img width="851" height="406" alt="image" src="https://github.com/user-attachments/assets/81bdca47-4961-48b4-b46f-751048ab874d" />

## Modal card to delete a flight:

<img width="850" height="380" alt="image" src="https://github.com/user-attachments/assets/9749c833-2f62-463e-9d7b-997272f09fec" />
##  Optimized Docker File

## Example: Flight Service

```dockerfile
FROM eclipse-temurin:17-jdk

WORKDIR /app

COPY target/*.jar flight-service.jar

EXPOSE 9002

ENTRYPOINT ["java", "-jar", "flight-service.jar"]

---


##  start-service.cmd

```cmd
java -jar service-registry\target\service-registry-0.0.1-SNAPSHOT.jar
java -jar ConfigServer\target\ConfigServer-0.0.1-SNAPSHOT.jar
java -jar api-gateway\target\api-gateway-0.0.1-SNAPSHOT.jar
java -jar auth-service\target\spring-security-own-0.0.1-SNAPSHOT.jar
java -jar flight-service\target\flight-service-0.0.1-SNAPSHOT.jar
java -jar passenger-service\target\passenger-service-0.0.1-SNAPSHOT.jar
java -jar ticket-service\target\ticket-service-0.0.1-SNAPSHOT.jar
java -jar email-service\target\email-service-0.0.1-SNAPSHOT.jar



---


##  Property Files

- 2 property files maintained**
  - For Docker
  - For Local
<img width="865" height="377" alt="image" src="https://github.com/user-attachments/assets/d7be0d70-bec5-41fe-96a9-0855fd39feed" />





##  Docker Profile Configuration

### application-docker.properties

- Used specifically for Docker environment
- Activated using Spring profile `docker`

---

### docker-compose.yml – Using Docker Profile

```yml
flight-service:
  build: ./flight-service
  container_name: flight-service
  ports:
    - "9002:9002"
  environment:
    SPRING_PROFILES_ACTIVE: docker
  depends_on:
    eureka-server:
      condition: service_healthy
    config-server:
      condition: service_healthy
    postgres-flight:
      condition: service_started
  networks:
    - app-net

---

##  SWOT Analysis – Flight Ticket Booking Application

###  Strengths
- Microservices-based architecture (Eureka, Config Server, API Gateway)
- Secure authentication using Spring Security + JWT
- Clear separation of services (Auth, Flight, Passenger, Ticket, Email)
- Admin features for adding and managing flights

---

###  Weaknesses
- Limited frontend features and UI polish
- No real payment gateway integration
- Basic error handling and validation
- High dependency on multiple services running together

---

###  Opportunities
- Integration of payment gateways (Razorpay/Stripe)
- Seat locking and dynamic pricing
- Real-time notifications using WebSockets
- Docker + Kubernetes deployment
- Advanced search, filters, and recommendations

---

###  Threats
- System failure if a critical microservice goes down
- Security risks if JWT handling is misconfigured
- Performance issues under high traffic
- Data inconsistency in distributed services





  
