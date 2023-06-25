# Static Site Template

## What is it?

This repo contains an AWS CloudFormation template for hosting static assets. The relevant stack components are:

* S3 for actually housing the assets,
* CloudFront for providing SSL connectivity and domain name handling (and CDN capabilities),
* Route53 for supporting DNS records, and
* AWS Certificate Manager (ACM) for SSL certificate generation (and renewal).


## Why would I use it?

This is a managed strategy for hosting static assets. No servers to manage; AWS S3 and CloudFront are used to host your website / assets.

## How much does it cost?

I dunno, man. Not much? In my experience it's usually a couple bucks a month, but I mainly have near-zero traffic sites. As your traffic increases you'll need to pay more due to AWS billing policies. This is mainly meant to remove any hurdles to getting something online (while being able to tweak all the knobs). Your mileage may vary.

If you're like me and have low-traffic sites the biggest cost-center each month is going to be the Route53 Hosted Zone (at like $1 or $2 a month).

## Prerequisites

### An AWS Account

This is necessary to invoke a CloudFormation template and create infrastructure.

### Domain Name Registered with AWS

This setup assumes HTTPS configuration with your domain name with a certificate managed via ACM. As a consequnce your domain must be registered through AWS to facilitate ACM certificate creation and renewal.

### The AWS CLI

While there are several ways to interact with AWS, this example will be using the [AWS command line interface (CLI)](https://aws.amazon.com/cli/).


## Creating the Infrastructure

1. `aws cloudformation deploy --stack-name camp-cedar-street-base --template-file ./dns.yml --parameter-overrides FullDomainName=campcedarstreet.com`
2. `aws cloudformation deploy --stack-name camp-cedar-street --template-file ./hosting.yml --parameter-overrides HostedZoneIDParameter=Z02534341NQJNQ9SMOGI8 FullDomainName=campcedarstreet.com`
