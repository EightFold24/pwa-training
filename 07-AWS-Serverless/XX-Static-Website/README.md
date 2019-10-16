# Module 1. Static Web Hosting

In this module you'll configure Amazon Simple Storage Service (S3) to host the static resources for your web application. In subsequent modules you'll add dynamic functionality to these pages using JavaScript to call remote RESTful APIs built with AWS Lambda and Amazon API Gateway.  

## Architecture Overview

The architecture for this module is very straightforward. All of your static web content including HTML, CSS, JavaScript, images and other files will be stored in Amazon S3. Your end users will then access your site using the public website URL exposed by Amazon S3. You don't need to run any web servers or use other services in order to make your site available.

For the purposes of this module you'll use the Amazon S3 website endpoint URL that we supply. It takes the form `http://{your-bucket-name}.s3-website.{region}.amazonaws.com`. For most real applications you'll want to use a custom domain to host your site. If you're interested in using a your own domain, follow the instructions for [setting up a static website using a custom domain in the Amazon S3 documentation.](http://docs.aws.amazon.com/AmazonS3/latest/dev/website-hosting-custom-domain-walkthrough.html)

### Step 1. Select a Region
This web application can be deployed in any AWS region that supports all the services used in this application, which include Amazon Cognito, AWS Lambda, Amazon API Gateway, Amazon S3 and Amazon DynamoDB.

You can refer to the [region table](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) to see which regions have the supported services. Among the supported regions you can choose are:

- US East (N. Virginia)
- US East (Ohio)
- US West (Oregon)
- EU (Frankfurt)
- EU (Ireland)
- EU (London)
- Asia Pacific (Tokyo)
- Asia Pacific (Seoul)
- Asia Pacific (Sydney)
- Asia Pacific (Mumbai)
 
Select your region from the dropdown in the upper right corner of the AWS Management Console.

![](https://d1.awsstatic.com/Getting%20Started/learning-paths/serverless%20web%20application/region.69a7598862b05a8d166ac34108eb6f25f5a90844.png)

### Step 2. Create an S3 Bucket

Amazon S3 can be used to host static websites without having to configure or manage any web servers. In this step you'll create a new S3 bucket that will be used to host all of the static assets (e.g. HTML, CSS, JavaScript, and image files) for your web application. 

In this step, you will use the console or AWS CLI to create an Amazon S3 bucket. Keep in mind that your bucket's name must be globally unique. We recommend using a name like `wildrydes-firstname-lastname`. If you get an error that your bucket name already exists, try adding additional numbers or characters until you find an unused name.

1. In the AWS Management Console choose Services then select S3 under Storage.
2. Choose +Create Bucket
3. Provide a globally unique name for your bucket such as `wildrydes-firstname-lastname`. If you get an error that your bucket name already exists, try adding additional numbers or characters until you find an unused name.
4. Select the Region you've chosen to use for this workshop from the dropdown.
5. Choose Create in the lower left of the dialog without selecting a bucket to copy settings from.

### Step 3. Upload Content

In this step, you will upload the website assets for this module to your S3 bucket. You can use the AWS Management Console (requires Google Chrome browser), AWS CLI, or the provided CloudFormation template to complete this step. If you already have the [AWS CLI installed and configured on your local machine](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-set-up.html), we recommend using that method. Otherwise, use the console if you have the latest version of Google Chrome installed. 

**Console step-by-step instructions**

In order to upload all files and subdirectories in a local directory via the AWS Management Console, you must use the latest version of the Chrome web browser. If you cannot use Chrome, please follow the instructions for using either the AWS CLI or the provided CloudFormation template.

1. Download an archive of this repository using [this link](https://github.com/awslabs/aws-serverless-workshops/archive/master.zip). 
2. Unzip the archive you downloaded on your local machine. 
3. Open the AWS Management Console in Chrome. Choose Services then select S3 under Storage. 
4. Select the bucket you created in the previous step and ensure you are viewing the Overview tab. 
5. Open either Windows File Explorer or macOS Finder and browse to the expanded contents of the zip file you downloaded in the first step. 
6. Browse to the WebApplication/1_StaticWebHosting/website directory on your local machine. 
7. Select all of the files and subdirectories under the website directory. Ensure that the website directory itself is not selected. 
8. Drag and drop the selected files from your local filesystem to the content under the Overview tab in the S3 console. 
9. Choose Upload in the lower left of the dialog box that appears. 
10. Wait for the upload to complete, and ensure you see the contents of the website directory listed in the S3 console. If you only see a single 

website directory, you should delete it from your bucket and follow these instructions again ensuring that you select only the contents of the directory before dragging and dropping into the S3 console. 

**CLI step-by-step instructions**

If you already have the CLI installed and configured, you can use it to copy the necessary web assets from `s3://wildrydes-us-east-1/WebApplication/1_StaticWebHosting/website to your bucket`.

1. Execute the following command making sure to replace `YOUR_BUCKET_NAME` with the name you used in the previous section and `YOUR_BUCKET_REGION` with the region code (e.g. us-east-2) where you created your bucket. `aws s3 sync s3://wildrydes-us-east-1/WebApplication/1_StaticWebHosting/website s3://YOUR_BUCKET_NAME --region YOUR_BUCKET_REGION`
2. If the command was successful, you should see a list of objects that were copied to your bucket. 


**CloudFormation step-by-step instructions**

If you are unable to use either of the previous methods, you can launch the provided CloudFormation template in order to copy the necessary assets into your S3 bucket. Launch a CloudFormation template by selecting a region and clicking Launch stack link in the [CloudFormation Template section of this module. ](https://aws.amazon.com/getting-started/projects/build-serverless-web-app-lambda-apigateway-s3-dynamodb-cognito/module-1/#template)

### Step 4. Enable Website Hosting

By default objects in an S3 bucket are available via URLs with the structure http://.amazonaws.com//. In order to serve assets from the root URL (e.g. /index.html), you'll need to enable website hosting on the bucket. This will make your objects available at the AWS Region-specific website endpoint of the bucket: .s3-website-.amazonaws.com.

You can also use a custom domain for your website. For example http://www.wildrydes.com is hosted on S3. Setting up a custom domain is not covered in this workshop, but you can find detailed instructions in our [documentation](http://docs.aws.amazon.com/AmazonS3/latest/dev/website-hosting-custom-domain-walkthrough.html).

In this step, you will use the console to enable static website hosting. You can do this on the Properties tab after you've selected the bucket. Set `index.html` as the index document, and leave the error document blank. See the documentation on [configuring a bucket for static website](https://docs.aws.amazon.com/AmazonS3/latest/dev/HowDoIWebsiteConfiguration.html) hosting for more details.  

1. From the bucket detail page in the S3 console, choose the Properties tab.
2. Choose the Static website hosting card.
3. Select Use this bucket to host a website and enter `index.html` for the Index document. Leave the other fields blank.
4. Note the Endpoint URL at the top of the dialog before choosing Save. You will use this URL throughout the rest of the workshop to view your web application. From here on this URL will be referred to as your website's base URL.
5. Click Save to save your changes.

### Step 5. Validate your implementation

After completing these implementation steps you should be able to access your static website by visiting the the website endpoint URL for your S3 bucket.

Visit your website's base URL (this is the URL you noted in the prior section) in the browser of your choice. You should see the Wild Rydes home page displayed. If you need to lookup the base URL, visit the S3 console, select your bucket and then click the Static Web Hosting on the Properties tab.

If the page renders correctly (see below for an example screenshot), you can move on to the next module User Management.