# Deploy Static Website on AWS

In this project, I've developed and deployed a static website to AWS using S3, CloudFront, and IAM.

The files included are: 

1. index.html - The Index document for the website.

2. /img - The background image file for the website.

3. /vendor - Bootssrap CSS framework, Font, and JavaScript libraries needed for the website to function.

4. /css - CSS files for the website.


# Steps to configuring AWS:

## Create an S3 Bucket

1. Go to the "AWS Management Console" page, enter "S3" in the "Find Services" field, then select "S3".

2. The Amazon S3 dashboard appears. Click on "Create a compartment".

3. Fill the Origin name the parameters

4. In the Bucket settings for blocking public access section , uncheck the "Block all public access" checkbox. This will enable public access to objects in the bucket via the S3 object URL.

5. Click on “Next”, then on “Create a compartment”.

6. Once the bucket is created, click the bucket name to open the bucket to the content.

## Upload files to S3 bucket

1. Check the AWS CLI configuration. If not already configured, type:

aws configure list
aws configure
aws configure set aws_session_token "<TOKEN>" --profile default

2. Upload files
Créez un compartiment PUBLIC dans le S3, et vérifiez-le localement en saisissant
```
aws s3api list-buckets
```

Téléchargez et décompressez le fichier udacity-starter-website.zip
```
cd udacity-starter-website
```
Déposez un seul fichier.
```
aws s3api put-object --bucket my-bucket-202203081 --key index.html --body index.html
```
Copiez les dossiers du disque local vers S3
```
aws s3 cp vendor/ s3://my-bucket-202203081/vendor/ --recursive
aws s3 cp css/ s3://my-bucket-202203081/css/ --recursive
aws s3 cp img/ s3://my-bucket-202203081/img/ --recursive
```

## Secure the bucket through IAM

1. Click on the “Permissions” tab.

2. The Bucket Policy section shows as empty. Click the Edit button.

3. Enter the following bucket policy replacing your-websitewith the name of your bucket and click "Save".


## Configure an S3 Bucket
1. Go to the Properties tab , then scroll down to edit the Static Website Hosting section .

2. Click on the “Edit” button to display the Edit Static Website Hosting screen . Now enable the Static Website Hosting option and fill in the default homepage and error page for your website.

3. Enter "index.html" for both "Index Document" and "Error Document", then click "Save". Once the settings have been saved, check the Static Website Hosting section under the Properties tab again . You should now be able to see the website endpoint , as shown below:


## Distribute website through CloudFront

1. Select "Services" in the upper left corner and type "cloud front" in the "Find a service by name or feature" text box, then select "CloudFront".
2. In the CloudFront dashboard, click "Create a distribution".
3. Under 'Select a distribution method for your content', click 'Get started'.
4. To create a distribution, use the following information:

Origin > Domain name	Do not select the bucket from the drop-down list, but paste the static website hosting endpoint as<bucket-name>.s3-website-region.amazonaws.com

Origin > Activer Origin Shield	Non

Default Cache Behavior	Use default settings	

Cache Key and Origin Requests	Use default settings

5. For the rest of the options, keep the default values ​​and click "Create distribution". Creating the CloudFront distribution can take up to 10 minutes.

6. As soon as your distribution's status changes from "In Progress" to "Deployed", copy the URL of your CloudFront distribution's endpoint from the "Domain Name" column.

7. In this example, the domain name value is dgf7z6g067r6d.cloudfront.net, but yours will be different.


## Access website in web browser

1. Open a web browser like Google Chrome, and paste the copied CloudFront domain name (for example, dgf7z6g067r6d.cloudfront.net) without adding /index.html at the end. The CloudFront domain name should show you the contents of the default home page, as shown below:

2. Access the website through the site endpoint, for example http://<bucket-name>.s3-website.us-east-2.amazonaws.com/.

3. Access the bucket object via its S3 object URL, for example https://<bucket-name>.s3.amazonaws.com/index.html. 