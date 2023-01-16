#!/bin/bash
mc admin user add minio loki $LOKI_S3_PASSWORD
mc mb minio/loki
mc admin policy add minio loki-private loki-user-policy.json
mc admin policy set minio loki-private user=loki



{
  "Version": "2012-10-17",
  "Statement": [
      {
          "Action": [
              "s3:*"
          ],
          "Effect": "Allow",
          "Resource": ["arn:aws:s3:::loki/*", "arn:aws:s3:::loki"],
          "Sid": ""
      }
  ]
}
