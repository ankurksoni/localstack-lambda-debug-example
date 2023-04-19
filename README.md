# Debug Lambda in localstack

Unlocking the power of local development & debugging for NodeJS Lambda functions with LocalStack & VS Code integration

## Disclaimer 
I am using [linux mint](https://www.linuxmint.com/download.php) to run this setup.

## Prerequisites

For this tutorial, you will need the following packages installed:
1. ***localstack*** [to create a local Lambda function]: https://docs.localstack.cloud/getting-started/installation/

   
2. ***awslocal*** [command-line interface to run local AWS commands against LocalStack]: https://docs.localstack.cloud/user-guide/integrations/aws-cli/#localstack-aws-cli-awslocal
     
3. ***VSCode*** [To run a debug configuration]: https://code.visualstudio.com/download

4. ***docker-compose*** [To launch LocalStack with additional configuration]: https://docs.docker.com/compose/install/

## Usage

1. Run the below command at the project root directory,
    ```
    docker compose up -d
    ```
2. `launch.json` and `tasks.json` are already created for you in directory `.vscode` and will work perfectly on your system.
3. A simple lambda function is created as `function.js`
4. First go to ***Run and Debug*** window by clicking it from the sidebar.
5. Your debugger shall start without any issues.
6. open another terminal in VSCode and run the below command.
    ```
        $ awslocal lambda create-function \
        --function-name localstack-nodejs-lambda-function \
        --code S3Bucket="hot-reload",S3Key="$(pwd)/" \
        --handler function.handler \
        --runtime nodejs14.x \
        --timeout 120 \
        --role arn:aws:iam::000000000000:role/lambda-role

    ```
7. When you hit the above command you will enter the code in debug mode and then can debug complexities as you desire.

## known issues
*   Due to the ports used by the debugger, you can currently only debug one Lambda at a time, due to which multiple concurrent invocations will not work.

## Courtesy
https://hashnode.localstack.cloud/debugging-nodejs-lambda-functions-locally-using-localstack