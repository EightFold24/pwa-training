# Module 4. RESTful APIs

In this module you'll use Amazon API Gateway to expose the Lambda function you built in the previous module as a RESTful API.
This API will be accessible on the public Internet.
It will be secured using the Amazon Cognito user pool you created in the previous module.
Using this configuration you will then turn your statically hosted website into a dynamic web application by adding client-side JavaScript that makes AJAX calls to the exposed APIs.  

## Architecture Overview

![](https://d1.awsstatic.com/Test%20Images/Kate%20Test%20Images/Serverless_Web_App_LP_assets-05.90540a6a2447e51cebdbb654c5c44d9344358b51.png)

The diagram above shows how the API Gateway component you will build in this module integrates with the existing components you built previously.
The grayed out items are pieces you have already implemented in previous steps.

The static website you deployed in the first module already has a page configured to interact with the API you'll build in this module.
The page at /ride.html has a simple map-based interface for requesting a unicorn ride.
After authenticating using the /signin.html page, your users will be able to select their pickup location by clicking a point on the map and then requesting a ride by choosing the "Request Unicorn" button in the upper right corner.

This module will focus on the steps required to build the cloud components of the API, but if you're interested in how the browser code works that calls this API, you can inspect the [ride.js](https://github.com/awslabs/aws-serverless-workshops/blob/master/WebApplication/1_StaticWebHosting/website/js/ride.js) file of the website.
In this case the application uses jQuery's [ajax()](https://api.jquery.com/jQuery.ajax/) method to make the remote request.  

## Implementation Instructions

Follow the step-by-step instructions below to create your REST API. Click on each step number to expand the section.

### Step 1. Create a New REST API

1. In the AWS Management Console, click Services then select API Gateway under Application Services. 
2. Choose Create API. 
3. Select New API and enter `WildRydes` for the API Name. 
4. Keep `Edge optimized` selected in the Endpoint Type dropdown.
_Note_: Edge optimized are best for public services being accessed from the Internet.
Regional endpoints are typically used for APIs that are accessed primarily from within the same AWS Region. 
5. Choose Create API

### Step 2. Create a Cognito User Pools Authorizer

Amazon API Gateway can use the JWT tokens returned by Cognito User Pools to authenticate API calls.
In this step you'll configure an authorizer for your API to use the user pool you created in [Module 2](https://aws.amazon.com/getting-started/projects/build-serverless-web-app-lambda-apigateway-s3-dynamodb-cognito/module-2/).

In the Amazon API Gateway console, create a new Cognito user pool authorizer for your API. Configure it with the details of the user pool that you created in the previous module. You can test the configuration in the console by copying and pasting the auth token presented to you after you log in via the /signin.html page of your current website.

1. Under your newly created API, choose Authorizers. 
2. Chose Create New Authorizer. 
3. Enter `WildRydes` for the Authorizer name. 
4. Select Cognito for the type. 
5. In the Region drop-down under Cognito User Pool, select the Region where you created your Cognito user pool in module 2 (by default the current region should be selected). 
6. Enter `WildRydes` (or the name you gave your user pool) in the Cognito User Pool input. 
7. Enter `Authorization` for the Token Source. 
8. Choose Create. 

**_Verify your authorizer configuration_**

1. Open a new browser tab and visit `/ride.html` under your website's domain. 
2. If you are redirected to the sign-in page, sign in with the user you created in the last module.
You will be redirected back to `/ride.html.` 
3. Copy the auth token from the notification on the `/ride.html`, 
4. Go back to previous tab where you have just finished creating the Authorizer 
5. Click Test at the bottom of the card for the authorizer. 
6. Paste the auth token into the Authorization Token field in the popup dialog. 
7. Click Test button and verify that the response code is 200 and that you see the claims for your user displayed.


### Step 3. Create a new resource and method

Create a new resource called /ride within your API.
Then create a POST method for that resource and configure it to use a Lambda proxy integration backed by the RequestUnicorn function you created in the first step of this module.

1. In the left nav, click on Resources under your WildRydes API. 
2. From the Actions dropdown select Create Resource. 
3. Enter `ride` as the Resource Name. 
4. Ensure the Resource Path is set to `ride`. 
5. Select Enable API Gateway CORS for the resource. 
6. Click Create Resource. 
7. With the newly created `/ride` resource selected, from the Action dropdown select Create Method. 
8. Select `POST` from the new dropdown that appears, then click the checkmark. 
9. Select Lambda Function for the integration type. 
10. Check the box for Use Lambda Proxy integration. 
11. Select the Region you are using for Lambda Region. 
12. Enter the name of the function you created in the previous module, `RequestUnicorn`, for Lambda Function. 
13. Choose Save. Please note, if you get an error that you function does not exist, check that the region you selected matches the one you used in the previous module. 
14. When prompted to give Amazon API Gateway permission to invoke your function, choose OK. 
15. Choose on the Method Request card. 
16. Choose the pencil icon next to Authorization. 
17. Select the WildRydes Cognito user pool authorizer from the drop-down list, and click the checkmark icon.

### Step 4. Deploy Your API

From the Amazon API Gateway console, choose Actions, Deploy API.
You'll be prompted to create a new stage.
You can use prod for the stage name.

1. In the Actions drop-down list select Deploy API. 
2. Select [New Stage] in the Deployment stage drop-down list. 
3. Enter `prod` for the Stage Name. 
4. Choose Deploy. 
5. Note the Invoke URL. You will use it in the next section.

### Step 5. Update the Website Config

Update the /js/config.js file in your website deployment to include the invoke URL of the stage you just created. You should copy the invoke URL directly from the top of the stage editor page on the Amazon API Gateway console and paste it into the _config.api.invokeUrl key of your sites /js/config.js file. Make sure when you update the config file it still contains the updates you made in the previous module for your Cognito user pool.

If you completed module 2 manually, you can edit the 

config.js file you have saved locally. If you used the AWS CloudFormation template, you must first download the 

config.js file from your S3 bucket. To do so, visit 

/js/config.js under the base URL for your website and choose File, then choose Save Page As from your browser.

1. Open the config.js file in a text editor. 
2. Update the invokeUrl setting under the api key in the config.js file. Set the value to the Invoke URL for the deployment stage your created in the previous section. An example of a complete 

config.js file is included below. Note, the actual values in your file will be different. 

window._config = {

    cognito: {

        userPoolId: 'us-west-2_uXboG5pAb', // e.g. us-east-2_uXboG5pAb         

        userPoolClientId: '25ddkmj4v6hfsfvruhpfi7n4hv', // e.g. 25ddkmj4v6hfsfvruhpfi7n4hv

        region: 'us-west-2' // e.g. us-east-2 

    }, 

    api: { 

        invokeUrl: 'https://rc7nyt4tql.execute-api.us-west-2.amazonaws.com/prod' // e.g. https://rc7nyt4tql.execute-api.us-west-2.amazonaws.com/prod, 

    } 

};  

1. Save your changes locally. 
2. In the AWS Management Console, choose Services then select S3 under Storage. 
3. Navigate to the website bucket and then browse to the 

js key prefix. 
4. Choose Upload. 
5. Choose Add files, select the local copy of 

config.js and then click Next. 
6. Choose Next without changing any defaults through the 

Set permissions and 

Set properties sections. 
7. Choose Upload on the 

Review section.

### Step 5. Validate your implementation

Note: It is possible that you will see a delay between updating the config.js file in your S3 bucket and when the updated content is visible in your browser. You should also ensure that you clear your browser cache before executing the following steps.

1. Visit `/ride.html` under your website domain. 
2. If you are redirected to the sign in page, sign in with the user you created in the previous module. 
3. After the map has loaded, click anywhere on the map to set a pickup location. 
4. Choose Request Unicorn. You should see a notification in the right sidebar that a unicorn is on its way and then see a unicorn icon fly to your pickup location.