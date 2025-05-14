# Pointscene API Scheduled Jobs Documentation

## Scheduled Jobs

The Pointscene API provides functionality to create, manage, and query scheduled jobs. These jobs allow you to automate recurring tasks within the platform.

## Overview

Scheduled jobs in Pointscene API enable users to:
- Add configuration
- Create new scheduled jobs
- Query existing scheduled jobs
- Update job configurations

## Add Configuration [example here](https://github.com/Pointscene/pointscene-api-examples/blob/main/docs/AddConfig.md)   

Before creating a scheduled job, you need to define its configuration. Add configuration settings for external services that a scheduled job needs to interact with. Securely store these configurations in an encrypted format.

## Create Scheduled Job [example here](https://github.com/Pointscene/pointscene-api-examples/blob/main/docs/CreateScheduledJob.md)   

Once you have defined the configuration, you can create a new scheduled job using the API. The createScheduledJob mutation allows you to create automated, recurring jobs within the Pointscene platform. These jobs can execute predefined workflows on a schedule, either using cron expressions or time intervals.

### Scheduled Job Parameters

### `instanceId`
- **Type**: ID (number internally)
- **Description**: The unique identifier of the instance where the job will be created.
- **Example**: `"inst_abc123"`
- **Notes**: Must be a valid instance that the user has access to.

### `workflow`
- **Type**: JSON object (`Record<string, any>`)
- **Description**: Defines the task to be executed, including all necessary configuration.
- **Example**: Synchronize data between ACC and Google Drive [example here](https://github.com/Pointscene/pointscene-api-examples/blob/main/docs/CreateScheduledJob.md)
- **Notes**: The structure depends on the type of job being created. All resource IDs must belong to the specified instance.

### `frequencyType`
- **Type**: String (enum)
- **Description**: Determines how the job's schedule is defined.
- **Valid Values**:
  - `CRON_BASED`: Schedule defined using a cron expression
  - `INTERVAL_BASED`: Schedule defined as a fixed interval in minutes
- **Example**: `"CRON_BASED"`

### Conditional Parameters

### `cronExpression`
- **Type**: String
- **Required**: Only when `frequencyType` is `CRON_BASED`
- **Description**: A standard cron expression defining when the job should run.
- **Example**: `"0 0 * * *"` (daily at midnight)
- **Notes**: Must be a valid cron expression. The system uses the standard cron format.

### `intervalMinutes`
- **Type**: Integer
- **Required**: Only when `frequencyType` is `INTERVAL_BASED`
- **Description**: The number of minutes between job executions.
- **Example**: `60` (hourly)
- **Notes**: Must be a positive integer.

### Optional Parameters

### `active`
- **Type**: Boolean
- **Default**: `true`
- **Description**: Whether the job should be active (running according to schedule) or inactive (paused).
- **Example**: `false`
- **Notes**: When set to `false`, the job won't execute until activated.

### `name`
- **Type**: String
- **Description**: A human-readable name for the job.
- **Example**: `"Daily Data Synchronization"`
- **Notes**: Should be descriptive to help identify the job's purpose.

### `description`
- **Type**: String
- **Description**: A detailed description of what the job does.
- **Example**: `"Synchronizes data from the source bucket to the destination bucket every day at midnight."`
- **Notes**: Useful for documenting the job's purpose and behavior.

## Query Scheduled Jobs [example here](https://github.com/Pointscene/pointscene-api-examples/blob/main/docs/QueryJobs.md)   

You can retrieve information about existing scheduled jobs to monitor their status or verify their configurations. API provides two GraphQL queries for retrieving information about scheduled jobs. These queries allow you to list all jobs for an instance or get detailed information about a specific job included job history.

## Update Scheduled Job [example of disabling a job here](https://github.com/Pointscene/pointscene-api-examples/blob/main/docs/UpdateJob.md)   

You can modify existing scheduled jobs to change their configuration, schedule, or task parameters. Allows you to modify an existing scheduled job in the platform. You can update various aspects of the job including its workflow, scheduling parameters, and status. This functionality is essential for maintaining and adjusting automated workflows as requirements change over time.

### Notes
- You only need to include the parameters you want to change
- When updating the workflow, the entire workflow object must be provided (partial updates of the workflow are not supported)
- Changing the frequency type requires providing the corresponding scheduling parameter (cronExpression or intervalMinutes)
- The job's execution history is preserved when updating the job

## Delete Scheduled Job [example here](https://github.com/Pointscene/pointscene-api-examples/blob/main/docs/DeleteJob.md)   

You can delete a scheduled job from the platform using the deleteScheduledJob mutation. This mutation allows you to remove a job from the system, preventing it from executing further.





