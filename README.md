# Introduction 

Introducing Red Hat® Marketplace, an open cloud marketplace that makes it easier to discover and access certified software for container-based environments in public clouds and on-prem. With automated deployment, software is immediately available to deploy on any Red Hat® OpenShift® cluster, providing a fast, integrated experience.

[Check this out to know more about Red Hat Marketplace](https://marketplace.redhat.com/en-us/about).

### How to install, setup & get started using the Findability Platform Predict Plus operator on Red Hat OpenShift cluster

In this tutorial, we demonstrate how to install, setup and get started using the Findability Platform Predict Plus (FPPredict Plus) operator from Red Hat Marketplace (RHM). Every operator on Red Hat Marketplace has different setup for installation and configuration and the focus of this tutorial is Findability Platform Predict Plus operator.

The advantages of using RHM operators are per below.  

* `Software for any cloud` :- Enterprise software for container-based environments in public clouds and on-prem

* `Automated deployment` :- Fast, integrated experience with instant availability on Red Hat® OpenShift® clusters

* `Fully supported` :- Free, continuous support for products purchased through Red Hat Marketplace

### A brief about Findability Platform Predict Plus operator (Version - 0.0.4)

FP-Predict +™, an Automated, self learning, and Multi Modeling Artificial Intelligence (AI) that handles Discrete Target variable, Continuous Target variable and Time series data with no need for coding. This operator will be helpful to solve some of the usecases under AI using different methods like Regression, Classification, Timeseries etc. This operator will be applicable to developers, data scientists, architects who wants to solve different usecases under machine learning and AI. 


# Prerequisites

* For all operators being installed from RHM, OpenShift cluster version 4.3 or higher is mandatory. Please set up Classic cluster using the instructions from below URL.

[Setting up OpenShift Cluster](https://cloud.ibm.com/docs/openshift?topic=openshift-getting-started)

* We need to have an account created at Red Hat Marketplace by following this [link](https://marketplace.redhat.com/api-security/en-us/login/landing).

# Estimated time

It would take about an hour to complete the tutorial.

# Steps

### Access the RedHat OpenShift Container Platform (Web Console)

Follow the steps below to launch the cluster console which is also called RedHat OpenShift Container Platform.

Login to IBM Cloud Account and navigate to Dashboard

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/dashboard.png)

Click on Clusters and select the cluster which you have created under prerequisites. In this tutorial, cluster name is `cp-rhm-poc`.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/cluster.png)

After you launch the cluster, click on `OpenShift web console` on the top right hand side.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/web-console.png)

We can see the RedHat OpenShift Container Platform (Web Console). Click on question mark icon on the top right hand side and select `Command Line Tools`. 

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/cmd-line-tools.png)

Navigate to the section `oc - OpenShift Command Line Interface (CLI)` and download the respective oc binary onto your local system. This is needed to manage OpenShift projects from a terminal and is further extended to natively support OpenShift Container Platform features.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/oc-binary.png)

We are all set to proceed to next step which is to register the OpenShift cluster on Red Hat Marketplace platform. This is mandatory to install any operators from RedHat Marketplace platform using the OpenShift cluster.

### Register the cluster on Red Hat Marketplace

Sign up and login to RHM portal at [Link](https://marketplace.redhat.com/en-us) and click on workspace and then click on cluster. We need to add our new OpenShift cluster and register it on RHM platform.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/add-cluster.png)

Update the cluster name, generate the pull secret as per the instructions and save it. 

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/cluster-details.png)

Copy the curl command which starts with `curl -sL https` and append the pull secret towards the end. The entire script should be handy to be used in next step.

We need to start the cluster first to register it. Open a command prompt and type `oc login`, update the username and password which are used for accessing the cluster and hit enter. 

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/start-cluster.png)

The cluster is up and running at this point. We need to run the entire script on command prompt which is copied from previous step and hit `enter` or `return` in Mac. It will take a couple of mins and we can see that we have successfully registered the cluster on RedHat Marketplace portal.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/register-cluster.png)

### Create a project in web console

We need to create a project to be used and managed from command line. Click on `Create Project` and give any name of your choice. We are using the name `findability-project` for this tutorial.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/create-project.png)

### Install the operator

**Sign in to Red Hat Marketplace, navigate to the search bar and select `Findability Platform Predict Plus`.**

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/sel-operator.png)

**Choose the `Free trial` option in the next page and select the instance.**

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/free-trial.png)

`Note` :- This is a trial instance with the following constraints per below.

* Up to 100K rows in training data and up to 50K rows in prediction data
* Up to 500 variables, features and columns
* 30 days free trial

**Navigate to `Workspace` option at the top and click on `My software` option on the left pane.**

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/software.png)

**Choose the operator `FP-Predict+` by clicking on it and we will be directed to the next page where we need to choose `Install operator` from `Operators` menu.**

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/operator-install.png)

**Check the box under `Target clusters` and select the `Name` and choose the project name which was created in previous step under `Namespace Scope` option. We can leave the other default options as is and click `Install`. We are going ahead with Automatic method of installation, there is also an option do install the operator manually.**

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/sel-namespace.png)

After a couple of minutes, the operator gets installed on the cluster. We should see the `Status` as `Up to date`. We can launch the web console by clicking on the option next to `Cluster Console`

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/instld-optr.png)

In the Web console, we can verify by clicking on Installed Operators under `Operators` option in the `left` navigation pane and see that the operator is successfully installed with status showing as Succeeded.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/installed-operator.png)

### Create storage for the operator

We need to create persistent volume in the name of `fp-predict-plus-pv` to be bound to persistent volume claims. This step is necessary to enable storage capabilities for the operator to manage datasets. Click on persistent volume under Storage, update the name as `fp-predict-plus-pv` and storage capacity as 20 GB and hit `Create`. If we need more storage, we can increase it in the YAML file and create the persistent volume accordingly.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/create-pv.png)

We need to create a persistent volume claim (storage) to use the storage created in previous step and bind it to the instance of this operator. Click on storage under Web Console and select Persistent Volume Claims.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/select-pvc.png)

The next step is to create persistent volume claim. We can select Storage Class from Gold, Silver, Bronze which was created in previous step, give the name as `fp-predict-plus-pvc`, select single user access & assign the storage size as 20 GB. 

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/create-pvc.png)

After the persistent volume claim (PVC) is created, it needs to be bound with the persistent volume (PV) which was created in earlier step. We should see the status as `Bound` per below after couple of minutes.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/pvc-bound.png)

### Install the operand (Instance) of FPPredict Plus

Click on Installed operators under `Operators` and click on FP Predict Plus Operator to get the options like Overview, YAML, Subscription, Events, FP-Predict-Plus. Click on YAML and update the `name` as `fp-predict-plus-pvc` per below, `useExisting as false` (useExisting would be true if we want to use the same storage for another instance), `volumeName` as `fp-predict-plus-pv`, routerCanonicalHostname would be the web console URL and hit `Save`. routerCanonicalHostname would start with the cluster name, cluster id till appdomain.cloud. The initial part in the URL - `https://console-openshift-console` should be removed while updating routerCanonicalHostname.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/yaml-changes.png)

The next step is to proceed towards FP-Predict-Plus option and click on Create FPpredictplus instance. Edit the YAML file and give a name for the instance and click `Save`.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/operand.png)

### Launch the operand (Instance) of FPPredict Plus

We are all set to launch the instance. `How do we do it?` We need to click on Networking and select Routes and then click on the URL which is under the location to launch the instance. 

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/route.png)

### Register the instance of FPPredict Plus

We can login using the default credentials as per the [configuration file](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/credentials.txt), accept the end user license agreement and will be directed to the next page per below. Click on `Download` and share the file with the Findability Sciences support team. The support team will send the license file (with 30 days validity) and needs to be uploaded using the `Upload File` option. We are all set to access the instance of FPPredict Plus. 

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/sys-info.png)

**Note :- Trial License key is provided only once by the support team. Please do not uninstall the instance of FP Predict Plus (in the web console or in Red Hat Marketplace portal) as re-installation of the instance would require a new trial license key.**

After uploading the license key, we can bring up the `FP Predict+` instance per below. The navigation pane on the `left` has four options namely Dashboard, Analytics, Dataset Management & License Information. We are good to go from here. 

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/fp-predict.png)

`Note` :- We may have to repeat all the steps if there is a version upgrade as some of the components from setup does not support product upgrades.

# Summary

With this, we have come to the end of this tutorial to understand all the aspects of installation, configuration, setup and more to get started using the FPPredict Plus operator from Red Hat Marketplace on OpenShift cluster to solve usecases under AI. Red Hat Marketplace is a one stop platform for exploring multiple operators which will help to solve some of the complex usecases under different domains. 

# Related Links

[Know more about FP Predict+ operator on RedHat Marketplace](https://marketplace.redhat.com/en-us/products/fp-predict)

