# AWS Cloud Cost Optimization: Automated Snapshot Deletion

This project aims to reduce AWS storage costs by automatically identifying and deleting unused or old snapshots. By leveraging AWS Lambda, CloudWatch Events, and Boto3, the solution automates the process of managing snapshots based on predefined criteria.

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Setup](#setup)
  - [Prerequisites](#prerequisites)
  - [Deployment](#deployment)
- [Configuration](#configuration)
- [Usage](#usage)

## Overview
AWS Cost Optimization: Automated Snapshot Deletion is designed to help users reduce unnecessary storage costs by automatically deleting snapshots that are no longer needed. The solution includes:
- Identification of snapshots not attached to any volume or attached to a volume that is not attached to any EC2 instance
- Automated deletion using AWS Lambda
- Scheduled execution with AWS CloudWatch Events

## Features
- **Automated Snapshot Deletion**: Automatically deletes snapshots that are not attached to any volume or attached to a volume that is not attached to any EC2 instance.
- **Cost Savings**: Reduces AWS storage costs by removing unnecessary snapshots.
- **Scheduled Execution**: Uses AWS CloudWatch Events to trigger the deletion process periodically.
- **Customizable**: Easily configure criteria for snapshot deletion.

## Setup

### Prerequisites
- AWS Account
- AWS CLI configured with appropriate credentials

### Deployment

1. **Create an EC2 Instance and Snapshot**
    - Launch a new EC2 instance in the AWS Management Console.
  
      ![Screenshot 2024-06-03 155917](https://github.com/PoornaChaitanya/Cloud-Cost-Optimization-Project/assets/84367538/e0c479d8-6ca6-4100-aac9-a4e7f77b4a24)

    - Create a volume and attach it to the EC2 instance.
    - Create a snapshot of the attached volume.

      ![Screenshot 2024-06-03 155932](https://github.com/PoornaChaitanya/Cloud-Cost-Optimization-Project/assets/84367538/3231e0b7-a0ea-4604-9bb3-57500489eeb9)


1. **Create and Configure Lambda Function**
    - Create a new Lambda function in the AWS Management Console.

      ![Screenshot 2024-06-03 155950](https://github.com/PoornaChaitanya/Cloud-Cost-Optimization-Project/assets/84367538/51bf7e6f-d491-45b6-84dc-65bdee6e271b)

    - Attach the following permissions directly to role of the Lambda function:
        - `ec2:DescribeSnapshots`
        - `ec2:DeleteSnapshot`
        - `ec2:DescribeVolumes`
        - `ec2:DescribeInstances`
    - Upload the Lambda function code (`snapshots.py`):

      ![Screenshot 2024-06-03 160007](https://github.com/PoornaChaitanya/Cloud-Cost-Optimization-Project/assets/84367538/7d09a385-f7df-4771-9096-2b496cafd6cf)

2. **Delete the EC2 Instance and Volume**
    - Terminate the EC2 instance created in step 1.

      ![Screenshot 2024-06-03 160050](https://github.com/PoornaChaitanya/Cloud-Cost-Optimization-Project/assets/84367538/9461d2a7-7fec-4b81-8690-13b87c113499)

    - Delete the volume attached to the EC2 instance and test the code in lambda function.

      ![Screenshot 2024-06-03 160249](https://github.com/PoornaChaitanya/Cloud-Cost-Optimization-Project/assets/84367538/35bb4181-c640-41ec-b072-c66cca2bb88e)


3. **Create CloudWatch Event Rule**
    - Create a CloudWatch Event Rule to trigger the Lambda function periodically (e.g., daily).
    - Configure the rule to trigger the Lambda function created in step 2.

## Configuration
Modify the `snapshots.py` file to adjust the snapshot deletion criteria as needed.

## Usage
Once deployed, the Lambda function will run periodically as per the CloudWatch Event rule, automatically deleting snapshots based on the defined criteria. Monitor the Lambda function logs to ensure that snapshots are being deleted as expected.


