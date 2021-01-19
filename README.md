
# AWS S3 Upload - Uploading Objects Securely from Web-Application (Using Pre-Signed URLs)

### _About Pre-signed URLs:_
Pre-signed URLs are useful if you want your user/customer to be able to upload a specific object to your bucket, but you don't require them to have AWS security credentials or permissions.
When you create a pre-signed URL, you must provide your security credentials and then specify 
   a bucket name, 
   an object key, 
   an HTTP method (PUT for uploading objects), 
   and an expiration date and time.
The pre-signed URLs are valid only for the specified duration.


### _Implementation:_

User sends a POST request.
This request is received by an API Gateway.
API G/w forwards this request to a Lambda fn.
Lambda fn. computes an S3 signed URL, and sends back this signed URL to API G/w.
API G/w sends this "upload_url" to the user, so the user is able to upload the files using it.
User-uploaded file can now enter S3 bucket using the signed URL.


1. Creating an S3 Bucket:
  -  `my-secure-pvt-bkt`
  -  Enable `CORS` in bucket permission to add CORSRule `<AllowedMethod>POST</AllowedMethod>`   
  -  Upload index.html to the bucket, & make it `Public`
  
 2. Creating an IAM Role: 
  -  `s3-presign-lambda-role`
  -  Attach managed permissions:  `AWSLambdaExecute`
  
 3. Creating Lambda Fn.: 
  -  `s3-presign-lambda`
  -  Attach the IAM Role
  
 4. Creating API GW:
  -  `s3-presign-api`
  -  Create Method: `POST`
  -  Attach Lambda function as proxy
  - Enable CORS
     
 ---
    
  
  ##### _Reference:_
[1] - https://docs.aws.amazon.com/AmazonS3/latest/dev/PresignedUrlUploadObject.html


[2] - https://boto3.readthedocs.io/en/latest/guide/s3.html#generating-presigned-urls
