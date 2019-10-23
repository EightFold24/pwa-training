# Module 1. Static Web Hosting

In this module you'll configure Amazon Simple Storage Service (S3) to host the static resources for your web application.

## Architecture Overview

The architecture for this module is very straightforward. All of your static web content including HTML, CSS, JavaScript, images and other files will be stored in Amazon S3. Your end users will then access your site using the public website URL exposed by Amazon S3. You don't need to run any web servers or use other services in order to make your site available.

For the purposes of this module you'll use the Amazon S3 website endpoint URL that we supply. It takes the form `http://{your-bucket-name}.s3-website.{region}.amazonaws.com`. For most real applications you'll want to use a custom domain to host your site. More information on how to use your own domain can be found in the following instructions for [setting up a static website using a custom domain in the Amazon S3 documentation.](http://docs.aws.amazon.com/AmazonS3/latest/dev/website-hosting-custom-domain-walkthrough.html)

### Step 1. Create an S3 Bucket

Amazon S3 can be used to host static websites without having to configure or manage any web servers. In this step you'll create a new S3 bucket that will be used to host all of the static assets (e.g. HTML, CSS, JavaScript, and image files) for your web application. 

Keep in mind that your bucket's name must be globally unique. We recommend using a name like `pwa-training-webapp-firstname`. Add you name onto the end of the bucket name to keep the bucket name unique.

1. In the AWS Management Console choose Services then select S3 under Storage.
2. Choose Create Bucket
3. Provide a globally unique name for your bucket such as `pwa-training-webapp-firstname`. If you get an error that your bucket name already exists, try adding additional numbers or characters until you find an unused name.
4. Select the Region you've chosen to use for this workshop from the dropdown.
5. Choose Create in the lower left of the dialog without selecting a bucket to copy settings from.

### Step 2. Upload Content

In this step, you will upload the website assets for this module to your S3 bucket via the AWS Management Console (requires the latest version of Google Chrome browser).

1. Open the AWS Management Console in Chrome. Choose Services then select S3 under Storage. 
2. Select the bucket you created in the previous step and ensure you are viewing the Overview tab. 
5. Open either Windows File Explorer or macOS Finder and browse to your website project folder. 
7. Select all of the files and subdirectories. 
8. Drag and drop the selected files from your local filesystem to the content under the Overview tab in the S3 console. 
9. Choose Upload in the lower left of the dialog box that appears. 
10. Wait for the upload to complete, and ensure you see the contents of the website directory listed in the S3 console. 

### Step 3. Add a Bucket Policy to Allow Public Reads

You can define who can access the content in your S3 buckets using a bucket policy. Bucket policies are JSON documents that specify what principals are allowed to execute various actions against the objects in your bucket.

In this step, you will add a bucket policy to your new Amazon S3 bucket to let anonymous users view your site. By default your bucket will only be accessible by authenticated users with access to your AWS account.

See [this example](http://docs.aws.amazon.com/AmazonS3/latest/dev/example-bucket-policies.html#example-bucket-policies-use-case-2) of a policy that will grant read only access to anonymous users. This example policy allows anyone on the Internet to view your content. The easiest way to update a bucket policy is to use the console. Select the bucket, choose the permission tab and then select Bucket Policy.  

1. In the S3 console, select the name of the bucket you created in section 1.
2. Choose the Permissions tab, then choose Bucket Policy.
    1. In the S3 console, select the name of the bucket you created in section 1.
    2. Choose the Permissions tab, then make sure Block public access is selected.
    3. Untick Block all public access, and choose Save.
    5. In the confirmation modal that appears, type 'confirm' and then click Confirm. 
    6. While still in the Permissions tab, choose Bucket Policy.  

3. Enter the following policy document into the bucket policy editor replacing `[YOUR_BUCKET_NAME]` with the name of the bucket you created in section 1:  
    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow", 
                "Principal": "*", 
                "Action": "s3:GetObject", 
                "Resource": "arn:aws:s3:::[YOUR_BUCKET_NAME]/*" 
            } 
        ] 
    }
    ```

1. Choose Save to apply the new policy.

### Step 3. Enable Website Hosting

By default objects in an S3 bucket are available via URLs with the structure http://.amazonaws.com//. In order to serve assets from the root URL (e.g. /index.html), you'll need to enable website hosting on the bucket. This will make your objects available at the AWS Region-specific website endpoint of the bucket: .s3-website-.amazonaws.com.

You can also use a custom domain for your website. For example http://www.wildrydes.com is hosted on S3. Setting up a custom domain is not covered in this workshop, but you can find detailed instructions in our [documentation](http://docs.aws.amazon.com/AmazonS3/latest/dev/website-hosting-custom-domain-walkthrough.html).

In this step, you will use the console to enable static website hosting. You can do this on the Properties tab after you've selected the bucket. Set `index.html` as the index document, and leave the error document blank. See the documentation on [configuring a bucket for static website](https://docs.aws.amazon.com/AmazonS3/latest/dev/HowDoIWebsiteConfiguration.html) hosting for more details.  

1. From the bucket detail page in the S3 console, choose the Properties tab.
2. Choose the Static website hosting card.
3. Select Use this bucket to host a website and enter `index.html` for the Index document. Leave the other fields blank.
4. Note the Endpoint URL at the top of the dialog before choosing Save. You will use this URL throughout the rest of the workshop to view your web application. From here on this URL will be referred to as your website's base URL.
5. Click Save to save your changes.

### Step 4. Validate your implementation

After completing these implementation steps you should be able to access your static website by visiting the the website endpoint URL for your S3 bucket.

Visit your website's base URL (this is the URL you noted in the prior section) in the browser of your choice. You should see the Wild Rydes home page displayed. If you need to lookup the base URL, visit the S3 console, select your bucket and then click the Static Web Hosting on the Properties tab.

If the page renders correctly (see below for an example screenshot), you can move on to the next module User Management.

### [Next Section >>>](../05-Cleanup)