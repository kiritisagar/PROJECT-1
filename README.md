# PROJECT-1(Static Website Hosting-using-s3)
![image](https://github.com/user-attachments/assets/bbae8e41-c6a6-4eea-92b5-42494c81e526)

![image](https://github.com/user-attachments/assets/687c7e61-f001-4031-9575-08354802235d)

Create an S3 Bucket

Log in to your AWS Management Console.
Navigate to S3 and create a new bucket.
Give your bucket a unique name (e.g., my-static-website-bucket) and choose the appropriate AWS region.
Configure the Bucket for Website Hosting

Enable static website hosting in the S3 bucket properties.
Specify the index.html file as the entry point and optionally an error.html for handling errors.
Set up the necessary bucket policy to allow public access (be cautious with this step).
Upload Website Files

Upload all your static website files (HTML, CSS, JavaScript, images) to the S3 bucket.
Ensure that the index.html file is in the root directory of the bucket.
Set Permissions

Modify the bucket permissions to allow public read access to your files. This is usually done by setting a bucket policy.

Example bucket policy:
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-static-website-bucket/*"
    }
  ]
}

