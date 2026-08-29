# Vehicle Service Management Application

## Test Cases

## 1. Testing Objective

The purpose of testing is to verify that all business requirements of the Vehicle Service Management Application work correctly.

---

## TC-01: Submit Vehicle Service Request

**Requirement:** Submit Vehicle Service Request

**Steps:**

1. Log in as Customer.
2. Create a Vehicle Service Request.
3. Enter Vehicle ID.
4. Enter Vehicle Model.
5. Enter Vehicle Type.
6. Enter Issue Description.
7. Submit the case.

**Expected Result:**

The request should be successfully created when all required fields are provided.

---

## TC-02: Validate Required Fields

**Requirement:** Required information validation

**Steps:**

1. Start a Vehicle Service Request.
2. Leave one or more required fields empty.
3. Attempt to submit.

**Expected Result:**

The system should prevent submission until all required information is provided.

---

## TC-03: Perform Vehicle Inspection

**Requirement:** Perform Vehicle Inspection

**Steps:**

1. Open a submitted service request as Service Advisor.
2. Open the Inspection stage.
3. Enter Inspection Notes.
4. Enter Condition Rating.
5. Complete the inspection.

**Expected Result:**

Inspection information should be saved successfully.

---

## TC-04: Inspection Must Be Completed

**Requirement:** Mandatory inspection

**Steps:**

1. Open the Inspection stage.
2. Do not complete the inspection.
3. Attempt to proceed to the next processing step.

**Expected Result:**

The case should not proceed until the mandatory inspection activity is completed.

---

## TC-05: Generate Service Estimate

**Requirement:** Generate Service Estimate

**Steps:**

1. Open Generate Service Estimate.
2. Enter Labor Cost.
3. Enter Parts Cost.
4. Review Total Cost.

**Expected Result:**

The system should calculate Total Cost automatically.

---

## TC-06: Verify Total Cost Calculation

**Requirement:** Total Cost calculation

**Input:**

```text
Labor Cost = 5000
Parts Cost = 3000
```

**Expected Result:**

```text
Total Cost = 8000
```

The calculated value should be stored in the case.

---

## TC-07: Review Service Estimate

**Requirement:** Review Service Estimate

**Steps:**

1. Log in as Customer.
2. Open the approval step.
3. Review the estimate.

**Expected Result:**

The Customer should be able to see:

* Labor Cost
* Parts Cost
* Total Cost

---

## TC-08: Approve Service Estimate

**Requirement:** Approval

**Steps:**

1. Log in as Customer.
2. Review the estimate.
3. Select Approved.

**Expected Result:**

The case should proceed to Service Execution.

---

## TC-09: Reject Service Estimate

**Requirement:** Rejection

**Steps:**

1. Log in as Customer.
2. Review the estimate.
3. Select Rejected.

**Expected Result:**

The case should be resolved with an appropriate rejected status and should not proceed to Service Execution.

---

## TC-10: Vehicle Data Object

**Requirement:** Maintain Vehicle Data

**Steps:**

1. Create or access Vehicle data.
2. Enter Vehicle ID.
3. Enter Model.
4. Enter Type.
5. Associate the Vehicle with a service request.

**Expected Result:**

The Vehicle information should be reusable and associated with the Vehicle Service Request.

---

## TC-11: Heavy Vehicle Routing

**Requirement:** Vehicle Type Routing

**Input:**

```text
Vehicle Type = Heavy
```

**Expected Result:**

The case should automatically route to:

`HeavyVehicleQueue`

---

## TC-12: Light Vehicle Routing

**Requirement:** Vehicle Type Routing

**Input:**

```text
Vehicle Type = Light
```

**Expected Result:**

The case should automatically route to:

`LightVehicleQueue`

---

## TC-13: Other Vehicle Type Routing

**Requirement:** Vehicle Type Routing

**Input:**

```text
Vehicle Type = Other
```

**Expected Result:**

The case should automatically route to:

`LightVehicleQueue`

---

## TC-14: Technician Assignment

**Requirement:** Auto Assign Technician

**Steps:**

1. Approve a service estimate.
2. Enter Service Execution.
3. Observe assignment.

**Expected Result:**

The system should automatically assign/route the case to the appropriate Technician persona or technician work queue.

---

## TC-15: Service Status Tracking

**Requirement:** Service Execution

**Steps:**

1. Open the service request as Technician.
2. Update Service Status.
3. Complete the service.

**Expected Result:**

The Service Status and Assigned Technician should be maintained correctly.

---

## TC-16: Service Completion Notification

**Requirement:** Notify Service Completion

**Steps:**

1. Complete the service.
2. Resolve the case.
3. Check the Customer notification.

**Expected Result:**

A completion notification should be generated containing:

* Case ID
* Vehicle ID
* Vehicle Model
* Service Summary
* Total Cost

---

## TC-17: SLA Goal

**Requirement:** Service SLA

**Configuration:**

```text
Goal = 2 Days
```

**Expected Result:**

When the 2-day goal is missed, the case should be flagged as approaching the deadline.

---

## TC-18: SLA Deadline

**Requirement:** Service SLA

**Configuration:**

```text
Deadline = 3 Days
```

**Expected Result:**

When the 3-day deadline is missed, the case priority should automatically increase.

---

## TC-19: End-to-End Approved Request

**Steps:**

1. Customer submits request.
2. Service Advisor performs inspection.
3. Service Advisor generates estimate.
4. Customer reviews estimate.
5. Customer approves estimate.
6. System routes case to appropriate queue.
7. Technician performs service.
8. Technician completes service.
9. Case is resolved.
10. Customer receives notification.

**Expected Result:**

The complete service process should execute successfully.

---

## TC-20: End-to-End Rejected Request

**Steps:**

1. Customer submits request.
2. Service Advisor performs inspection.
3. Service Advisor generates estimate.
4. Customer reviews estimate.
5. Customer rejects estimate.

**Expected Result:**

The case should be resolved as rejected and should not enter Service Execution.

---

## Test Summary

| Requirement             | Test Case           |
| ----------------------- | ------------------- |
| Submit Service Request  | TC-01               |
| Required Validation     | TC-02               |
| Vehicle Inspection      | TC-03, TC-04        |
| Service Estimate        | TC-05, TC-06        |
| Estimate Review         | TC-07               |
| Estimate Approval       | TC-08, TC-09        |
| Vehicle Data            | TC-10               |
| Technician Assignment   | TC-14, TC-15        |
| Completion Notification | TC-16               |
| SLA                     | TC-17, TC-18        |
| Vehicle Routing         | TC-11, TC-12, TC-13 |
| End-to-End Process      | TC-19, TC-20        |
