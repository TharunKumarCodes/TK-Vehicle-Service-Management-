# Vehicle Service Management Application

## Project Documentation

## 1. Introduction

The Vehicle Service Management Application is designed to automate and manage the complete vehicle servicing lifecycle using Pega Platform.

The application provides a centralized process for customers, service advisors, and technicians. It manages service requests, inspections, estimates, approvals, technician assignment, service execution, SLA tracking, and customer notifications.

## 2. Business Problem

Traditional vehicle service processes may involve manual request handling, disconnected vehicle information, manual technician assignment, and limited visibility of service estimates.

These issues can result in:

* Delayed service processing.
* Incorrect or duplicated vehicle information.
* Manual routing of service requests.
* Lack of estimate transparency.
* Delayed customer approvals.
* Difficulty tracking service requests.
* Poor visibility into service completion.

The proposed Pega application addresses these problems through workflow automation and structured case management.

## 3. Proposed Solution

The solution uses a Pega case type named **Vehicle Service Request**.

The case progresses through multiple stages:

1. Submit Vehicle Service Request
2. Inspection
3. Approval
4. Service Execution
5. Resolution

Business rules are used for:

* Cost calculation.
* Customer approval.
* Vehicle-type routing.
* SLA management.
* Completion notification.

## 4. Case Type

### Vehicle Service Request

The Vehicle Service Request is the primary case type.

It represents a service request from creation through completion.

## 5. Case Lifecycle

### Stage 1: Submit Vehicle Service Request

The Customer submits a service request.

Required information includes:

* Vehicle ID
* Vehicle Model
* Vehicle Type
* Issue Description

The required fields must be validated before submission.

### Stage 2: Inspection

The Service Advisor performs the vehicle inspection.

The following information is captured:

* Inspection Notes
* Condition Rating

The inspection step is mandatory.

The case should not proceed until the inspection is completed.

The Service Advisor then generates the service estimate.

### Stage 3: Approval

The Customer reviews the service estimate.

The estimate contains:

* Labor Cost
* Parts Cost
* Total Cost

The Customer selects either:

* Approved
* Rejected

Approved requests proceed to Service Execution.

Rejected requests are resolved.

### Stage 4: Service Execution

The request is automatically routed based on Vehicle Type.

Heavy vehicles are routed to:

`HeavyVehicleQueue`

Light and other vehicles are routed to:

`LightVehicleQueue`

The Technician performs the service and updates the Service Status.

### Stage 5: Resolution

After the service is completed, the case is resolved.

A completion notification is sent to the Customer.

## 6. Data Model

### Vehicle Data Object

The application contains a reusable Vehicle data object.

Properties:

* Vehicle ID
* Model
* Type

The Vehicle object is associated with the Vehicle Service Request case.

## 7. Case Properties

| Property            | Purpose                      |
| ------------------- | ---------------------------- |
| Vehicle ID          | Identifies the vehicle       |
| Vehicle Model       | Stores vehicle model         |
| Vehicle Type        | Determines routing           |
| Issue Description   | Describes customer issue     |
| Inspection Notes    | Stores inspection findings   |
| Condition Rating    | Records vehicle condition    |
| Labor Cost          | Stores labor estimate        |
| Parts Cost          | Stores parts estimate        |
| Total Cost          | Stores calculated estimate   |
| Approval Status     | Stores customer decision     |
| Assigned Technician | Stores technician assignment |
| Service Status      | Tracks service execution     |
| Service Summary     | Stores completion summary    |

## 8. Business Rules

### Total Cost Rule

The Total Cost is calculated automatically.

```text
Total Cost = Labor Cost + Parts Cost
```

### Vehicle Routing Rule

```text
IF Vehicle Type = Heavy
THEN Route to HeavyVehicleQueue

ELSE
Route to LightVehicleQueue
```

### Approval Rule

```text
IF Approval Status = Approved
THEN Continue to Service Execution

IF Approval Status = Rejected
THEN Resolve Case
```

## 9. SLA Configuration

The Vehicle Service Request has the following SLA:

```text
Goal: 2 Days
Deadline: 3 Days
```

Goal behavior:

* Flag the case when the 2-day goal is missed.

Deadline behavior:

* Increase case priority when the 3-day deadline is missed.

No complex escalation path is required.

## 10. Correspondence

A service completion correspondence is configured.

The Customer receives relevant service information when the case is completed.

The notification includes:

* Case ID
* Vehicle ID
* Vehicle Model
* Service Summary
* Total Cost

## 11. Personas

### Customer

Responsible for request submission and estimate approval.

### Service Advisor

Responsible for inspection and estimate generation.

### Technician

Responsible for service execution.

## 12. Expected Benefits

The application provides:

* Automated service request processing.
* Improved data consistency.
* Faster technician assignment.
* Transparent service estimates.
* Controlled approval workflow.
* Automatic SLA management.
* Improved customer communication.
* Better service tracking.

## 13. Conclusion

The Vehicle Service Management Application demonstrates how Pega can be used to automate a complete business process using case management, data objects, personas, business rules, routing, correspondence, and SLA capabilities.
