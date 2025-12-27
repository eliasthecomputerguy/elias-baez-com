# elias-baez-com
Repo for elias-baez.com

## Hosting my resume

My resume is hosted on **S3**.

I use **CloudFront** to terminate my **ACM** SSL Certificate and redirect HTTP requests.

Then I use **CodePipeline** to detect changes in my Git repo and automatically push them into **S3**.