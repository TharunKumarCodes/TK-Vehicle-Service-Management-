# 🚗 Vehicle Service Management Application

## 📌 Overview

The **Vehicle Service Management Application** is a Pega-based application designed to manage the complete vehicle service lifecycle, from submitting a service request to vehicle inspection, service estimate generation, customer approval, technician assignment, service execution, and service completion.

The application is built using **Pega App Studio** and **Pega Blueprint**, using Pega's low-code case management capabilities to automate the vehicle servicing process.

---

## 🎯 Objectives

The main objectives of this application are to:

* Allow customers to submit vehicle service requests.
* Capture and maintain vehicle-related information.
* Perform vehicle inspections through Service Advisors.
* Generate service estimates automatically.
* Calculate the total service cost.
* Allow customers to approve or reject service estimates.
* Automatically route service requests to appropriate work queues.
* Assign service requests to technicians.
* Track service execution and completion.
* Notify customers when the service is completed.
* Monitor service requests using SLA goals and deadlines.

---

## 🔄 Application Workflow

```text
Customer
   │
   ▼
Submit Vehicle Service Request
   │
   ▼
Inspection
   │
   ├── Perform Vehicle Inspection
   │
   └── Generate Service Estimate
   │
   ▼
Approval
   │
   ├── Review Service Estimate
   │
   ├── Approved ───────► Service Execution
   │
   └── Rejected ───────► Case Resolved
                             
Service Execution
   │
   ├── Automatic Vehicle-Type Routing
   │
   ├── Technician Assignment
   │
   └── Service Completion
          │
          ▼
   Customer Notification
          │
          ▼
       Case Resolved
```

---

## 🏗️ Main Case Type

### Vehicle Service Request

The **Vehicle Service Request** is the primary case type used to manage the complete service process.

The case captures the following information:

| Property            | Purpose                           |
| ------------------- | --------------------------------- |
| Vehicle ID          | Identifies the vehicle            |
| Vehicle Model       | Stores the vehicle model          |
| Vehicle Type        | Determines service routing        |
| Issue Description   | Describes the customer's issue    |
| Inspection Notes    | Stores inspection findings        |
| Condition Rating    | Records vehicle condition         |
| Labor Cost          | Stores labor estimate             |
| Parts Cost          | Stores parts estimate             |
| Total Cost          | Stores calculated service cost    |
| Approval Status     | Stores customer approval decision |
| Assigned Technician | Stores technician assignment      |
| Service Status      | Tracks service progress           |
| Service Summary     | Stores service completion details |

---

## 👥 Personas

### 👤 Customer

The Customer can:

* Submit a Vehicle Service Request.
* Enter vehicle information.
* Describe the vehicle issue.
* Review the service estimate.
* View Labor Cost, Parts Cost, and Total Cost.
* Approve or reject the estimate.
* Receive service completion notifications.

### 🧑‍💼 Service Advisor

The Service Advisor can:

* Perform vehicle inspections.
* Enter Inspection Notes.
* Enter Condition Rating.
* Generate service estimates.
* Enter Labor Cost.
* Enter Parts Cost.
* Review the calculated Total Cost.

### 🔧 Technician

The Technician can:

* Receive automatically assigned service requests.
* Perform vehicle service.
* Update Service Status.
* Maintain Assigned Technician information.
* Complete the service request.

---

## 📊 Vehicle Data Object

A reusable **Vehicle** data object is created to maintain vehicle information independently from the service request case.

### Vehicle Properties

| Property   | Description               |
| ---------- | ------------------------- |
| Vehicle ID | Unique vehicle identifier |
| Model      | Vehicle model             |
| Type       | Vehicle type              |

The Vehicle data object is associated with the **Vehicle Service Request** case and can be reused across multiple service requests.

This supports consistent vehicle information and service history tracking.

---

## 💰 Service Estimate

The Service Advisor enters:

* Labor Cost
* Parts Cost

The application automatically calculates:

```text
Total Cost = Labor Cost + Parts Cost
```

### Example

```text
Labor Cost = ₹5,000
Parts Cost = ₹3,000

Total Cost = ₹5,000 + ₹3,000
           = ₹8,000
```

The calculated Total Cost is stored in the case and displayed to the Customer during approval.

---

## ✅ Approval Process

The Customer reviews the service estimate before making a decision.

The approval screen displays:

* Labor Cost
* Parts Cost
* Total Cost

The Customer can select:

### Approved

The case proceeds to **Service Execution**.

### Rejected

The case is resolved with an appropriate rejected status and does not proceed to Service Execution.

---

## 🔀 Automatic Vehicle-Type Routing

The application automatically routes service requests based on the **Vehicle Type**.

### Heavy Vehicle

```text
Vehicle Type = Heavy
        │
        ▼
HeavyVehicleQueue
```

### Light / Other Vehicle

```text
Vehicle Type ≠ Heavy
        │
        ▼
LightVehicleQueue
```

This routing is implemented using appropriate Pega decision logic such as a **When rule or Decision Table**.

---

## 🔧 Service Execution

The **Service Execution** stage handles service fulfilment.

The system automatically routes the request to the appropriate technician work queue.

The following information is maintained:

* Assigned Technician
* Service Status
* Service Summary

The Technician updates the Service Status as the service progresses and completes the request after the service is finished.

---

## 🔔 Service Completion Notification

When the service request is completed and resolved, the system sends a correspondence/notification to the Customer.

The notification contains:

* Case ID
* Vehicle ID
* Vehicle Model
* Service Summary
* Total Cost

This ensures that the Customer receives confirmation and important service details.

---

## ⏱️ Service Level Agreement (SLA)

A simple SLA is configured for the **Vehicle Service Request** case.

| SLA      | Duration |
| -------- | -------: |
| Goal     |   2 Days |
| Deadline |   3 Days |

### Goal Breach

When the 2-day goal is missed, the case is flagged as approaching the deadline.

### Deadline Breach

When the 3-day deadline is missed, the case priority is automatically increased.

No complex escalation path is required.

---

## 🧩 Case Lifecycle

The complete case lifecycle is:

```text
Submit Vehicle Service Request
              ↓
          Inspection
              ↓
     Generate Service Estimate
              ↓
           Approval
          ↙        ↘
     Rejected      Approved
        ↓              ↓
   Case Resolved   Service Execution
                       ↓
              Technician Assignment
                       ↓
                Service Completion
                       ↓
              Customer Notification
                       ↓
                  Case Resolved
```

---

## 📋 Project Requirements

The application addresses the following requirements:

* [x] Submit Vehicle Service Request
* [x] Perform Vehicle Inspection
* [x] Generate Service Estimate
* [x] Approve Service Estimate
* [x] Maintain Vehicle Data
* [x] Review Service Estimate
* [x] Auto Assign Technician
* [x] Notify Service Completion
* [x] Define Service SLA
* [x] Route Service Request by Vehicle Type

---

## 🛠️ Technologies Used

* **Pega Platform**
* **Pega App Studio**
* **Pega Blueprint**
* **Pega Case Management**
* **Pega Data Objects**
* **Pega Personas**
* **Pega Business Rules**
* **Pega Approval Workflow**
* **Pega SLA**
* **Pega Correspondence**

---

## 📁 Repository Structure

```text
Vehicle-Service-Management/
│
├── README.md
├── PROJECT_DOCUMENTATION.md
├── USER_GUIDE.md
├── TEST_CASES.md
├── PROJECT_REPORT.md
│
└── screenshots/
    ├── blueprint.png
    ├── application.png
    ├── service-request.png
    ├── inspection.png
    ├── estimate.png
    ├── approval.png
    ├── service-execution.png
    └── completion.png
```

---

## 🎯 Expected Benefits

The application provides:

* Automated service request processing.
* Improved vehicle data consistency.
* Faster service request routing.
* Automatic cost calculation.
* Transparent estimate approval.
* Automated technician assignment.
* SLA-based service monitoring.
* Improved service tracking.
* Automated customer communication.
* Better overall service management.

---

## 🚀 Future Enhancements

The application can be enhanced in the future with:

* Online appointment scheduling.
* Payment integration.
* Service history dashboard.
* Customer feedback and ratings.
* Spare-parts inventory management.
* Automated service reminders.
* Technician performance dashboards.
* Mobile support for technicians.
* Advanced reporting and analytics.

---

## 🏁 Conclusion

The **Vehicle Service Management Application** demonstrates how Pega App Studio and Pega Blueprint can be used to automate a real-world business process.

The application provides an end-to-end workflow covering service request submission, vehicle inspection, estimate generation, customer approval, automatic technician routing, service execution, SLA management, and customer notification.

By combining case management, reusable data objects, business rules, routing, approval workflows, correspondence, and SLA capabilities, the application provides a structured and efficient solution for managing vehicle servicing operations.

---

## 👨‍💻 Project

**Project Name:** Vehicle Service Management Application
**Platform:** Pega Platform
**Development Tools:** Pega App Studio & Pega Blueprint
**Application Type:** Case Management / Workflow Automation
