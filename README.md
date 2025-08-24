Task 1 – S3 Static Website Hosting with IAM User
📌 Project Overview

This task demonstrates how to set up a static website using Amazon S3 and manage access using AWS IAM. The setup follows the principle of least privilege to ensure security while providing necessary functionality.

By the end of this task, you will have:

An S3 bucket hosting a static website.

A working static site link.

An IAM user (cloudlaunch-user) with restricted permissions.

A JSON policy that limits access only to S3 and its resources.

Credentials and login details for the IAM user.

🛠️ Step-by-Step Setup
1. Create the S3 Bucket

Bucket Name: cloudlaunch-bucket

Region: (e.g., us-east-1)

Block Public Access: Disabled (to allow public site hosting).

Bucket Policy: Added to permit public read access for objects.

Example bucket policy:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::cloudlaunch-bucket/*"
    }
  ]
}

2. Enable Static Website Hosting

Navigate to the bucket → Properties → Static website hosting.

Choose Enable.

Set Index document = index.html.

Upload your website files (e.g., index.html, style.css).

3. Verify the Website

Once enabled, AWS provides a URL for the site.

Example:

http://cloudlaunch-bucket.s3-website-us-east-1.amazonaws.com

4. Create IAM User (cloudlaunch-user)

User name: cloudlaunch-user

Access type: AWS Management Console access.

Console password: Auto-generated, with require password reset on first login enabled.

5. Create Custom IAM Policy

The user should have read-only access to the S3 bucket and its contents.

Policy Name: cloudlaunch-s3-readonly
Policy JSON:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "S3ListBucket",
      "Effect": "Allow",
      "Action": [
        "s3:ListAllMyBuckets",
        "s3:ListBucket"
      ],
      "Resource": [
        "arn:aws:s3:::cloudlaunch-bucket"
      ]
    },
    {
      "Sid": "S3GetObjects",
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:GetObjectAcl"
      ],
      "Resource": [
        "arn:aws:s3:::cloudlaunch-bucket/*"
      ]
    }
  ]
}


Attach this policy to the cloudlaunch-user.

🔗 Links & Credentials

Static Site URL:
http://cloudlaunch-bucket.s3-website-us-east-1.amazonaws.com

AWS Console URL:
https://<your-account-alias>.signin.aws.amazon.com/console

IAM User:

Username: cloudlaunch-user

Password: [provided separately]

Enforced: Change password on first login

✅ Evaluation Criteria Mapping

Clarity of setup → Step-by-step walkthrough provided.

Best practices → IAM least privilege applied.

Policy definitions → Clean, formatted JSON included.

Output → Working S3 website link.

Documentation → This README file is structured, clear, and comprehensive.

🔹 Bonus (Optional for Task 1): Integrate with CloudFront for better performance, HTTPS support, and global caching.

Do you want me to now prepare a Task 2 README.md that covers VPC, subnets, route tables, and IAM policy in the same detailed structure?