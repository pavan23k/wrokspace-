# bpe_ui_rest
Blue Planet: Enterprise bpe_ui_rest  

#### Prerequisites

* Docker Image

* AWS account with permissions to push into ECR

* Kubernetes cluster


## Getting Started

* using the makefile we are creating and pushing it to ECR

* using the deployment scripts


**Bitbucket repository** -  https://bitbucket.ciena.com/projects/BP_ENTERPRISE/repos/bpe_ui_rest/browse


 **Build a pipeline in Teamcity using makefile Script**


**Teamcity :BP_Enterprise>UI Apps>Enterprise UI REST** https://teamcity.ciena.com/blueplanet/admin/editBuildRunners.html?id=buildType:bp_enterprise_ui_apps_bpe_ui

* Name: Enterprise UI REST

* Build configuration ID: bp_enterprise_ui_apps_bpe_ui_rest
---

**Create an image and push it to ECR**

#### Deploy the resources

 **->Build Step : Build and publish docker container**

* Name: Build and publish docker container

* Custom script: (Enter build script content):

```
#! /bin/bash

set -e

if [[ %teamcity.build.branch% == "master" || %teamcity.build.branch% == "release"* ]]
then
  make image
  make push
fi

```

_before running the build enable the build step_

* Run the build

* check the Build logs

* check if any errors in the build

* check the build is successful

* if the build is successful check the ECR services on AWS console

## AWS Console - ECR

* go to ECR services
* you can see the ECR Repository is created

```     		
Repository name : bpe_ui_rest
          Image :
        Image URL: 906862171241.dkr.ecr.us-east-1.amazonaws.com/bpe_ui_rest

```

**->Build Step : Deploying kubernetes Cluster**
This will deploy in dev namespace

* Name: deploy-dev

* Working directory: Blue Planet: Enterprise/bpe_ui_rest/k8s (add your Repository)

* Custom script: (Enter build script content):

```
make deploy_dev

```

* Run the build

* check the Build logs

* check if any errors in the build

* check the build is successful

* if the build is successful, you can see the cluster is create successfully

##### check the pods services in the dev namespace
~~~~
$Kubectl get pods,svc -n dev
~~~~
~~~
NAME                  TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
service/bpe-ui-rest   ClusterIP   10.100.136.177   <none>        8080/TCP   2d

NAME                               READY   STATUS    RESTARTS   AGE
pod/bpe-ui-rest-65bb7fd98c-8bkvx   2/2     Running   0          2d
~~~

##### bpe_ui_rest is running successfully
