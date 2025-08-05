# AWS Step Functions - All Types Example

A comprehensive example demonstrating all major AWS Step Functions state types including Pass, Choice, Parallel, Map, Wait, Fail, and Succeed states.

## State Machine Overview

This state machine showcases:
- **Pass State**: Adds metadata to input
- **Choice State**: Routes execution based on request type
- **Parallel State**: Runs multiple branches concurrently
- **Map State**: Iterates over array items
- **Wait State**: Pauses execution for 10 seconds
- **Fail/Succeed States**: Terminal states for error handling and success

## How to Run

### Prerequisites
- AWS CLI configured with appropriate permissions
- AWS Step Functions service access

### Deploy the State Machine

1. Create the state machine using AWS CLI:
```bash
aws stepfunctions create-state-machine \
  --name "AllTypesExample" \
  --definition file://state-machine.json \
  --role-arn "arn:aws:iam::YOUR_ACCOUNT:role/StepFunctionsExecutionRole"
```

### Example Input Payloads

#### For Parallel Execution:
```json
{
  "requestType": "runParallel",
  "userId": "user123"
}
```

#### For Map Execution:
```json
{
  "requestType": "runMap",
  "items": ["item1", "item2", "item3"],
  "userId": "user123"
}
```

#### For Failure Case:
```json
{
  "requestType": "invalidType",
  "userId": "user123"
}
```

### Execute the State Machine

```bash
aws stepfunctions start-execution \
  --state-machine-arn "arn:aws:states:REGION:ACCOUNT:stateMachine:AllTypesExample" \
  --input '{"requestType": "runParallel", "userId": "user123"}'
```

## Expected Outputs

- **Parallel execution**: Completes both branches and returns combined results
- **Map execution**: Processes each item in the array and returns processed results
- **Invalid request**: Terminates with "InvalidRequestType" error
