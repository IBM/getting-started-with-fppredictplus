# Access trial software in Red Hat Marketplace 

For Red Hat® OpenShift® 4 users, [Red Hat® Marketplace](https://marketplace.redhat.com/en-us/about) gives you one place to access certified software for container-based environments. Software in the marketplace is immediately available to deploy on any Red Hat® OpenShift® cluster, providing a fast, integrated experience. In this tutorial, we show you how to install, set up and start using trial software in the marketplace, using the Findability Platform Predict Plus (FPPredict Plus) as an example. You can extend the instructions here for other software available on the Red Hat Marketplace.

### Quick intro to Findability Platform Predict Plus operator (Version - 0.0.4)

FP-Predict +™ is an automated, self learning, multi-modeling artificial intelligence (AI) tool that handles discrete target variables, continuous target variables, and time series data with no need for coding. <--EM: WHat is "no need for coding" referncing? Is it just a GUI that you can use?-->

# Prerequisites

* Red Hat OpenShift version 4.3 is requried to use with the software in Red Hat Markeplace. You can set up a class cluster using these instructions: 
[Set up OpenShift Cluster](https://cloud.ibm.com/docs/openshift?topic=openshift-getting-started) <!--EM WHy are we sending them to our docs? This is just about how to use Red Hat OpenShift on IBM Cloud-->

* [Create an account](https://marketplace.redhat.com/api-security/en-us/login/landing)) on Red Hat Marketplace

# Estimated time

It would take about an hour to complete the tutorial.

# Steps

## Access the RedHat OpenShift Container Platform web console

Follow the steps below to launch the RedHat OpenShift Container Platform.

1. Login to your IBM Cloud account and navigate to the dashboard:

    ![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/dashboard.png)

1. Click **Clusters** and select the cluster you created in the prerequisites section. In this tutorial, the cluster name is `cp-rhm-poc`.

    ![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/cluster.png)

1. After you launch the cluster, click on **OpenShift web console** on the top right-hand side of the screen.

    ![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/web-console.png)

1. You should see the RedHat OpenShift Container Platform web console. Click the question mark icon on the top right-hand side and select **Command Line Tools**. 

    ![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/cmd-line-tools.png)

1. Navigate to the section `oc - OpenShift Command Line Interface (CLI)` and download the respective oc binary onto your local system. You need this to manage OpenShift projects from a terminal. The binary is extended to natively support OpenShift Container Platform features.

    ![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/oc-binary.png)

Now you are ready to register the OpenShift cluster on Red Hat Marketplace. This step is mandatory to install any operators from Red Hat Marketplace platform using the OpenShift cluster.

## Register the cluster on Red Hat Marketplace

1. Log into the [Red Hat Marketplace](https://marketplace.redhat.com/en-us). Select a workspace and click **Cluster**. You need to add the new OpenShift cluster and register it on the Red Hat Marketplace platform.

    ![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/add-cluster.png)

1. Update the cluster name, generate the pull secret as per the instructions and save it. <!--EM: I'm confused about this. On the screen it looks like you create the secret, install the operator and then lick "Add cluster" but that's not what you're describing here is it?-->

    ![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/cluster-details.png)

1. Copy the curl command which starts with `curl -sL https` and append the pull secret towards the end. The entire script should be handy to be used in next step. <!--EM: Where is the reader getting a curl-command? Is that in the GUI? -->

1. You need to start the cluster first to register it. Open a command prompt and type `oc login`, update the username and password which are used for accessing the cluster, and press **Enter**. 

    ![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/start-cluster.png)

Your cluster should be up and running at this point. You need to run the entire script on a command prompt which is copied from previous step and hit `enter` or `return` in Mac. It will take a couple of minutes to can see that you successfully registered the cluster on Red Hat Marketplace portal.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/register-cluster.png)

## Create a project in the web console <!--EM: Is this the RHM web console?-->

Now we will show you how to create a project to be used and managed from command line. Click **Create Project** and name the project however you want. We use the name `findability-project` for this tutorial.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/create-project.png)

## Install the operator

1. Sign in to the Red Hat Marketplace, navigate to the search bar, and search for "Findability Platform Predict Plus".

    ![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/sel-operator.png)

1. Choose the **Free trial** option on the next page and select the instance.<!--EM: The "instance" of what?-->

    ![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/free-trial.png)

    > Note: This trial instance has the following constraints:

    * Up to 100K rows in training data and up to 50K rows in prediction data
    * Up to 500 variables, features and columns
    * 30 days free trial

1. Click the **Workspace** button at the top, followed by the **My software** option on the left pane.

    ![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/software.png)

1. Click the operator you want, in this case **FP-Predict+**. You will be directed to the next page where you need to choose **Install operator** from the Operators menu.

    ![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/operator-install.png)

1. Under the Target clusters heading, check the box for the name of your cluster. Under "Namespace Scope", choose the project name you created in the previous step. You can leave the other default options and click **Install**. In this tutorial, we are choosing the automatic method of installation, but you can also choose to install the operator manually.

    ![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/sel-namespace.png)

1. After a couple of minutes, the operator is installed on the cluster. The status should change to be "Up to date". Launch the web console by clicking on the option next to Cluster Console.

    ![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/instld-optr.png)

1. In the web console, verify that you installed the operatory correctly by slecting **Operators** in the left navigation and by clicking on Installed Operators. The status should show that the installation succeeded.

   ![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/installed-operator.png)

## Create storage for the operator

1. Now that your operator is set up, you need to create persistent volume in the name of `fp-predict-plus-pv` to be bound to persistent volume claims. This step is necessary to enable storage capabilities for the operator to manage datasets. In the left navigation, Click **Storage > Persistent volume**. Update the name to `fp-predict-plus-pv` and set the storage capacity to 20 GB and hit **Create**. If you need more storage, you can increase it in the YAML file and create the persistent volume accordingly.

    ![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/create-pv.png)

1. You need to create a persistent volume claim (storage) to use the storage created in the previous step and bind it to the instance of this operator. On the web console, click on **Storage** and select **Persistent Volume Claims**.

    ![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/select-pvc.png)

1. The next step is to create a persistent volume claim. Choose the storage class you need &mdash; either gold, silver, or bronze. Add your name as `fp-predict-plus-pvc`, select single user access, and assign the storage size as 20 GB. 

    ![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/create-pvc.png)

1. After you create the persistent volume claim (PVC), you need to bind it with the persistent volume (PV) which you created in tye earlier step. You should see the status as `Bound` per below after couple of minutes.

    ![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/pvc-bound.png)

## Install the instance of FPPredict Plus

Click on Installed operators under `Operators` and click on FP Predict Plus Operator to get the options like Overview, YAML, Subscription, Events, FP-Predict-Plus. Click on YAML and update the name per below under persistent volume with `useExisting as false`, name of persistent volume claims, routerCanonicalHostname would be the web console URL and hit `Save`. routerCanonicalHostname would start with the cluster name, cluster id till appdomain.cloud. The initial part in the URL - `https://console-openshift-console` should be removed while updating routerCanonicalHostname.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/yaml-changes.png) <!--EM: Is this the wrong image? It doesnt' seem to go with teh text above-->

The next step is to proceed towards FP-Predict-Plus option and click on Create FPpredictplus instance. Edit the YAML file and give a name for the instance and click `Save`.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/operand.png)

### Launch the instance of FPPredict Plus

Now you are set to launch the instance. To do so, click on Networking and select Routes and then click on the URL which is under the location to launch the instance. 

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/route.png)
<!--EM: Is this the right image?-->

### Register the instance of FPPredict Plus

Log in using the default credentials as per the [configuration file](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/credentials.txt) and accept the end user license agreement. You will be directed to the next page as the following image shows. Click **Download** and share the file with the Findability Sciences support team. 

The support team will send the license file (with 30 days validity) and needs to be uploaded using the `Upload File` option. We are all set to access the instance of FPPredict Plus. 

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/sys-info.png)

After uploading the license key, bring up the `FP Predict+` instance like below. The navigation pane on the left should have four options:  Dashboard, Analytics, Dataset Management & License Information.

![](https://github.com/IBM/getting-started-with-fppredictplus/blob/master/images/fp-predict.png)

`Note` :- We may have to repeat all the steps if there is a version upgrade as some of the components from setup does not support product upgrades.

# Summary

This tutorial showed you how to install, configure, set up and add storage to get started using the FPPredict Plus operator from Red Hat Marketplace on OpenShift cluster to solve usecases under AI. Red Hat Marketplace is a one stop platform for exploring multiple operators which will help to solve some of the complex usecases under different domains. 

# Related Links

[Know more about FP Predict+ operator on RedHat Marketplace](https://marketplace.redhat.com/en-us/products/fp-predict)

