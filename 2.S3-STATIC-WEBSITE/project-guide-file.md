# PROJECT-1(Static Website Hosting-using-s3)
![image](https://github.com/user-attachments/assets/bbae8e41-c6a6-4eea-92b5-42494c81e526)


## step1:

In the AWS console go to search bar and type S3, then click on create bucket

![image](https://github.com/user-attachments/assets/1834107e-1058-4fec-a147-e5ea8415502a)

## You will want to create a bucket name, it must be unique and not previously used

# You will scroll down to Block Public Access settings for this bucket, you will uncheck Block all public access, check that you acknowledge the warning

![image](https://github.com/user-attachments/assets/ef0d22f0-bde3-46bd-97f2-6c9cb1f0740c)

Leave everything else default, You can now create your bucket

# you select upload, you will select add file with index.html file
![image](https://github.com/user-attachments/assets/cc65dd7c-daf1-434a-9cab-6c39aa4b072c)


# Set Permissions

Modify the bucket permissions to allow public read access to your files. This is usually done by setting a bucket policy.

# Example bucket policy:
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


scroll down to bucket policy, and select edit
we will paste code it in the Bucket policy section
select YOUR-BUCKET-ARN and replace with our own bucket name
go up to Bucket ARN and copy the text we will input it between “ /*”

![image](https://github.com/user-attachments/assets/f7f97744-0a6d-4b4a-ab02-ece1abcaaa3d)

# copy the url and hit on broser 

![Screenshot (196)](https://github.com/user-attachments/assets/e3859e05-3e33-4635-892f-adf0df13553a)

# Your going to click on your newly created bucket name select properties

# Static website hosting, you want that option enabled, also make sure host static website is selected

![image](https://github.com/user-attachments/assets/46501c95-b61c-4a8e-bf32-f4cea9622ad6)

# At this point you will also want the index document section to have the file we up index.html in the box and changes saved
![image](https://github.com/user-attachments/assets/327758f1-18aa-4112-ae67-0263a72ddb4d)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------



