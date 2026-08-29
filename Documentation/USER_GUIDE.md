# Vehicle Service Management Application

## User Guide

## 1. Purpose

This guide explains how the different users interact with the Vehicle Service Management Application.

The application has three primary personas:

* Customer
* Service Advisor
* Technician

---

## 2. Customer Guide

### Step 1: Submit Service Request

The Customer starts a new **Vehicle Service Request**.

Enter:

* Vehicle ID
* Vehicle Model
* Vehicle Type
* Issue Description

Submit the request after providing all required information.

### Step 2: Review Service Estimate

After inspection and estimate generation, the Customer receives the estimate.

Review:

* Labor Cost
* Parts Cost
* Total Cost

### Step 3: Approve or Reject

Select the appropriate decision.

#### Approve

The request moves to Service Execution.

#### Reject

The request is resolved as rejected.

### Step 4: Receive Completion Notification

After the service is completed, the Customer receives a service completion notification containing:

* Case ID
* Vehicle ID
* Vehicle Model
* Service Summary
* Total Cost

---

## 3. Service Advisor Guide

### Step 1: Open Service Request

Open the assigned Vehicle Service Request.

### Step 2: Perform Inspection

Enter:

* Inspection Notes
* Condition Rating

Complete the mandatory inspection step.

### Step 3: Generate Estimate

Enter:

* Labor Cost
* Parts Cost

The system calculates:

```text
Total Cost = Labor Cost + Parts Cost
```

Verify the calculated Total Cost before submitting the estimate.

---

## 4. Technician Guide

### Step 1: Receive Assignment

The system automatically routes the service request to the appropriate technician work queue.

### Step 2: Check Vehicle Type

For Heavy vehicles:

`HeavyVehicleQueue`

For Light or other vehicles:

`LightVehicleQueue`

### Step 3: Perform Service

Perform the required vehicle service.

Update:

* Assigned Technician
* Service Status

### Step 4: Complete Service

Update the Service Status to the appropriate completed status and provide the Service Summary.

The case can then proceed to resolution.

---

## 5. Vehicle Data

The Vehicle data object maintains reusable vehicle information.

It contains:

* Vehicle ID
* Model
* Type

The same vehicle information can be reused for multiple service requests.

---

## 6. SLA

Each Vehicle Service Request is subject to:

* Goal: 2 days
* Deadline: 3 days

Missing the goal flags the case as approaching the deadline.

Missing the deadline increases the case priority.

---

## 7. End-to-End Process

```text
Customer submits request
        ↓
Service Advisor performs inspection
        ↓
Service Advisor generates estimate
        ↓
Customer reviews estimate
        ↓
Customer approves/rejects
        ↓
Approved?
   ↙          ↘
 No            Yes
 ↓              ↓
Resolve     Service Execution
                ↓
       Automatic Technician Routing
                ↓
          Service Completed
                ↓
       Customer Notification
                ↓
             Resolved
```
