# Serverless-Photo-Gallery-Application-with-AWS-and-Flask

This project implements a **Serverless Photo Gallery Application** using AWS services such as **Lambda**, **API Gateway**, **S3**, **DynamoDB**, and **Cognito**. The application demonstrates both SQL (Amazon RDS) and NoSQL (DynamoDB) implementations, showcasing scalable and persistent solutions for a photo management system.

## Important Notice
**For security reasons, sensitive files such as keys, credentials, and configuration files will NOT be included in this repository.**


## Overview

The system includes:
- **Static Web Interface** hosted on S3
- **API Gateway** endpoints for backend connectivity
- **AWS Lambda Functions** for serverless processing
- **DynamoDB** for NoSQL storage of photo metadata
- **S3 Buckets** for photo storage
- **Cognito** for user authentication and pool management

---

## Features

1. **User Management**:
   - **Sign-Up**: Create accounts with email verification and hashed passwords.
   - **Log-In**: Authenticate users with session tokens.
   - **Cancel Account**: Remove user data, albums, and associated photos.

2. **Photo Management**:
   - **Add Photos**: Upload photos to an S3 bucket.
   - **Delete Photos**: Remove selected photos.
   - **Update Photos**: Modify titles, descriptions, and tags.

3. **Album Management**:
   - **Create Albums**: Organize photos into albums.
   - **Delete Albums**: Remove albums with associated photos.

4. **Search**:
   - Filter photos by tags, titles, or descriptions.

---

## Architecture Diagram

The application architecture uses the following AWS services:
- **Lambda**: Serverless compute for API requests.
- **API Gateway**: HTTP endpoints for the backend.
- **DynamoDB**: Persistent metadata storage.
- **S3**: Hosting the static web interface and storing photos.
- **Cognito**: User authentication and session management.

---

## Setup Instructions

### Prerequisites

- AWS Account (Region: **us-east-1** or **N. Virginia**)
- Installed tools: `AWS CLI`, `Python 3.x`, `npm`

### Steps

1. **Create S3 Buckets**:
   - Host the static website.
   - Store photos.

2. **Create DynamoDB Table**:
   - Table Name: `PhotoGallery`
   - Partition Key: `PhotoID`
   - Sort Key: `CreationTime`

3. **Set Up Cognito User Pool**:
   - Pool Name: `PhotoGalleryUserPool`
   - Save `Pool ID` and `Client ID` for integration.

4. **Create IAM Roles**:
   - `lambda_photogallery_role`: Attach `AmazonDynamoDBFullAccess` and `AmazonCognitoPowerUser`.
   - `apiS3PutGet-Role`: Attach `AmazonAPIGatewayPushToCloudWatchLogs` and `AmazonS3FullAccess`.

5. **Deploy Lambda Functions**:
   - Functions: `signup`, `login`, `confirmemail`, `addphoto`, `getphotos`, `getphoto`, `search`.
   - Update `<USER_POOL_ID>` and `<CLIENT_ID>` in the code.

6. **Configure API Gateway**:
   - Create resources and methods for endpoints such as `/signup`, `/photos`, `/photos/{id}`, etc.
   - Deploy the API with a stage name `dev`.

7. **Update Static Website**:
   - Replace placeholders in `process.js` with API URL and S3 bucket name.
   - Host the updated static files in the S3 bucket.

8. **Access the Application**:
   - Visit the S3-hosted website URL.

---

## Testing

### User Management
- **Sign-Up**: Register users with email verification.
- **Log-In**: Authenticate users using tokens.
- **Cancel Account**: Delete user data and photos.

### Photo Operations
- **Add Photo**: Upload photos to S3.
- **Delete Photo**: Remove specific photos.
- **Update Photo**: Modify metadata of uploaded photos.

### Album Operations
- **Create Album**: Group photos into collections.
- **Delete Album**: Remove albums and associated photos.
