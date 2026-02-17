# Deployment Guide: Ceja Family Daycare

This document outlines the steps to deploy the Ceja Family Daycare website to AWS using S3 and CloudFront with the `mediusa` profile.

## Infrastructure Details
- **S3 Bucket**: `ceja-family-daycare-production`
- **CloudFront Distribution ID**: `ELQBUBW41VDQD`
- **Live URL**: `https://d27kl9dh2k5ieb.cloudfront.net`
- **AWS Profile**: `mediusa`

## Prerequisites
Ensure the AWS CLI is installed and the `mediusa` profile is configured:
```bash
aws configure --profile mediusa
```

## Deployment Steps

### 1. Sync Files to S3
Upload only the necessary assets, ensuring that we exclude any project configuration files.
```bash
aws s3 sync ./ s3://ceja-family-daycare-production --profile mediusa --exclude ".git/*" --exclude ".DS_Store" --exclude "bucket-policy.json" --exclude "DEPLOYMENT.md"
```

### 2. Invalidate CloudFront Cache
Clear the cache to ensure the latest changes are visible immediately.
```bash
aws cloudfront create-invalidation --distribution-id ELQBUBW41VDQD --paths "/*" --profile mediusa
```

## Maintenance Patterns
- Files should be served as public via S3 Bucket Policy (already configured).
- Content headers should be centered as per sitewide design patterns.
- Always verify the site on localhost:8000 before syncing to production.
