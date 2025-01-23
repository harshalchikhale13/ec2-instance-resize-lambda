# EC2 Instance Resize Lambda Function

This repository contains an AWS Lambda function to resize an EC2 instance by stopping it, modifying its instance type, and restarting it. The function supports cross-region operations by allowing the region to be specified dynamically in the event.

## Features

- Stops the EC2 instance gracefully.
- Waits until the instance is fully stopped before modifying it.
- Changes the instance type (default: `t2.medium`).
- Restarts the instance after modification.
- Handles cross-region operations by allowing the region to be specified dynamically in the event.
- Provides detailed error handling and logging.

## Prerequisites

1. **AWS Account**:
   - Ensure your account has EC2 instances to manage.
2. **AWS Lambda**:
   - Python runtime (3.7 or higher).
3. **IAM Role for Lambda**:
   - Permissions required:
     - `ec2:StopInstances`
     - `ec2:StartInstances`
     - `ec2:ModifyInstanceAttribute`
     - `ec2:DescribeInstances`
     - `ec2:WaitFor`
4. **Boto3 Library**:
   - Pre-installed in the AWS Lambda runtime.

## Deployment

1. Clone the repository:
   ```bash
   git clone https://github.com/harshalchikhale13/ec2-instance-resize-lambda.git
   cd ec2-instance-resize-lambda


## Zip the Lambda function code:
2. zip -r ec2_resize_lambda.zip .

3. Upload the zip file to your AWS Lambda function.

4. Assign the Lambda function an IAM role with appropriate EC2 permissions.

## Usage

1. Trigger the Lambda function with an event containing:

  **instanceId** : The ID of the EC2 instance you want to resize.
  **region** : The AWS region where the instance is located.

## Example Event
{
    "instanceId": "i-0abcdef1234567890",
    "region": "ap-south-1"
}

1. The Lambda function will:
Stop the instance in the specified region.
Wait until it is completely stopped.
Modify the instance type to t2.medium (or the hardcoded type in the script).
Restart the instance.

## Customization

**Instance Type** : Modify the InstanceType value in the code to change the default instance type.
Code: ec2_client.modify_instance_attribute(InstanceId=instance_id, InstanceType={'Value': 't2.medium'})

**Default Region** : Update the default region in the lambda_handler function:
Code : region = event.get('region', 'ap-south-1')








