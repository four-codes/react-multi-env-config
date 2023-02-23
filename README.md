MultiStage build

    # from node docker images
    FROM node:alpine as node
    WORKDIR /app
    COPY . .
    RUN npm install 
    RUN REACT_APP_STAGE=prod npm run build --prod

    #  multi-stage
    FROM nginx:latest
    COPY --from=node    /app/build /usr/share/nginx/html
    EXPOSE 80
    
 _Based on the environment deployment before the build, you should replace those values with the tokanize task in Azure DevOps and build to pick it up with appropriate commands._
 
 ```js
 var dev = {
    s3: {
      BUCKET: "#{YOUR_DEV_S3_UPLOADS_BUCKET_NAME}#",
    },
    apiGateway: {
      REGION: "#{YOUR_DEV_API_GATEWAY_REGION}#",
      URL: "#{YOUR_DEV_API_GATEWAY_URL}#",
    },
    cognito: {
      REGION: "#{YOUR_DEV_COGNITO_REGION}#",
      USER_POOL_ID: "#{YOUR_DEV_COGNITO_USER_POOL_ID}#",
      APP_CLIENT_ID: "#{YOUR_sname}#",
    },
  };
  
  var prod = {
    s3: {
      BUCKET: "#{YOUR_PROD_S3_UPLOADS_BUCKET_NAME}#",
    },
    apiGateway: {
      REGION: "#{YOUR_PROD_API_GATEWAY_REGION}#",
      URL: "#{YOUR_PROD_API_GATEWAY_URL}#",
    },
    cognito: {
      REGION: "#{YOUR_PROD_COGNITO_REGION}#",
      USER_POOL_ID: "#{YOUR_PROD_COGNITO_USER_POOL_ID}#",
      APP_CLIENT_ID: "#{YOUR_PROD_COGNITO_APP_CLIENT_ID}#",
      IDENTITY_POOL_ID: "#{YOUR_PROD_IDENTITY_POOL_ID}#",
    },
  };
  
  var sit = {
    s3: {
      BUCKET: "#{YOUR_SIT_S3_UPLOADS_BUCKET_NAME}#",
    },
    apiGateway: {
      REGION: "#{YOUR_SIT_API_GATEWAY_REGION}#",
      URL: "#{YOUR_SIT_API_GATEWAY_URL}#",
    },
    cognito: {
      REGION: "#{YOUR_SIT_COGNITO_REGION}#",
      USER_POOL_ID: "#{YOUR_SIT_COGNITO_USER_POOL_ID}#",
      APP_CLIENT_ID: "#{YOUR_SIT_COGNITO_APP_CLIENT_ID}#",
      IDENTITY_POOL_ID: "#{YOUR_SIT_IDENTITY_POOL_ID}#",
    },
  };
  
  var test = {
    s3: {
      BUCKET: "#{YOUR_TEST_S3_UPLOADS_BUCKET_NAME}#",
    },
    apiGateway: {
      REGION: "#{YOUR_TEST_API_GATEWAY_REGION}#",
      URL: "#{YOUR_TEST_API_GATEWAY_URL}#",
    },
    cognito: {
      REGION: "#{YOUR_TEST_COGNITO_REGION}#",
      USER_POOL_ID: "#{YOUR_TEST_COGNITO_USER_POOL_ID}#",
      APP_CLIENT_ID: "#{YOUR_TEST_COGNITO_APP_CLIENT_ID}#",
      IDENTITY_POOL_ID: "#{YOUR_TEST_IDENTITY_POOL_ID}#",
    },
  };
  
  const config =
    process.env.REACT_APP_STAGE === "prod"
      ? prod
      : process.env.REACT_APP_STAGE === "sit"
      ? sit
      : process.env.REACT_APP_STAGE === "test"
      ? test
      : dev;
  
  export default config;
 ```
