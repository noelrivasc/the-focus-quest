---
title: Deploying a re-frame App
date: 2025-04-23
description: With a combination of AWS S3, CloudFront and GitHub Actions
tags:
  - Clojure
  - Technical Notes
---

## The Gist

Delightfully simple, since [shadow-cljs](https://shadow-cljs.github.io/docs/UsersGuide.html) takes care of most of the operation. It boils down to:

- Create a S3 Bucket
- Create a CloudFront Distribution
- Set bucket policies to allow CloudFront to access the content
- Set bucket policies to allow GitHub actions to sync files
- Set secrets and environment variables
- Create a GitHub build and deploy workflow

## GitHub Actions configuration

```yaml
on:
  push:
    branches: [ test-github-actions ]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    environment: prod

    steps:
      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY }}
          aws-secret-access-key: ${{ secrets.AWS_ACCESS_KEY_SECRET }}
          aws-region: ${{ vars.AWS_REGION }}

      - name: Checkout code
        uses: actions/checkout@v4

      - name: Use NodeJS 21.x
        uses: actions/setup-node@v4
        with:
          node-version: 21.x

      - name: Install npm dependencies
        run: npm install

      - name: Build release
        run: npm run release

      - name: Sync to S3
        run: |
          aws s3 sync ./resources/public s3://${{ vars.AWS_S3_BUCKET }} --delete
```

## The Result

So you can now see the app in all its glory: https://d3r6lgifjuis4q.cloudfront.net/. This is [the app repository](https://github.com/noelrivasc/cljs-wsid).

Yeah... that still needs work.
