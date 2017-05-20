# Run Parse-server on GCP App Engine

> [Note] Original document from [GCP](https://cloud.google.com/nodejs/resources/frameworks/parse-server#download_app).

It's easy to get started developing Parse-server apps running on Google Cloud Platform. And because the apps you create will be running on the same infrastructure that powers all of Google's products, you can be confident that they will scale to serve all of your users, whether there are a few or millions of them.
This tutorial gets you going fast by deploying a simple Parse-server app. This tutorial assumes that you are familiar with Node.js programming and that you have already Prepared Your Environment for Node.js Development.


## Before you begin

Check off each step as you complete it.

### Create a project in the Google Cloud Platform Console.
If you haven't already created a project, create one now. Projects enable you to manage all Google Cloud Platform resources for your app, including deployment, access control, billing, and services.

1. Open the [Cloud Platform Console](https://console.cloud.google.com/).
2. In the drop-down menu at the top, select Create a project.
3. Click Show advanced options. Under App Engine location, select a United States location.
4. Give your project a name.
5. Make a note of the project ID, which might be different from the project name. The project ID is used in commands and in configurations.

### Enable billing for your project.
If you haven't already [enabled billing](https://console.cloud.google.com/project/_/settings?_ga=1.22855806.496551942.1491453407) for your project, enable billing now. Enabling billing allows the application to consume billable resources such as running instances and storing data.

### Install the Google Cloud SDK.
If you haven't already installed the Google Cloud SDK, [install and initialize the Google Cloud SDK](https://cloud.google.com/sdk/docs/) now. The SDK contains tools and libraries that enable you to create and manage resources on Google Cloud Platform.


## Download and run the app

A simple Hello World app written in Node.js and using Parse-server is available to help you quickly get a feel for deploying an app to Cloud Platform. After you've completed the prerequisites, you can download and deploy the Parse-server sample app. The following sections guide you through getting the Parse-server app up and running.
You can view the deployed app [here](http://parse-dot-nodejs-docs-samples.appspot.com/).

### Clone the Parse-server app

The code for the Parse-server sample app is in the [GoogleCloudPlatform/nodejs-docs-samples](https://github.com/GoogleCloudPlatform/nodejs-docs-samples/tree/master/appengine/parse-server) repository on GitHub. If you haven't already, copy the repository to your local machine:

```
git clone https://github.com/GoogleCloudPlatform/nodejs-docs-samples.git
```

Go to the directory that contains the sample code:

```
cd nodejs-docs-samples
```

The Parse-server sample app is in the appengine folder:

```
cd appengine/parse-server
```

Alternatively, you can [download the sample](https://github.com/GoogleCloudPlatform/nodejs-docs-samples/archive/master.zip) as a zip and extract it.

### Create a MongoDB database

There are multiple options for creating a new MongoDB database. For example:

- Create a Google Compute Engine virtual machine with [MongoDB pre-installed](https://cloud.google.com/launcher/?q=mongodb).
- Use [mLab](https://mlab.com/google/) to create a free MongoDB deployment on Google Cloud Platform Central 1 (us-central1) region. Currently, you can not select another region.
- Use [MongoDB Atlas](https://www.mongodb.com/cloud) to create a free MongoDB deployment on Amazon Web Service N. Virginia (us-east-1) region. Currently, you can not select another region.

### Set environment variables

To run the app locally, you need to set a few environment variables in the config.json file:

- DATABASE_URI - MongoDB URI for your database.
- APP_ID - Id of the app your Parse-server will be running.
- MASTER_KEY - The master key to use for overriding ACL security.
- SERVER_URL - Url of your app, for example, http://localhost:8080/parse

### Run the app on your local computer

1. Install dependencies:

```
npm install
```

2. Run the start script:

```
npm start
```

3. In your web browser, enter this address:

```
http://localhost:8080
```

You can see the Hello World message from the sample app displayed in the page. This page is delivered by the Parse-server web server running on your computer.

When you're ready to move forward, press Ctrl+C to stop the local web server.


## Running Parse-server on Google Cloud Platform

The following diagram shows the process of deploying the app on Cloud Platform.

![](https://cloud.google.com/languages/images/hello-world-app-structure.png)

The App Engine flexible environment runs your application in containers that can automatically scale to handle your application's load. Behind the scenes, this architecture uses both Compute Engine and Docker. To learn more, see [App Engine flexible environment](https://cloud.google.com/appengine/docs/flexible/).

### Deploy the app to Google Cloud Platform

Enter this command to deploy the sample:

```
gcloud app deploy
```

Wait for the message that notifies you that the app update has completed.

### See the app run in the cloud

In your web browser, enter this address:

```
https://<your-project-id>.appspot.com
```

This time, the page that displays the Hello World message is delivered by a web server running in the App Engine flexible environment.

If you update your app, you can deploy the updated version by entering the same command you used to deploy the app the first time. The new deployment creates a [new version](https://console.cloud.google.com/project/_/appengine/versions) of your app and promotes it to the default version. The older versions of your app remain, as do their associated VM instances. Be aware that all of these app versions and VM instances are billable resources. For information about deleting or stopping your VM instances, see [Cleaning up](https://cloud.google.com/nodejs/getting-started/delete-tutorial-resources).

For convenience, you can use an npm script to run the gcloud command. Add these lines to your ``package.json`` file:

```json
"scripts": {
  "start": "node server.js",
  "deploy": "gcloud app deploy  --project <your-project-id>"
}
```

Now you can run this command to deploy your application:

```
npm run deploy
```

## Configuration

Every app that runs in the App Engine flexible environment requires an app.yaml file to describe its deployment configuration.

```
// appengine/parse-server/app.yaml
runtime: nodejs
env: flex
```

[VIEW ON GITHUB](https://github.com/GoogleCloudPlatform/nodejs-docs-samples/blob/master/appengine/parse-server/app.yaml)

This minimal app.yaml file sets the runtime to nodejs with the flexible environment. There are many other configuration values you can specify in app.yaml that allow you to customize resources, scaling, and other settings. For details about the configuration settings for the flexible environment, see [App Engine flexible environment](https://cloud.google.com/appengine/docs/flexible/).
