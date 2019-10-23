# Module 5. Resource Cleanup

In this module, you will go through the steps to terminate all the resources you created throughout this tutorial. You will terminate an Amazon S3 bucket, an AWS Lambda function, an IAM role, a DynamoDB table, a REST API, and a CloudWatch Log. It is a best practice to delete resources you are no longer using to avoid unwanted charges.

**Services to Delete**: AWS Lambda, Amazon API Gateway, Amazon S3, Amazon DynamoDB, AWS CloudWatch 

## Instructions

Follow the step-by-step instructions below to delete the AWS resources you created in each module.

### Step 1. Delete your Amazon S3 bucket

1. In the AWS Management Console choose Services then select S3 under Storage. 
2. Select the bucket you created in module 1. 
3. Choose Delete bucket. 
4. Enter the name of your bucket when prompted to confirm, Then choose confirm.

### Step 2. Delete your serverless backend

Delete the AWS Lambda function, IAM role and Amazon DynamoDB table you created in module 3.

**Lambda Function**

1. In the AWS Management Console, click Services then select Lambda under Compute. 
2. Select the `AddPwaUser` function you created in module 3. 
3. From the Actions drop-down, choose Delete function. 
4. Choose Delete when prompted to confirm. 

**IAM Role**

1. In the AWS Management Console, click Services then select IAM under Security, Identity & Compliance. 
2. Select Roles from the navigation menu. 
3. Type `PwaUsersLambda` into the filter box. 
4. Select the role you created in module 3. 
5. From the Role actions drop-down, select Delete role. 
6. Choose Yes, Delete when prompted to confirm. 

**DynamoDB Table**

1. In the AWS Management Console, click Services then select DynamoDB under Databases 
2. Choose Tables in the navigation menu. 
3. Choose the table you created in module 3. 
4. Choose Delete table from the Actions drop-down. 
5. Leave the checkbox to Delete all CloudWatch alarms for this table selected and choose Delete.

### Step 3. Delete your REST API

Delete the REST API created in module 4. There is a Delete API option in the Actions drop-down when you select your API in the Amazon API Gateway Console.

1. In the AWS Management Console, click Services then select API Gateway under Application Services. 
2. Select the API you created in module 4. 
3. Expand the Actions drop-down and choose Delete API. 
4. Enter the name of your API when prompted and choose Delete API.

### Step 4. Delete your CloudWatch Log

AWS Lambda automatically creates a new log group per function in Amazon CloudWatch Logs and writes logs to it when your function is invoked. You should delete the log group for your lambda function.

1. From the AWS Console click Services then select CloudWatch under Management Tools. 
2. Choose Logs in the navigation menu. 
3. Select your log group (e.g. `/aws/lambda/AddPwaUser`). If you have many log groups in your account, you can type into the Filter text box to easily locate the log group. 
4. Choose Delete log group from the Actions drop-down. 
5. Choose Yes, Delete when prompted to confirm. 

![](https://d1.awsstatic.com/Test%20Images/Kate%20Test%20Images/Serverless_Web_App_LP_assets-badge.298c74454576a83068bd07f5ec1f271f9d10ad04.png)

### Congratulations, you built and terminated a serverless web application using Amazon Web Services!