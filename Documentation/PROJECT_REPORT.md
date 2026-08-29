# Vehicle Service Management Application

## Project Report

## 1. Title

**Vehicle Service Management Application**

## 2. Introduction

The Vehicle Service Management Application is a workflow-based application developed using Pega App Studio and Pega Blueprint.

The application manages vehicle service requests from initial customer submission through inspection, estimate generation, approval, technician assignment, service execution, and final completion.

The project demonstrates how Pega Platform can be used to automate business processes and provide a structured case management solution.

## 3. Problem Statement

Vehicle servicing involves several activities performed by different users. Without an automated system, service requests can be difficult to track and may require manual coordination between customers, service advisors, and technicians.

The application is designed to solve these challenges by providing an automated service management workflow.

## 4. Project Objectives

The objectives are:

* Automate vehicle service request submission.
* Maintain reusable vehicle information.
* Record vehicle inspection findings.
* Generate service estimates.
* Calculate total service costs automatically.
* Obtain customer approval.
* Automatically assign service requests.
* Route requests based on vehicle type.
* Track service execution.
* Enforce service SLAs.
* Notify customers after service completion.

## 5. System Users

The application supports three main personas.

### Customer

The Customer submits service requests and approves or rejects service estimates.

### Service Advisor

The Service Advisor performs vehicle inspections and prepares service estimates.

### Technician

The Technician performs the actual vehicle service and updates the service status.

## 6. Application Workflow

The application follows this workflow:

```text
Submit Request
      ↓
Inspection
      ↓
Generate Estimate
      ↓
Customer Approval
      ↓
Service Execution
      ↓
Service Completion
      ↓
Customer Notification
      ↓
Resolution
```

## 7. Functional Requirements

### Requirement 1: Submit Vehicle Service Request

The Customer must be able to submit a service request containing vehicle and issue information.

### Requirement 2: Perform Vehicle Inspection

The Service Advisor must record inspection notes and condition rating.

### Requirement 3: Generate Service Estimate

Labor Cost and Parts Cost must be captured and Total Cost must be calculated automatically.

### Requirement 4: Approve Service Estimate

The Customer must approve or reject the estimate.

### Requirement 5: Maintain Vehicle Data

Vehicle information must be maintained in a reusable Vehicle data object.

### Requirement 6: Review Service Estimate

The Customer must be able to view Labor Cost, Parts Cost, and Total Cost before making a decision.

### Requirement 7: Auto Assign Technician

Approved service requests must be automatically routed to a Technician or technician work queue.

### Requirement 8: Notify Service Completion

The Customer must receive a completion notification when the service request is resolved.

### Requirement 9: Define Service SLA

The application must have:

* Goal: 2 days
* Deadline: 3 days

### Requirement 10: Route by Vehicle Type

Heavy vehicles must be routed to HeavyVehicleQueue.

Light and other vehicles must be routed to LightVehicleQueue.

## 8. Data Management

The reusable Vehicle data object contains:

* Vehicle ID
* Model
* Type

This allows vehicle information to be reused across multiple service requests.

## 9. Cost Calculation

The application uses the following calculation:

```text
Total Cost = Labor Cost + Parts Cost
```

This reduces manual calculation errors and provides an accurate estimate to the customer.

## 10. Approval Logic

The approval process uses the following logic:

```text
Customer Decision
       |
       +---- Approved ----> Service Execution
       |
       +---- Rejected -----> Resolve Case
```

## 11. Routing Logic

The routing rule is:

```text
IF Vehicle Type = Heavy
    Route to HeavyVehicleQueue
ELSE
    Route to LightVehicleQueue
```

This allows the application to automatically direct service requests to the appropriate work queue.

## 12. SLA Management

The application uses a simple SLA.

### Goal

The goal is **2 days** from case creation.

If the goal is missed, the case is flagged as approaching the deadline.

### Deadline

The deadline is **3 days** from case creation.

If the deadline is missed, the case priority is automatically increased.

## 13. Customer Notification

After service completion, the system sends correspondence to the Customer.

The notification contains:

* Case ID
* Vehicle ID
* Vehicle Model
* Service Summary
* Total Cost

## 14. Benefits

The application provides several benefits:

* Reduces manual processing.
* Improves service request tracking.
* Provides consistent vehicle data.
* Automates estimate calculations.
* Improves customer transparency.
* Automates technician routing.
* Provides SLA monitoring.
* Improves customer communication.
* Provides a complete view of the service lifecycle.

## 15. Testing

The application should be tested using positive and negative scenarios.

Important scenarios include:

* Valid service request submission.
* Missing required fields.
* Mandatory inspection validation.
* Correct Total Cost calculation.
* Customer approval.
* Customer rejection.
* Heavy vehicle routing.
* Light vehicle routing.
* Technician assignment.
* Completion notification.
* SLA goal breach.
* SLA deadline breach.

## 16. Expected Outcome

The expected outcome is a functional Pega Vehicle Service Management Application that manages the complete service request lifecycle.

The application should allow customers to submit requests, service advisors to inspect vehicles and generate estimates, customers to approve estimates, technicians to execute services, and the system to automatically route, track, and notify users.

## 17. Conclusion

The Vehicle Service Management Application successfully demonstrates the use of Pega Platform for automating a real-world vehicle servicing process.

The application integrates case management, personas, reusable data objects, calculated fields, approval workflows, automatic routing, correspondence, and SLA management into a single solution.

By automating the service lifecycle, the application improves process efficiency, data consistency, service visibility, and customer experience.

The project demonstrates how low-code Pega capabilities can be used to transform a manual business process into an organized and automated digital workflow.
