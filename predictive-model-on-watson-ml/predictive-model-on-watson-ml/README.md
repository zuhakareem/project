# Deploy a model to predict heart failure with Watson Machine Learning

> **DISCLAIMER**: This application is used for demonstrative and illustrative purposes only and does not constitute an offering that has gone through regulatory review.

This code pattern can be thought of as two distinct parts:

1. A predictive model will be built using AutoAI on IBM Cloud Pak for Data. The model is then deployed to the Watson Machine Learning service, where it can be accessed via a REST API.

2. A Node.js web app that allows a user to input some data to be scored against the previous model.

When the reader has completed this Code Pattern, they will understand how to:

* Build a predictive model with AutoAI on Cloud Pak for Data
* Deploy the model to the IBM Watson Machine Learning service
* Via a Node.js app, score some data against the model via an API call to the Watson Machine Learning service


## Architecture

1. The developer creates a [Cloud Pak for Data](https://www.ibm.com/cloud/watson-studio) project.
1. A model is created with AutoAI by uploading some data.
1. Data is backed up and stored on Cloud Object Storage.
1. The model is deployed using the Watson Machine Learning service.
1. A [Node.js](https://nodejs.org/) web app is deployed on IBM Cloud. It calls the predictive model hosted on the Watson Machine Learning service.
1. A user visits the web app, enters their information, and the predictive model returns a response.


## Prerequisites

* An [IBM Cloud Account](https://cloud.ibm.com)
* An account on [IBM Cloud Pak for Data](https://dataplatform.cloud.ibm.com/).

## Steps

1.	Create an IBM Cloud API key
2.	Create a new Cloud Pak for Data project
3.	Build a model with AutoAI
4.	Deploy the model with WML
5.	Run the Node.js application


### 1. Create an IBM Cloud API key

To use the Watson Machine Learning service programmatically we'll need an API key. Even though this isn't used until later on, let's create one now.

Navigate to <https://cloud.ibm.com/iam/apikeys> and choose to create a new API key.

Give it a name and description, hit OK. Write down the API key somewhere.


### 2. Create a new Cloud Pak for Data project

Log into IBM's [Cloud Pak for Data](https://dataplatform.cloud.ibm.com) service (formally known as Watson Studio). Once in, you'll land on the dashboard.

Create a new project by clicking `Create a project`.

Choose an `Empty project`.

Enter a `Name` and associate the project with a `Cloud Object Storage` service.

At the project dashboard click on the `Assets` tab and upload the data set associated with this repo. [`patientdataV6.csv`](https://raw.githubusercontent.com/IBM/predictive-model-on-watson-ml/master/data/patientdataV6.csv)

### 3. Build a model with AutoAI

Now we're going to build a model from the data using IBM's AutoAI. A tool that will automatically create multiple models and test them, giving us the best result. Data science made easy!

Start by clicking on `Add to project` and choosing `AutoAI experiment`.

Give it a `Name` and specify a `Watson Machine Learning` instance.

Choose to use data from your project.

Choose the `patientdataV6.csv` option.

For the "What do you want to predict?" option, choose `HEARTFAILURE`.

The experiment will take a few minutes to run. Once completed hover over the top option to make the `Save as` button appear. Click it.

Choose to save the experiment as a `Model`. You can optionally download a generated Jupyter Notebook that can be used to re-create the steps that were taken to create the model.

You model will be saved. Click the dialog to view it in your project.

Once you're at the model overview choose the button `Promote to deployment space`.

### 4. Deploy the model with WML

To promote the model to deployment you must specify a deployment space. If no space is created choose the `New space +` option to create one. This action will associate the model with the space.

Navigate to the space using the hamburger menu (`☰`) on the top right and choose to `View all spaces`.


Click on the space you saved the model to.

Choose the deploy the model by clicking the rocket ship icon.

Choose the `Online` deployment option and give it a name.

Your new deployment will appear.

Click on the `API reference` tab and save the `Endpoint`. We'll be using this in our application.

### 5. Run the Node.js application

You can deploy this application as a Cloud Foundry application to IBM Cloud by simply clicking the button below. This option will create a deployment pipeline, complete with a hosted Git lab project and devops toolchain.

<p align="center">
    <a href="https://cloud.ibm.com/devops/setup/deploy?repository=https://github.com/IBM/predictive-model-on-watson-ml">
    <img src="https://cloud.ibm.com/devops/setup/deploy/button_x2.png" alt="Deploy to IBM Cloud">
    </a>
</p>

You may be prompted for an *IBM Cloud API Key* during this process. Use the `Create (+)` button to auto-fill this field and the others. Click on the `Deploy` button to deploy the application.

Before using the application go to the `Runtime` section of the application and in the `Environment variables` tab add in your `API_KEY` and `DEPLOYMENT_URL` values from steps 1 and 4.

> **TIP** Do *NOT* wrap these values with double quotes.

Once updated your application will restart and you can visit the application by clicking on `Visit App URL`.

The app is fairly self-explantory, simply fill in the data you want to score and click on the `Classify` button to test how those figures would score against our model. The model predicts that the risk of heart failure for a patient with these medical characteristics.

## License

This code pattern is licensed under the Apache Software License, Version 2.  Separate third party code objects invoked within this code pattern are licensed by their respective providers pursuant to their own separate licenses. Contributions are subject to the [Developer Certificate of Origin, Version 1.1 (DCO)](https://developercertificate.org/) and the [Apache Software License, Version 2](http://www.apache.org/licenses/LICENSE-2.0.txt).

[Apache Software License (ASL) FAQ](http://www.apache.org/foundation/license-faq.html#WhatDoesItMEAN)
