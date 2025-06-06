# README for AwardCo_1

## Overview
The AwardCo_1 application is designed to automate the processing of employee and department data through various workflows. It integrates with external systems via REST APIs to fetch, process, and store employee and department information, ultimately facilitating efficient data management and reporting. The application handles batch processing of data, ensuring that updates and records are synchronized across systems, thereby improving operational efficiency and accuracy. It also includes error handling mechanisms to manage failures gracefully, ensuring data integrity and reliability.

## Integration Details
This application integrates with:
- **REST APIs**: To fetch employee and department details from external systems.
- **File Systems**: For reading and writing CSV files to and from SFTP servers.
- **Data Tables**: For storing and upserting employee and department data.

Data flows in and out of the application primarily in JSON and CSV formats, with interactions occurring between the application and external APIs for data retrieval and updates.

## Installation Steps
1. Ensure that all necessary dependencies and libraries for the application are installed.
2. Configure the application environment with the required API keys and authentication contexts for Paycor and SFTP.
3. Set up the necessary data tables in the database for storing employee and department information.
4. Deploy the application to the desired environment (e.g., cloud or on-premises).

## Variables Used
- **engage**: Context variable for Engage integration.
- **legalEntityId**: Path parameter used to identify the legal entity in API calls.
- **continuationToken**: Query parameter for paginating through API results.
- **batchId**: Identifier for the batch being processed.
- **maxFailures**: Configuration variable to limit the number of allowed failures in scheduled tasks.
- **contexts**: Array of context variables used in various workflows to manage state.
- **output**: Variable used to capture the output of various steps in workflows.
- **authContext**: Variable used to define the authentication context for API calls.

## API Details
- **GetDepartmentDetails**
  - **Endpoint**: `/v1/legalentities/{legalEntityId}/departments?continuationToken`
  - **Description**: Fetches department details for a specified legal entity, supporting pagination through continuation tokens.

- **GetPersonDetails**
  - **Endpoint**: `/v1/legalentities/{legalEntityId}/persons?include=All&continuationToken`
  - **Description**: Retrieves person details associated with a legal entity, allowing for comprehensive employee data management.

- **DeleteBatch**
  - **Endpoint**: `/deleteBatch?id`
  - **Description**: Deletes a specified batch after processing, ensuring that completed tasks are cleared from the system.

- **ReadCSVFile**
  - **Endpoint**: `/test/awardCo`
  - **Description**: Reads a CSV file from Azure Storage, facilitating data ingestion for processing.

- **WriteCSVFiletoSFTP**
  - **Endpoint**: SFTP server endpoint (configured in the application).
  - **Description**: Writes processed CSV files to an SFTP server for external access and storage.

## Processes / Workflows
- **Batch Receiver**: Receives batch events, processes them, and updates records accordingly.
- **Scheduler**: Schedules batch processes to run at specified intervals, ensuring timely data updates.
- **Batch Process**: Handles the main logic for processing batches of data, including initialization and completion steps.
- **Employee Data**: Manages the retrieval and processing of employee information, including updates and error handling.
- **File Process**: Facilitates the reading and writing of files to and from SFTP servers, ensuring data is correctly stored and accessible.
- **Main Process**: Coordinates the overall workflow, integrating department and person data processing in parallel.
- **Delete Batch**: Handles the deletion of completed batches, ensuring that the system remains clean and efficient.
- **Test Batch Process**: Tests the batch processing logic to ensure it functions as expected.
- **Test Main Process**: Validates the main process workflow to confirm that all components work together seamlessly.
- **Test PGP Encryption**: Tests the PGP encryption functionality for secure file handling.
- **Department Data**: Manages the upsert operations for department data, ensuring that updates are accurately reflected in the system.
- **Person Data**: Handles the upsert operations for person data, ensuring comprehensive employee records are maintained.

## Error Handling
The application employs robust error handling mechanisms across its workflows:
- **Retry Logic**: Certain workflows include retry logic to handle transient errors when fetching data from external APIs.
- **Conditional Logic**: Workflows like Employee Data and Department Data utilize conditional checks to determine success or failure, triggering appropriate error handling steps.
- **Logging**: Errors are logged using the Log activity, providing visibility into issues that occur during processing.
- **Notifications**: In case of critical failures, workflows are designed to notify external systems or users, ensuring that issues are addressed promptly.

Workflows such as Test Batch Process and Test Main Process include specific error handling logic to validate the overall application functionality and ensure that any failures are managed effectively.