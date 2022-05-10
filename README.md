# Project description
Every time you log in to the MuleSoft Anypoint Platform using the User Interface Portal, you are implicitly calling a set of APIs invoked by the UI: the Platform APIs! Instead of UI, you can do direct HTTP requests, highly useful When automating your Software Development Lifecycle. They provide you with more flexibility and customization than the Anypoint CLI or the Mule Maven Plugin.

You can make use of this project - postman collection to automate your API Specification, be it - RAML or OAS, written anywhere.

# Motivation
Some clients face issues with automating the API Specifications written in RAML/ OAS outside of the design centre and implementing those specs using MuleSoft Anypoint Platform. Creating or pasting already written API Specs is time taking and repetative task.
This collection of Design Centre APIs automate the need of creating, writing and publishing API specs to Design Centre and Exchange provides quick and reliable way of automating API Specifications written 

# Code Example
![API Spec Automation Pre Req] (https://epam-my.sharepoint.com/:i:/p/nitish_raj1/EQLYGpUB8QFFu-H6nih3zaYB5OVwGoMJ9SHKuA0VP5GoDg?e=FK68J2)

![API Spec Automation Lifecycle] (https://epam-my.sharepoint.com/:i:/p/nitish_raj1/EVwWQ3sMvABEiB_BGZFzgcIB4RNtnexer2OGQ_s7P5e9wQ?e=Y5WdyI)

## Operations
1. Login via Connected App
2. Create a new project
3. Acquire write lock on the branch
4. Add file(s) or folder(s) to upload
5. Publish an asset to Exchange

*Other related optional operations - Adding Dependencies, moving or renaming files or folders, Create fragment, Get file or folder content or structure etc*
More Platform APIs regarding Exchange, API Manager can be found here - https://www.postman.com/mulesoft-api/workspace/abca7de1-d2bb-4be1-8d2b-8d56f87dfbab/documentation/16547909-1e97eed6-ef8c-4d46-9d30-2ff41c8102c5

# Prerequisites
Before we start working with Anypoint platform APIs to automate our API specifications, you need these three pieces of data: an access token, the organization id and the owner id. Let us see where you can find those details.

# Installation
This collection pack contains an environment "API Specification Automation". Set the values before you use any request. You must set the following:

### If Login via Connected App (Using SSO)
    1. url - Anypoint Platform domain address, e.g. https://anypoint.mulesoft.com
    2. client - Connected App Client Id
    3. client_secret - Connected App Client Secret

##### *If Login via Username Password*
    1. url - This will be your Anypoint Platform domain address, e.g. https://anypoint.mulesoft.com
    2. username - This will be login Username
    3. password - This will be login password

### Mandatory environment variables for Project Creation
    1. Project_name - E.g. FINS Salesforce Insurance Exp API Spec
    2. project_classifier - E.g. raml or oas
    3. project_language - E.g. raml (raml) yaml or json (oas)

### Mandatory environment variables for adding any Project Dependencies
    1. dependency_groupId
    2. dependency_assetId
    3. dependency_versionId

### Mandatory environment variables for publishing specs/ fragments to exchange
    1. exchange_apiVersion (e.g. v1)
    2. exchange_assetVersion (e.g. 1.0.0)
    3. exchange_assetId (e.g. salesforce-sys-api-spec)

# API Reference

#### 1. Login via Connected App

```https
POST {{url}}/accounts/api/v2/oauth2/token

curl --location --request POST 'https://anypoint.mulesoft.com/accounts/api/v2/oauth2/token' \
--header 'Content-Type: application/json' \
--data-raw '{
    "client_id": "16bd7f3edeb046f2a460a17569a8f034",
    "client_secret": "9876775EA68643b0ae7e11cDaD2a3390",
    "grant_type": "client_credentials"
}'
```

#### 2. Get profile information

```https
GET {{url}}/accounts/api/profile

curl --location --request GET 'https://anypoint.mulesoft.com/accounts/api/profile' \
--header 'Authorization: Bearer 0caf7d88-0d67-408b-82bb-4d083f1fa9ba' 
```

#### 3. Create a new project

```https
POST {{url}}/designcenter/api-designer/projects

curl --location --request POST 'https://anypoint.mulesoft.com/designcenter/api-designer/projects' \
    --header 'Authorization: Bearer 0caf7d88-0d67-408b-82bb-4d083f1fa9ba' \
    --header 'x-organization-id: 3d4f22b1-075d-4054-b298-04c96a1e2d2c' \
    --header 'x-owner-id: 486bbf0f-925d-431f-9e88-50eda43f30aa' \
    --header 'Content-Type: application/json' \
    --data-raw '{
        "name": "FINS Salesforce Insurance Exp API Spec",
        "classifier": "raml"
}'
```

#### 4. Acquire the Write Lock

```https
POST {{url}}/designcenter/api-designer/projects/{{project_id}}/branches/{{branch}}/acquireLock

curl --location --request POST 'https://anypoint.mulesoft.com/designcenter/api-designer/projects/9b92e545-8ab3-45ca-96dd-ca0c365daa94/branches/master/acquireLock' \
    --header 'Authorization: Bearer 0caf7d88-0d67-408b-82bb-4d083f1fa9ba' \
    --header 'x-organization-id: 3d4f22b1-075d-4054-b298-04c96a1e2d2c' \
    --header 'x-owner-id: 486bbf0f-925d-431f-9e88-50eda43f30aa' \
    --header 'Content-Type: application/json' \
    --data-raw '{}'
```

#### 5. Upload a File (Any - File or File with Folder)

```https
POST {{url}}/designcenter/api-designer/projects/{{project_id}}/branches/{{branch}}/save/v2

curl --location --request POST 'https://anypoint.mulesoft.com/designcenter/api-designer/projects/9b92e545-8ab3-45ca-96dd-ca0c365daa94/branches/master/save/v2' \
    --header 'Authorization: Bearer 0caf7d88-0d67-408b-82bb-4d083f1fa9ba' \
    --header 'x-organization-id: 3d4f22b1-075d-4054-b298-04c96a1e2d2c' \
    --header 'x-owner-id: 486bbf0f-925d-431f-9e88-50eda43f30aa' \
    --form 'fins-salesforce-insurance-exp-api-spec.raml=@"/C:/NonProjects/MuleSoft/API Spec Automation/fins-salesforce-insurance-exp-api-spec.raml"' \
    --form 'dataTypes/ExternalIdType.raml=@"/C:/NonProjects/MuleSoft/API Spec Automation/dataTypes/ExternalIdType.raml"' \
    --form 'dataTypes/ValidationResponseType.raml=@"/C:/NonProjects/MuleSoft/API Spec Automation/dataTypes/ValidationResponseType.raml"' \
    --form 'examples/ExternalIdExample.raml=@"/C:/NonProjects/MuleSoft/API Spec Automation/examples/ExternalIdExample.raml"' \
    --form 'examples/ValidationResponseExample.raml=@"/C:/NonProjects/MuleSoft/API Spec Automation/examples/ValidationResponseExample.raml"'
```

#### 6. Publish to Exchange

```https
POST {{url}}/designcenter/api-designer/projects/{{project_id}}/branches/{{branch}}/publish/exchange

curl --location --request POST 'https://anypoint.mulesoft.com/designcenter/api-designer/projects/9b92e545-8ab3-45ca-96dd-ca0c365daa94/branches/master/publish/exchange' \
    --header 'Authorization: Bearer 0caf7d88-0d67-408b-82bb-4d083f1fa9ba' \
    --header 'x-organization-id: 3d4f22b1-075d-4054-b298-04c96a1e2d2c' \
    --header 'x-owner-id: 486bbf0f-925d-431f-9e88-50eda43f30aa' \
    --header 'Content-Type: application/json' \
    --data-raw '{
        "main": "fins-salesforce-insurance-exp-api-spec.raml",
        "apiVersion": "v1",
        "version": "1.0.0",
        "assetId": "fins-salesforce-insurance-exp-api-spec",
        "groupId": "3d4f22b1-075d-4054-b298-04c96a1e2d2c",
        "classifier": "raml"
    }'
```



# Tests
All APIs come with tests and while automating the collection, make sure they are active.

# Contributing

    1. Clone the repository
    2. Create a feature branch: git checkout -b my-new-feature
    3. Commit your changes: git commit -am 'Added a feature'
    4. Push to the branch: git push origin my-new-feature
    5. Submit a pull request to merge into the development branch and request peer review

# TODO
Do not forget to issue **Soft/ Hard delete an asset in Exchange Copy** for Design Centre and Exchange in case you are testing out this project. You would not want to create any unncessary projects/ assets in your design centre or exchange. 

# versioning
NA 

# Release
NA

# License
NA
