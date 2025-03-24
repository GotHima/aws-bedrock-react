# Travel Destination Recommender

1. [Background](#background)
   - [Tech stack](#tech-stack)
   - [AWS services used (via Amplify)](#aws-services-used-via-amplify)
2. [AWS account setup](#aws-account-setup)
   - [Amazon Bedrock](#amazon-bedrock)
   - [AWS CLI](#aws-cli)
3. [Contents in this repo](#contents-in-this-repo)
   - [1. AWS Amplify](#1-aws-amplify)
   - [2. React UI](#2-react-ui)
4. [How to run the app](#how-to-run-the-app)
   - [First time](#first-time)
   - [Development](#development)
   - [[Optional] Deployment](#optional-deployment)

## Background

This app was created based on the tutorial:  
https://aws.amazon.com/getting-started/hands-on/build-serverless-web-app-lambda-amplify-bedrock-cognito-gen-ai/

### Tech stack

- AWS Amplify
- AWS services
- React

### AWS services used (via Amplify)

- Bedrock
- Cognito
- Lambda
- AppSync

## AWS account setup

### Amazon Bedrock

- go to Amazon Bedrock service in AWS console
- choose 'Claude 3 Sonnet' from model catalog
- request for access

### AWS CLI

- log in your AWS account locally via `aws configure`

## Contents in this repo

### 1. AWS Amplify

- source folder `amplify/` (created by `npm create amplify@latest -y`)
- `data/bedrock.js`
  - code for Lambda functions
  - `request()`: constructs a POST request using user-provided input (prompt) and forward it to Bedrock
  - `response()`: parses the response from Bedrock and returns it to client
- `backend.ts`
  - adds Bedrock as a HTTP data source
  - grants policy to invoke it
- `data/resource.ts`
  - create a GraphQL API custom query by creating a schema/type to connect to the data source (Bedrock)
  - builds a custom query to use the data source

### 2. React UI

- source folder `src/` (created by `npm install aws-amplify @aws-amplify/ui-react` and followed by `npm i`)
- the CSS styles were copied from the JS tutorial sample in AWS Developer Center
- uses the `Authenticator` component from Amplify to wrap the app to include sign-up/sign-in/reset password/MFA functionality
- invokes the GraphQL API via Amplify client to get recommendations from Bedrock

## How to run the app

### First time

- bootstrap an AWS environment for use with AWS CDK, run `npx aws-cdk@latest bootstrap aws://{your-aws-account-id}/{aws-region}`

### Development

- to deploy the backend to the sandbox environment, run `npx ampx sandbox`
- an output file `amplify_outputs.json` will be created in the root dir
- it will continue to watch for any new changes and redeploy it
- as for the frontend (React), run `npm run dev`

### [Optional] Deployment

- you can deploy the app as a static site using AWS Amplify
