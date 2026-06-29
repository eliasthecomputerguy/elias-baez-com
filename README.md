# elias-baez.com

Source for my personal resume site, live at **https://elias-baez.com**.

The site itself is a single, dependency-free `index.html` (no framework, no build
step). The part worth looking at is how it ships: a fully automated, serverless
deployment pipeline on AWS.

## Architecture

```
   git push
      |
      v
  AWS CodePipeline  ->  Amazon S3 (static site origin)
                              |
                              v
                       Amazon CloudFront (CDN + TLS via ACM)
                              |   HTTPS, with HTTP redirected to HTTPS
                              v
                          Visitors
```

## How it's deployed

- **Amazon S3** stores the static site and serves as the origin.
- **Amazon CloudFront** sits in front as the CDN, terminates TLS using an
  **AWS Certificate Manager (ACM)** certificate, and redirects all HTTP requests
  to HTTPS.
- **AWS CodePipeline** watches this Git repository and, on every push, automatically
  syncs the latest `index.html` into the S3 bucket. No manual uploads, no servers
  to manage, and no build artifacts to babysit.
