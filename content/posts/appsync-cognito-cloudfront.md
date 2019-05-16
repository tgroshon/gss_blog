---
title: "Appsync Cognito Cloudfront"
date: 2019-05-13T20:44:15-04:00
draft: true
categories:
  - DevOps
  - Web Development
tags:
  - AWS
  - Serverless
  - GraphQL
  - AppSync
  - JavaScript
  - Terraform
---

## Introduction

Serverless architecture, despite the click-baity and inaccurate name, has interested me for the last
couple years. I love how it takes the on-demand and pay-for-what-you-use quality of the cloud and
breaks that down to the request level. Because AWS is my preferred cloud provider, [Lambda](https://aws.amazon.com/lambda/)
is a key part of many of my projects. Usually, I couple Lambda with [API Gateway](https://aws.amazon.com/api-gateway/)
which acts as the HTTP proxy mapping web endpoints to Lambda functions. That works great for
HTTP API's and I recommend it.

However, what if you want to get new-agey and deploy a [GraphQL](https://graphql.org) API?
If you aren't sure what GraphQL is, you should check official website which has a great tutorial.
So now that you got the basic picture of GraphQL, how could you deploy it in AWS? You can make that
work with API Gateway but it's a little cludgey and normally results in implementing a super Lambda
function that contains all your GraphQL resolver logic.

Lucky us! AWS has a GraphQL specific API proxy called AppSync.
Last month, I did an [article overviewing AppSync]({{< ref "aws-appsync.md" >}}) and concluded
I would try it out on an upcoming project. Well dear reader, I have done it and now I am bringing
you my results!

## Building a React SPA with Amplify

### Amplify Lib & CLI


### Amplify Console

## Replacing Amplify with Terraform and Serverless

### Terraform Scripts

### Serverless

## Conclusion
