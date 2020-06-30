# How to install, setup & get started using the Findability Platform Predict Plus operator on RedHat Marketplace

In this tutorial, we demonstrate how to install, setup and get started using the Findability Platform Predict Plus (FPPredict Plus) operator on RedHat Marketplace (RHM). The advantages of using RHM operators are per below.  

* `Software for any cloud` :- Enterprise software for container-based environments in public clouds and on-prem

* `Automated deployment` :- Fast, integrated experience with instant availability on Red Hat® OpenShift® clusters

* `Fully supported` :- Free, continuous support for products purchased through Red Hat Marketplace

## A brief about Findability Platform Predict Plus operator

This operator is helpful to solve some of the usecases under AI using different methods like Regression, Classification, Timeseries etc. This operator will be applicable to developers, data scientists, architects who wants to solve different usecases under machine learning and AI. 


## Prerequisites

For all operators being installed from RHM, OpenShift cluster version 4.3 or higher is mandatory. Please set up Classic cluster using the instructions from below URL.

[Setting up OpenShift Cluster](https://cloud.ibm.com/docs/openshift?topic=openshift-getting-started)

## Next Step - Access the RedHat OpenShift Container Platform (Web Console)

Follow the steps below to launch the cluster console which is also called RedHat OpenShift Container Platform.

* Login to IBM Cloud Account and navigate to Dashboard

[Dashboard](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/dashboard.png)

* Click on Clusters and select the cluster which you have created under prerequisites. In our case, cluster name is cp-rhm-poc.

[Select the cluster](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/cluster.png)

* After you launch the cluster, click on OpenShift web console on the top right hand side.

[Launch Web Console](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/web-console.png)

* We can see the RedHat OpenShift Container Platform (Web Console). Click on question mark ikon on the top right hand side and select Command Line Tools. 

[Command line tools](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/cmd-line-tools.png)

* Navigate to the section `oc - OpenShift Command Line Interface (CLI)` and download the respective oc binary onto your local system. This is needed to manage OpenShift projects from a terminal and is further extended to natively support OpenShift Container Platform features.

[Install oc binary](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/oc-binary.png)









