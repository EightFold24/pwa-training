**AWS Experience:** Beginner

**Time to complete:** 2 hours

**Cost to complete:**  Each service used in this architecture is eligible for the [AWS Free Tier](https://aws.amazon.com/free/). If you are outside the usage limits of the Free Tier, completing this tutorial will cost you less than $0.25*.

**Prerequisites:** To complete this tutorial, you will need:

- An AWS account**
- A text editor
- Recommended browser: The latest version of Chrome

*_This estimate assumes you follow the recommended configurations throughout the tutorial and terminate all resources within 24 hours._

_**Accounts that have been created within the last 24 hours might not yet have access to the resources required for this tutorial._

## Overview

In this tutorial, you'll create a simple serverless web application that enables users to request unicorn rides from the [Wild Rydes](http://www.wildrydes.com/) fleet. The application will present users with an HTML based user interface for indicating the location where they would like to be picked up and will interface on the backend with a RESTful web service to submit the request and dispatch a nearby unicorn. The application will also provide facilities for users to register with the service and log in before requesting rides.

## Application Architecture

The application architecture uses [AWS Lambda](https://aws.amazon.com/lambda/), [Amazon API Gateway](https://aws.amazon.com/apigateway/), [Amazon S3](https://aws.amazon.com/s3/), [Amazon DynamoDB](https://aws.amazon.com/dynamodb/), and [Amazon Cognito](https://aws.amazon.com/cognito/) as pictured below:

![Serverless Component Arcitecture](https://d1.awsstatic.com/Test%20Images/Kate%20Test%20Images/Serverless_Web_App_LP_assets-16.7cbed9781201a79b9efa761807c4312e68b23485.png)

1. **Static Web Hosting**
    
    Amazon S3 hosts static web resources including HTML, CSS, JavaScript, and image files which are loaded in the user's browser.  

2. **User Management**
    
    Amazon Cognito provides user management and authentication functions to secure the backend API.  

3. **Serverless Backend**
    
    Amazon DynamoDB provides a persistence layer where data can be stored by the API's Lambda function.  

4. **RESTful API**
    
    JavaScript executed in the browser sends and receives data from a public backend API built using Lambda and API Gateway.  

### Modules

This tutorial is broken up into five modules. You must complete each module before proceeding to the next. However, modules 1 and 2 have AWS CloudFormation templates available that you can use to launch the necessary resources without manually creating them yourself. The templates let you skip those modules.  

 

1. [Static Web Hosting]()
2. [User Management]()
3. [Serverless Backend]()
4. [RESTful APIs]()
5. [Resource Termination and Next Steps]()