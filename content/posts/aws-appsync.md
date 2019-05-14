---
title: "Overview of AWS AppSync"
date: 2019-04-11T20:24:55-04:00
draft: true
---

I recently learned about [AWS AppSync](https://aws.amazon.com/appsync/) while perusing A Cloud Guru
courses and stumbling on this one: ["Introduction to AWS AppSync"](https://acloud.guru/learn/intro-aws-appsync). 
I am excited! AppSync is a managed service for deploying GraphQL APIs. Think of it like 
[API Gateway](https://aws.amazon.com/api-gateway/) but for GraphQL instead of HTTP requests.

GraphQL is to AppSync as HTTP is to API Gateway.


From the course learnin and my trials so far, the workflow breaksdown like this:

1. Upload a GraphQL schema document
2. Configure data sources
3. Map schema to data sources with resolvers 

Let's do a quick dive into each.  I am gonna cheat and not go into a couple topics: authentication and
querying. I'll save those for other posts.  But I am happy that AppSync supports AWS Cognito out-of-the-box.

## Upload a GraphQL Schema Document

You create a GraphQL schema of the same format explained by the official [schema docs](https://graphql.github.io/learn/schema/)
namely:

A. Declare types
B. Declare queries, mutations, subscriptions

GraphQL is strongly typed. It has some built-in data types like `ID`, `String`, `Boolean`, `Int`, etc.
AWS also included some [custom types](https://docs.aws.amazon.com/appsync/latest/devguide/scalars.html)
like `AWSDate`, `AWSEmail`, and `AWSPhone` that are automatically validated.

A simple schema could look like this:

```graphql
// List out the types for your models
type User {
  id: ID!  // Exlamation point denotes a required field
  name: String!
  email: AWSEmail!
}

type Comment {
  id: ID!
  author: User
  content: String
  post_time: AWSDateTime
}

type Post {
  id: ID!
  title: String!
  content: String!
  comments: [Comment] // Square brackets denote an array
}

// List out your inputs; complex parameters passed to functions
input PostInput {
  id: ID!
  title: String!
  content: String!
  comments: [Comment]
}

input UserInput {
  id: ID!
  name: String!
  email: AWSEmail!
}

// All the queries (reads) that can be done - RPC style!
type Query {
  getUser(id: ID!): User
  listUsers: [User]
  getPost(id: ID!): Post
  listPosts: [Posts]
}

// All the mutations (writes) that can be done - RPC style!
type Mutation {
  createPost(input: PostInput): Post
  createUser(input: UserInput): User
}

// Your API Schema declaration!!!
schema {
  query: Query
  mutation: Mutation
}
```

## Configure Data Sources

AppSync has the ability to connect directly to backend services. So far, it can connect to the following
sources:

1. Dynamo tables
2. Lambda functions
3. AWS Elasticsearch domain 
4. RDS (only Aurora so far)
5. Arbitrary HTTP endpoint
 
Dynamo tables and Lambda functions will be your bread and butter data sources. GraphQL data can be stored
easily as JSON, which makes Dynamo a natural choice. Then Lambda fills the slot for most your other 
important side effects (sending emails/texts/notifications, generating reports from multiple tables, 
or hitting external API endpoints).

 
## Map Schema to Data Sources with Resolvers

Resolvers is a common concept for GraphQL backends, but AppSync's implementation is pretty unique.
A resolver attaches one of your schema fields (usually a Query or Mutation field) to a data source.
To do this, it 
In the case of DynamoDB
by indicating to the AppSync engine how to map your data into a 

## Conclusion
