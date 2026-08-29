# Vehicle Service Management Application

## Overview

The **Vehicle Service Management Application** is a Pega-based application designed to manage the complete vehicle service process, from submitting a service request to vehicle inspection, service estimate generation, customer approval, technician assignment, service execution, and service completion notification.

The application is developed using **Pega App Studio** and **Pega Blueprint** and uses Pega's case management capabilities to automate the vehicle servicing workflow.

## Objectives

The main objectives of the application are:

* Allow customers to submit vehicle service requests.
* Maintain reusable vehicle information.
* Enable service advisors to inspect vehicles.
* Generate service estimates automatically.
* Allow customers to approve or reject estimates.
* Automatically route service requests to technicians/work queues.
* Track service execution.
* Notify customers when service is completed.
* Enforce service-level agreements using goals and deadlines.

## Application Workflow

```text
Customer
   |
   v
Submit Vehicle Service Request
   |
   v
Inspection
   |
   +--> Perform Vehicle Inspection
   |
   +--> Generate Service Estimate
   |
   v
Approval
   |
   +--> Customer Reviews Estimate
   |
   +--> Approved ------> Service Execution
   |
   +--> Rejected ------> Case Resolved
   |
   v
Service Execution
   |
   +--> Automatic Vehicle-Type Routing
   |
   +--> Technician Assignment
   |
   v
Service Completion
   |
   v
Customer Notification
   |
   v
Case Resolved
```

## Main Case Type

### Vehicle Service Request

The **Vehicle Service Request** case represents the complete service lifecycle.

The case contains information such as:

* Vehicle ID
* Vehicle Model
* Vehicle Type
* Issue Description
* Inspection Notes
* Condition Rating
* Labor Cost
* Parts Cost
* Total Cost
* Approval Status
* Assigned Technician
* Service Status
* Service Summary

## Personas

### Customer

The Customer can:

* Submit a vehicle service request.
* Provide vehicle information.
* Describe the vehicle issue.
* Review service estimates.
* Approve or reject service estimates.
* Receive service completion notifications.

### Service Advisor

The Service Advisor can:

* Perform vehicle inspection.
* Enter inspection findings.
* Record condition rating.
* Generate service estimates.
* Enter labor and parts costs.
* Review calculated total cost.

### Technician

The Technician can:

* Receive assigned service requests.
* Perform vehicle service.
* Update service status.
* Complete service activities.

## Vehicle Data Object

A reusable **Vehicle** data object is maintained independently from the case.

### Vehicle Properties

| Property   | Description                      |
| ---------- | -------------------------------- |
| Vehicle ID | Unique identifier of the vehicle |
| Model      | Vehicle model                    |
| Type       | Vehicle type                     |

The Vehicle data object can be reused across multiple service requests.

## Cost Calculation

The application automatically calculates the total service estimate.

```text
Total Cost = Labor Cost + Parts Cost
```

For example:

```text
Labor Cost = 5000
Parts Cost = 3000

Total Cost = 5000 + 3000
           = 8000
```

## Automatic Routing

Service requests are automatically routed based on vehicle type.

```text
Vehicle Type = Heavy
        |
        v
HeavyVehicleQueue
```

```text
Vehicle Type = Light / Other
        |
        v
LightVehicleQueue
```

## Approval Process

The Customer reviews:

* Labor Cost
* Parts Cost
* Total Cost

The Customer then selects:

* Approved
* Rejected

### Approved

The case proceeds to **Service Execution**.

### Rejected

The case is resolved with an appropriate rejected status.

## SLA

The application uses a simple Service Level Agreement.

| SLA Component | Value  |
| ------------- | ------ |
| Goal          | 2 Days |
| Deadline      | 3 Days |

If the 2-day goal is missed, the case is flagged as approaching the deadline.

If the 3-day deadline is missed, the case priority is automatically increased.

## Service Completion Notification

When the service request is completed/resolved, the Customer receives a notification containing:

* Case ID
* Vehicle ID
* Vehicle Model
* Service Summary
* Total Cost

## Technologies

* Pega Platform
* Pega App Studio
* Pega Blueprint
* Pega Case Management
* Pega Data Objects
* Pega Personas
* Pega Business Rules
* Pega SLA
* Pega Correspondence

## Project Requirements Covered

The application addresses the following requirements:

1. Submit Vehicle Service Request
2. Perform Vehicle Inspection
3. Generate Service Estimate
4. Approve Service Estimate
5. Maintain Vehicle Data
6. Review Service Estimate
7. Auto Assign Technician
8. Notify Service Completion
9. Define Service SLA
10. Route Service Request by Vehicle Type

## Conclusion

The Vehicle Service Management Application provides an automated and structured approach to vehicle servicing. It improves service request management, ensures proper approval and routing, maintains consistent vehicle information, tracks service activities, and keeps customers informed about service completion.
