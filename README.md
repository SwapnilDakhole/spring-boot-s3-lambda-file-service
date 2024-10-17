
**spring-boot-s3-lambda-file-service**

---

### README.md

```md
# Spring Boot S3 and Lambda File Service

## Overview

This repository contains two Spring Boot projects:
1. **File Storage Service**: Handles file uploads and retrieves files from AWS S3.
2. **AWS Lambda Trigger Service**: Triggers an AWS Lambda function when a file is uploaded to an S3 bucket.

Both projects utilize AWS services and are designed to work with MySQL for storing additional metadata.

## Features

- **File Storage Service**:
  - Upload files to AWS S3.
  - Retrieve files from AWS S3 by filename.
  
- **AWS Lambda Trigger Service**:
  - Triggers a Lambda function automatically when a file is uploaded to an S3 bucket.
  - Lambda function processes or logs file metadata after the upload.

## Prerequisites

- **Java 17**
- **Maven**
- **MySQL** database
- **AWS SDK for Java v2**
- **AWS Account** (for S3, Lambda)

## Setup

### AWS Configuration

1. Create an S3 bucket to store files.
2. Set up an AWS Lambda function that will be triggered upon file uploads to S3.
3. Configure necessary IAM roles for S3 and Lambda with the correct permissions.

### MySQL Configuration

1. Create a MySQL database to store file metadata.
2. Update the database connection settings in the `application.yml` of each Spring Boot project.

### Spring Boot Configuration

1. Update the `application.yml` in both projects with your AWS credentials, S3 bucket name, and MySQL database connection details.

   **Example `application.yml`:**
   ```yaml
   aws:
     s3:
       bucket: your-s3-bucket-name
     access-key: YOUR_AWS_ACCESS_KEY
     secret-key: YOUR_AWS_SECRET_KEY
   spring:
     datasource:
       url: jdbc:mysql://localhost:3306/your_database
       username: your_username
       password: your_password
   ```

### Running the Application

#### File Storage Service

1. Navigate to the `file-storage-service` directory.
2. Run the application:
   ```bash
   mvn spring-boot:run
   ```
3. Upload files via API (e.g., using Postman) to the `/upload` endpoint.

#### Lambda Trigger Service

1. Navigate to the `lambda-trigger-service` directory.
2. Deploy the Lambda function that will be triggered by S3 file uploads.
3. Ensure your Lambda function is correctly configured to process the S3 events.

## API Endpoints

### File Storage Service

- **Upload a file:**
  ```http
  POST /upload
  ```
  Uploads a file to the configured S3 bucket.

- **Retrieve a file:**
  ```http
  GET /files/{filename}
  ```
  Downloads a file from S3 based on the filename.

## Project Structure

### File Storage Service

- `controller/`: Contains the API endpoints for file uploads and retrieval.
- `service/`: Handles interaction with AWS S3.
- `model/`: Defines entities for storing file metadata.

### Lambda Trigger Service

- AWS Lambda function code is designed to handle file upload events from S3.

## Dependencies

- Spring Boot
- AWS SDK for Java v2
- Spring Data JPA (for MySQL)
- Lombok (for simplifying Java code)

## Future Enhancements

- Add more comprehensive error handling.
- Implement authentication for file uploads and retrieval.
- Extend Lambda functionality to perform additional tasks (e.g., file processing or metadata extraction).

