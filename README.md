# Travel Destination Recommender

## Background

This app was created based on the tutorial:  
https://www.youtube.com/watch?v=Ao5TF4yUNXQ

## Tech stack

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

- Go to Amazon Bedrock service in AWS console
- Choose 'Claude 3 Sonnet' from model catalog
- Request for access

### AWS CLI

- log in your AWS account locally via `aws configure`

## Contents in this repo

1. AWS Amplify

- folder `amplify/` (created by `npm create amplify@latest -y`)
- Lambda functions
  - `request()`: to construct a POST request (prompt) to Bedrock
  - `response()`: to parse the response from Bedrock and return to client
- `backend.ts`
  - add Bedrock as a HTTP data source
  - grant policy to invoke it
  - build a custom query to use the data source
- `auth/resource.ts`
  - create a GraphQL API custom query by creating a schema/type to connect to the data source (Bedrock)
  - bootstrap before deployment, run `npx aws-cdk@latest bootstrap aws://132358260776/ap-southeast-1`
  - to deploy to sanbox, run `npx ampx sandbox`
  - an output file `amplify_outputs.json` will be created in the root dir

2. React UI

- folder `src/` (created by `npm install aws-amplify @aws-amplify/ui-react`)
- use the `Authenticator` component to wrap the app to include sign-up/sign-in/reset password/MFA features
- invoke the GraphQL API via Amplify client to get recommendations from Bedrock
- copy the CSS styles from the JS tutorial sample in AWS Developer Center to apply
- deploy the static site
