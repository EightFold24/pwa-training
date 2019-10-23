# Module 2: Serverless Service Backend

In this module you'll use AWS Lambda and Amazon DynamoDB to build a backend process for handling requests for your web application.
The browser application that you made in previous steps will send its form data to AWS to be stored.
In order to fulfill those requests, the JavaScript running in the browser will need to invoke a service running in the cloud.  

## Architecture Overview

![](https://d1.awsstatic.com/Test%20Images/Kate%20Test%20Images/Serverless_Web_App_LP_assets-04.094e0479bc43ee7ecbbd1f7cc37ab90b83fe5e73.png)

You'll implement a Lambda function that will be invoked each time a user requests to add data to the datastore.
The function will record the request in a DynamoDB table and then respond to the front-end application with details about the new entry added.

The function is invoked from the browser using Amazon API Gateway.
You'll implement that connection in the next module.
For this module you'll just test your function in isolation.

### Step 1. Create an Amazon DynamoDB Table

Use the Amazon DynamoDB console to create a new DynamoDB table. Name your table (e.g. if your webapp form takes user information your table might be called `PwaUsers`) and give it a partition key (e.g. `PwaUserID`) with type String. The table name and partition key are case sensitive. Use the defaults for all other settings.

After you've created the table, note the ARN for use in the next step.

1. From the AWS Management Console, choose Services then select DynamoDB under Databases. 
2. Choose Create table. 
3. Enter a Table name. This field is case sensitive. 
4. Enter a Partition key and select String for the key type. This field is case sensitive. 
5. Check the Use default settings box and choose Create. 
6. Scroll to the bottom of the Overview section of your new table and note the ARN. You will use this in the next section.

### Step 2. Create an IAM Role for Your Lambda function

Every Lambda function has an IAM role associated with it. This role defines what other AWS services the function is allowed to interact with. For the purposes of this workshop, you'll need to create an IAM role that grants your Lambda function permission to write logs to Amazon CloudWatch Logs and access to write items to your DynamoDB table.

Use the IAM console to create a new role. Name it (e.g. `PwaUsersLambda`) and select AWS Lambda for the role type. You'll need to attach policies that grant your function permissions to write to Amazon CloudWatch Logs and put items to your DynamoDB table.

Attach the managed policy called `AWSLambdaBasicExecutionRole` to this role to grant the necessary CloudWatch Logs permissions. Also, create a custom inline policy for your role that allows the `ddb:PutItem` action for the table you created in the previous section.

1. From the AWS Management Console, click on Services and then select IAM in the Security, Identity & Compliance section. 
2. Select Roles in the left navigation bar and then choose Create Role. 
3. Select Lambda for the role type from the AWS service group, then click Next: Permissions. Note: Selecting a role type automatically creates a trust policy for your role that allows AWS services to assume this role on your behalf. If you were creating this role using the CLI, AWS CloudFormation or another mechanism, you would specify a trust policy directly. 
4. Begin typing `AWSLambdaBasicExecutionRole` in the Filter text box and check the box next to that role. 
5. Choose Next Step. 
6. Enter a Role Name (e.g. `PwaUsersLambda`). 
7. Choose Create Role. 
8. Type your role name into the filter box on the Roles page and choose the role you just created. 
9. On the Permissions tab, choose the Add inline policy link in the lower right corner to create a new inline policy. 
10. Select Choose a service.  
11. Begin typing `DynamoDB` into the search box labeled Find a service and select DynamoDB when it appears.
12. Choose Select actions.  
13. Begin typing `PutItem` into the search box labeled Filter actions and check the box next to PutItem when it appears.  
14. Select the Resources section.  
15. With the Specific option selected, choose the Add ARN link in the table section.  
16. Paste the ARN of the table you created in the previous section in the Specify ARN for table field, and choose Add. 
17. Choose Review Policy. 
18. Enter `DynamoDBWriteAccess` for the policy name and choose Create policy.

### Step 3. Create a Lambda Function for Handling Requests

AWS Lambda will run your code in response to events such as an HTTP request.
In this step you'll build the core function that will process API requests from the web application.
In the next module you'll use Amazon API Gateway to create a RESTful API that will expose an HTTP endpoint that can be invoked from your users' browsers.
You'll then connect the Lambda function you create in this step to that API in order to create a fully functional backend for your web application.

Use the AWS Lambda console to create a new Lambda function that will process the API requests.
Modify the provided [lambda.js](lambda.js) example and use as your function code.

Make sure to configure your function to use the IAM role you created in the previous section (e.g. `PwaUsersLambda`).

1. Choose Services then select Lambda in the Compute section. 
2. Click Create function. 
3. Keep the default Author from scratch card selected. 
4. Enter name in the Name field (e.g. `AddPwaUser`). 
5. Select Node.js for the Runtime. 
6. Ensure `Use an existing role` is selected from the Permissions dropdown. 
7. Select the previously created role from the Existing Role dropdown (e.g. `PwaUsersLambda`). 
8. Click on Create function.
9. Edit the contents of [lambda.js](lambda.js) to add your data to the DynamoDB and then return a response.
10. Scroll down to the Function code section and replace the exiting code in the index.js code editor with your modified [lambda.js](lambda.js) file. 
11. Click "Save" in the upper right corner of the page.

### Step 4. Validate Your Implementation

For this module you will test the function that you built using the AWS Lambda console.
In the next module you will add a REST API with API Gateway so you can invoke your function from the browser-based application that you deployed in the first module.

1. From the main edit screen for your function, select Configure test event from the the Select a test event... dropdown. 
2. Keep Create new test event selected. 
3. Enter a name in the Event name field (e.g. `AddPwaUserEvent`) 
4. Modify, copy, and paste the following test event into the editor: 
    ```json
    {
        "path": "/pwausers",
        "httpMethod": "POST",
        "headers": {
            "Accept": "*/*",
            "content-type": "application/json; charset=UTF-8"
        },
        "queryStringParameters": null,
        "pathParameters": null,
        "body": "{\"fname\":\"Mickey\",\"lname\":\"Mouse\"}"
    }
    ```

5. Click Create. 
6. On the main function edit screen click Test with `TestRequestEvent` selected in the dropdown. 
7. Scroll to the top of the page and expand the Details section of the Execution result section. 
8. Verify that the execution succeeded and that the function result looks like the following: 
    ```json
    {
      "statusCode": 201,
      "body": "{\"PwaUserId\":\"6C-LRYNh42Hj3pdh4Ob5OA\",\"Firstname\":\"Mickey\",\"Lastname\":\"Mouse\",\"Message\":\"Successfully added user!\"}",
      "headers": {
        "Access-Control-Allow-Origin": "*"
      }
    }
    ```

### [Next Section >>>](../03-RESTfulAPI)