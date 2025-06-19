# 🔒 AWS Security Assessment Project
Documenting real cloud vulnerabilities in controlled environment

## Project Overview
Conducted security assessment of AWS environment to identify misconfigurations and vulnerabilities using native tools like GuardDuty and CloudTrail.

## Generated Security Events
- **25 failed IAM login attempts** simulating brute-force attacks
- **Public S3 bucket created:** `` `insecure-bucket-1750833295` ``
  - Intentionally configured with:
    ```bash
    BlockPublicAcls=false
    IgnorePublicAcls=false
    BlockPublicPolicy=false
    RestrictPublicBuckets=false
    ```

## Expected GuardDuty Findings
1. `UnauthorizedAccess:IAMUser`
2. `Policy:S3/BucketPublic`
3. `S3:PublicBucket`

## Evidence
Screenshots will be added here once GuardDuty findings appear

## Remediation Steps
```bash
# Secure public buckets:
aws s3api put-public-access-block \
    --bucket insecure-bucket-1750833295 \
    --public-access-block-configuration \
    "BlockPublicAcls=true, IgnorePublicAcls=true, BlockPublicPolicy=true, RestrictPublicBuckets=true"

# Delete test user (after assessment):
aws iam delete-user --user-name TestSecurityUser
```
