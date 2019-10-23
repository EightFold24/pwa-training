# Module 3. RESTful APIs

In this module you'll use Amazon API Gateway to expose the Lambda function you built in the previous module as a RESTful API. This API will be accessible on the public Internet. Using this configuration you will then turn your static website into a dynamic web application by adding client-side JavaScript that makes calls to the exposed APIs.  

## Architecture Overview

![](https://d1.awsstatic.com/Test%20Images/Kate%20Test%20Images/Serverless_Web_App_LP_assets-05.90540a6a2447e51cebdbb654c5c44d9344358b51.png)

The diagram above shows how the API Gateway component you will build in this module integrates with the existing components you built previously.
The grayed out items are pieces you have already implemented in other steps.

This module will focus on the steps required to build the cloud components of the API.

## Implementation Instructions

Follow the step-by-step instructions below to create your REST API.

### Step 1. Create a New REST API

1. In the AWS Management Console, click Services then select API Gateway under Application Services. 
2. Choose Create API. 
3. Select New API and enter an API Name (e.g. `PwaUsers`). 
4. Keep `Edge optimized` selected in the Endpoint Type dropdown.
_Note_: Edge optimized are best for public services being accessed from the Internet.
Regional endpoints are typically used for APIs that are accessed primarily from within the same AWS Region. 
5. Choose Create API

### Step 2. Create a new resource and method

Create a new resource within your API.
Then create a POST method for that resource and configure it to use a Lambda proxy integration backed by the lambda function you created in the first step of the previous module.

1. In the left nav, click on Resources under your API. 
2. From the Actions dropdown select Create Resource. 
3. Enter a Resource Name (e.g. `pwauser`). 
4. Ensure the Resource Path is set to the same (e.g. `pwauser`). 
5. Select Enable API Gateway CORS for the resource. 
6. Click Create Resource. 
7. With the newly created resource selected, from the Action dropdown select Create Method. 
8. Select `POST` from the new dropdown that appears, then click the checkmark. 
9. Select Lambda Function for the integration type. 
10. Check the box for Use Lambda Proxy integration. 
11. Select the Region you are using for Lambda Region. 
12. Enter the name of the lambda function you created in the previous module (e.g. `AddPwaUser`). 
13. Choose Save. Please note, if you get an error that your function does not exist, check that the region you selected matches the one you used in the previous module. 
14. When prompted to give Amazon API Gateway permission to invoke your function, choose OK. 

### Step 3. Deploy Your API

From the Amazon API Gateway console, choose Actions, Deploy API.
You'll be prompted to create a new stage.
You can use prod for the stage name.

1. In the Actions drop-down list select Deploy API. 
2. Select New Stage in the Deployment stage drop-down list. 
3. Enter `prod` for the Stage Name. 
4. Choose Deploy. 
5. Note the Invoke URL. You will use it in the next section.

### Step 4. Test Your API using Postman (Optional)

Before we try to update our website to interact with the deployed API, lets first test it out using something like [Postman](https://www.getpostman.com/). That way if something goes wrong when we implement it on our website, we can be sure it's not something wrong with the API. 

Postman is a great UI tool that aids in the development of APIs by allowing us to interact with them easily.

1. Download [Postman](https://www.getpostman.com/downloads)
2. Create a POST request using your URL endpoint.
3. Under the body tab, add the data that your webapp will be sending (e.g. `{"fname":"Mickey","lname":"Mouse"}`).
4. Under the Headers tab, add the Content-Type as application/json for good measure.
5. Send your request and ensure you get back the correct response.
    ```json
    {
        "PwaUserId": "6fZDN4DDqcHVDXMyYKoJ3Q",
        "Firstname": "Mickey",
        "Lastname": "Mouse",
        "Message": "Successfully added user!"
    }
    ```

### Step 5. Update the Website Config

Update the submission javascript in your website deployment to include the invoke URL of the stage you created in step 3. You should copy the invoke URL directly from the top of the stage editor page on the Amazon API Gateway console and paste it into your javascript.

1. Add the URL into your webapp either as a local constant in the javascript file that will execute the API call,
    ```js
    ENDPOINT = "https://rc7nyt4tql.execute-api.us-west-2.amazonaws.com/prod";
    ``` 
    or create a new javascript file `config.js` and add it to your index page.
    ```js
    window._config = {
        api: {
            invokeUrl: 'https://rc7nyt4tql.execute-api.us-west-2.amazonaws.com/prod',
        }
    };
    ```
2. Update your javascript to create a POST to your URL. There are a number of ways to do this in javascript. One way is to use the [XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest) object.
    ```js
    submitForm = function(form) {
        var xhttp = new XMLHttpRequest();
        xhttp.addEventListener("readystatechange", function () {
            if (this.readyState === 4) {
                console.log(JSON.stringify(form), " successfully written!");
                alert(this.responseText)
            }
        });
        xhttp.open("POST", ENDPOINT, true);
        xhttp.send(JSON.stringify(form));
    };
    ```
    Note that if you opted for the configuration method above, then the open function call should be `xhttp.open("POST", _config.api.invokeUrl, true);`

3. Save your changes locally. 

### Step 5. Validate your implementation

Note: You should ensure that you clear your browser cache before executing the following steps.

1. Run your website locally. 
2. Submit your form and see that an alert has shown with the contents of the response.

### [Next Section >>>](../04-Static-Website)