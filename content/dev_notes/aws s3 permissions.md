---
title: "aws s3 permissions"
enableToc: false
date: "2023-07-05"
lastmod: :git
tags:
- aws
---

```
{
    "Version": "2008-10-17",
    "Statement": [
        {
            "Sid": "AllowPublicRead",
            "Effect": "Allow",
            "Principal": {
                "AWS": "*"
            },
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::ecom-testt/images/*"
            ]
        }
    ]
}
```
Use the [policy generator](https://awspolicygen.s3.amazonaws.com/policygen.html)
to create this configuration.

The resource name "ARN" should be available on the bucket policy edit page.

Then name can be thought of as a directory path. To specify a directory, modify
the path to point to the directory. To apply the configuration for all
s3 objects in the directory add `/*`. 