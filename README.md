# Reusable GitHub action for SFDX Deployment
This is a re-usable GitHub action that uses JWT(server-to-server) type authorization to authorize to the Salesforce org and deploy/ validate the SFDX project to the same.


## Pre Steps
1. Create a repository with a SFDX project structure
2. Generate a Self Signed Certificate using open ssl.
3. Create a new Repository secret named **SALESFORCE_JWT_SECRET_KEY** (Settings> Secrets and variables> Actions> New Repository Secret) 
5. Store the content of key file as Repository secret named **SALESFORCE_JWT_SECRET_KEY**
6. Create a Connected app with JWT enabled and upload the certificate on it. [help article](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_jwt_flow.htm&type=5)
7. Configure Environments in your repository setting(Settings> Environments> New Environment). [help article](https://docs.github.com/en/actions/deployment/targeting-different-environments/using-environments-for-deployment)
8. Every Environment should have one variable named **SALESFORCE_USERNAME** (stores username of the user used for connection) and one secret named **SALESFORCE_CONSUMER_KEY** (stores the client id from the created connected app )  
10. Create a GitHub action in your repsitory and use the [SFDX Reusable Workflow](https://github.com/Charush-Devgan/Reusable-SFDX-Workflow/blob/main/.github/workflows/SFDX%20Reusable%20Workflow.yml). You can take help from this [reference](https://github.com/Charush-Devgan/Reusable-SFDX-Workflow/blob/main/.github/workflows/main.yml)


## Deep Dive into the action

### Input Parameters

| Variable      | Description                                                                  | Default value  | Required |
| :-----------: | :----------------------------------------------------------------------------|:--------------:|:--------:|
| ref           | the branch that you need to deploy                                           | main           |  true    |
| run-tests     | run test classes for you deployment or not                                   | true           |  false   | 
| check-only    | to just validate or deploye the project                                      | true           |  false   |
| path          | path to SF project in case you you want to deploy repo other than current one|                |  false   |
| env           | GitHub environment to which you wamt to deploy                               |                |  true    |
