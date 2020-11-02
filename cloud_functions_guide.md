# **Introduction to Cloud Functions**

This introductory level guide describes how to use Google Cloud Platform's Cloud Functions.

Google defines its own product as [such](https://cloud.google.com/functions/docs/concepts/overview):
```
"Google Cloud Functions is a serverless execution environment for building and connecting cloud services. 
With Cloud Functions you write simple, single-purpose functions that are attached to events emitted from your cloud infrastructure and services. 
Your function is triggered when an event being watched is fired. Your code executes in a fully managed environment. 
There is no need to provision any infrastructure or worry about managing any servers."
```
Google's definition of Cloud Functions raises several key concepts. This guide will explore these ideas and more. For now though, consider Cloud Functions as simply a bit of code that runs in the cloud without requiring much infrastructure management from the developer.

## Before you begin

This guide is intended for new users of Google Cloud Functions who possess some familiarity with Google Cloud products and software development. In order to properly use this guide, you will require a Google account and access to a Google Cloud [project](https://cloud.google.com/resource-manager/docs/creating-managing-projects). 

## Guide overview

1. [Concepts](#concepts)
2. [Steps to create a Cloud Function](#steps-to-create-a-cloud-function)
3. [Use cases](#use-cases)
---

# **Concepts**

## Serverless
In the past, organizations needed to [set up, manage, and update servers](https://cloud.google.com/functions/docs/concepts/overview#serverless) in order to run their applications. However, cloud providers like Google Cloud Platform now offer serverless capabilities, which handle all the [infrastructure administration](https://medium.com/techmagic/serverless-vs-docker-what-to-choose-in-2019-80cb80f4b680) for us. In other words, serverless computing allows developers to just focus on writing and deploying the code.

Google Cloud Platform features multiple [serverless options](https://cloud.google.com/serverless-options), including Cloud Functions.

<img src="https://github.com/JohnYoon13/cloud-functions/blob/master/images/00.serverless.png" width="700" height="700" />

## Stateless
Google Cloud Platform describes Cloud Functions as [stateless—"one function invocation should not rely on in-memory state set by a previous invocation."](https://cloud.google.com/functions/docs/concepts/exec#stateless_functions)

In contrast, *stateful* applications retain data from previous usage in order to facilitate future usage. A computer terminal is stateful in that it remembers prior command line inputs. On the other hand, a calculator, which resets to zero after the completion of every operation, is stateless.

Cloud Functions' stateless nature provides [advantages](https://medium.com/@rachna3singhal/stateless-over-stateful-applications-73cbe025f07) such as speed and the ability to easily scale an application by deploying it on multiple servers.

<img src="https://github.com/JohnYoon13/cloud-functions/blob/master/images/stateless.png" width="600" height="600" />

## Scalable
Scalability is another powerful Cloud Functions feature. 

Users can benefit from Cloud Functions' capacity to automatically adjust to rapidly changing request levels. When incoming traffic increases significantly, "[scaling features](https://cloud.google.com/functions/docs/max-instances) create new instances of your function. Each of these instances can only handle one request at a time, so large spikes in request volume might create many instances."

## Events and triggers

Google Cloud Platform's products such as Google Cloud Storage and Pub/Sub possess event capabilities. For instance, if Google Cloud Storage receives a new image, it also registers that an event occured. 

With this in mind, Cloud Functions have [triggers](https://cloud.google.com/functions/docs/concepts/events-triggers#triggers) that activate whenever a specified event occurs. So if a new image enters Google Cloud Storage, the Cloud Functions' trigger notices the event, and the Cloud Function can grab the image to modify it and output it to another destination.

[Events](https://medium.com/@iromin/google-cloud-functions-tutorial-what-is-google-cloud-functions-8796fa07fc7a) that trigger Cloud Functions can stem from: 

- HTTP
- Cloud Storage
- Cloud Pub/Sub
- Cloud Firestore
- Firebase
- Stackdriver Logging

<img src="https://github.com/JohnYoon13/cloud-functions/blob/master/images/event.png" width="700" height="500" />

## Summary
Cloud Functions create stateless and event-driven functions that can quickly scale to meet demand, all without managing server overhead.

---
# **Steps to create a Cloud Function**
Creating a Cloud Function through Google Cloud Platform's interface can translate the previously discussed concepts into more practical terms.

**0.** Set up a Google Cloud Platform [project](https://cloud.google.com/resource-manager/docs/creating-managing-projects).

**1.** Open the navigation menu located in the upper left corner of the project landing page

<img src="https://github.com/JohnYoon13/cloud-functions/blob/master/images/00.start-nav.png"/>

---

**2.** Go to the **COMPUTE** section and select *Cloud Functions*. Pin Cloud Functions for easier access in the future.

<img src="https://github.com/JohnYoon13/cloud-functions/blob/master/images/0.start.png" width="400" height="600" />

---

**3.** Select the "Create Function" option.

<img src="https://github.com/JohnYoon13/cloud-functions/blob/master/images/1.create.png" width="800" height="50" />

---

**4.** Enter the *Function name*, such as "tutorial." Then choose the [region](https://cloud.google.com/compute/docs/regions-zones) to host the function. Finally, set the preferred trigger event. Google Cloud Platforms offers multiple [options](https://cloud.google.com/functions/docs/concepts/events-triggers), but this guide will choose *Cloud Pub/Sub* as the trigger, with an accompanying [Pub/Sub topic](https://cloud.google.com/pubsub/docs/admin) and Cloud Scheduler already created to facilitate the process. In other words, every time the Pub/Sub topic receives data, the Cloud Function will trigger and run the function.

<img src="https://github.com/JohnYoon13/cloud-functions/blob/master/images/2.configurations.png" width="500" height="600" />

---

**5.** Save the results and press *Next*. This will lead to the source code page. Under *Runtime*, select a programming language, such as Python. Then implement your source code in *main.py*; in this case, the code contains a simple "Hello World" print statement. Then, verify that the *requirements.txt* file contains all the required libraries and packages. Finally, choose the [*Entry Point*](https://cloud.google.com/functions/docs/concepts/exec), which specifies the function name that the Cloud Function will execute.

<img src="https://github.com/JohnYoon13/cloud-functions/blob/master/images/3.setup.png" width="700" height="600" />

---

**6.** After reviewing that all the configurations prove correct, deploy the Cloud Function.

<img src="https://github.com/JohnYoon13/cloud-functions/blob/master/images/4.deploy.png" width="700" height="100" />

---

**7.** The deployment process can take up to several minutes. Upon successful deployment, a green check mark will appear alongside the Cloud Function. 

<img src="https://github.com/JohnYoon13/cloud-functions/blob/master/images/5.results.png"/>

---

**8.** To confirm that the application correctly generates the expected "Hello World" print statement, select the function and choose the *View Logs* option. Use the *Edit* feature to update the source code if necessary.

<img src="https://github.com/JohnYoon13/cloud-functions/blob/master/images/6.logs.png"/>

<img src="https://github.com/JohnYoon13/cloud-functions/blob/master/images/7.logs-results.png" width="800" height="100" />

---
# **Use cases**
Cloud Functions' lightweight and flexible characteristics lend themselves to many different [use cases](https://cloud.google.com/functions/docs/concepts/overview#use_cases). Cloud Functions can behave as a glue that binds together cloud services. 

<img src="https://github.com/JohnYoon13/cloud-functions/blob/master/images/use.png"/>

---

# Next steps

You can find additional information relating to Google Cloud Functions such as tutorials and API Reference documentation [here](https://cloud.google.com/functions/docs).

To see a practical workflow using Cloud Functions with other Google Cloud Platform tools such as Pub/Sub and BigQuery, refer to the following [guide](https://github.com/JohnYoon13/GCP/blob/master/gcp.md).
