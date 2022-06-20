# Migrating Spring Boot Petclinic application tutorial 

---
**NOTE**
This tutorial is relevant to Migrate to Containers version 1.11.1 or newer
---
[Spring Boot Petclinic application](https://github.com/spring-projects/spring-petclinic) is a Java application built with [Spring Boot](https://spring.io/projects/spring-boot) and [Maven](https://maven.apache.org/).

In this tutorial you will deploy this application into a Tomcat server running on a [Google Compute Engine (GCE)](https://cloud.google.com/compute) VM and connect it to a [MySQL](https://www.mysql.com/) database running on a GCE VM.

You'll then modernize this application by using [Migrate to Containers (M2C)](https://cloud.google.com/migrate/containers) to migrate it to run in a Tomcat app container on a [Google Kubernetes Engine (GKE)](https://cloud.google.com/kubernetes-engine) cluster and generate Day2 artifacts to support modern CI/CD operations for your application. Unlike the [petclinic](../petclinic) guide, where we migrated the Tomcat into a Linux system container, in this guide we will extract the applications and Tomcat specific configuration and create a Tomcat Docker image for it.

## What you'll do

In this tutorial you’ll do the following:

* Prepare your Google Cloud environment
* Create a MySQL Ubuntu VM on GCE  and prepare the Petclinic database
* Build and deploy Petclinic application into Tomcat on a GCE vm
* Install and configure M2C
* Qualify the workloads for migration using the M2C [Migrate Fit Assessment (mFIT)](https://cloud.google.com/migrate/containers/docs/fit-assessment)
* Migrate Petclinic database vm to a container
* Migrate Petclinic application to a Tomcat container
* Deploy the migrated database and application to your GKE cluster
* Optimize Tomcat deployment
* Create a Continuous Integration (CI) pipeline to automatically build a new Tomcat image when the application is changed
* Clean up by deleting the project

## Before you begin

For this reference guide, you need a Google Cloud project. You can create a new one, or select a project you already created:

1. Select or create a Google Cloud project.  
[GO TO THE PROJECT SELECTOR PAGE](https://console.cloud.google.com/cloud-resource-manager)

2. Enable billing for your project.  
[ENABLE BILLING](https://support.google.com/cloud/answer/6293499#enable-billing)

3. Enable the Service Management API, Service Control API, Cloud Resource Manager API, Compute Engine API, Kubernetes Engine API, Google Container Registry API, Cloud Build API, Cloud Source Repositories API.  
[ENABLE THE APIS](https://console.cloud.google.com/flows/enableapi?apiid=servicemanagement.googleapis.com%20servicecontrol.googleapis.com%20cloudresourcemanager.googleapis.com%20compute.googleapis.com%20container.googleapis.com%20containerregistry.googleapis.com%20cloudbuild.googleapis.com%20sourcerepo.googleapis.com)

## Begin your migration journey
Your migration journey consist of a number of steps:  
1. [Prepare](1-prepare/README.md) - In this step you will prepare your environment by installing MySQL and Tomcat VMs, building and deploying the application and then installing Migrate to Containers.
2. [Assess](2-assess/README.md) - In the assess step, you will run the Migrate to Containers fit assessment and assess whether or not your MySQL and Tomcat workloads are good fit for containerization.
3. [Migrate](3-migrate/README.md) - In the migrate step you will migrate both of your VMs into containers and generate Day2 artifacts which can later be used in modern CI/CD pipelines.
4. [Deploy](4-deploy/README.md) - In the deploy step you will deploy your migrated workloads into a GKE cluster and verify that your application is working as expected.
5. [Optimize](5-optimize/README.md) - In the optimize step you will learn how to manually and automatically scale your migrated workloads and how to roll out application updated.
6. [Day2](6-day2/README.md) - Once migrated and optimized it is advised to adopt modern CI/CD practices to build and deploy your migrated workflows post migration. In this step you'll go through an opinionated CI implementation using [Cloud Source Repositories](https://cloud.google.com/source-repositories) and [Cloud Build](https://cloud.google.com/build).

## Cleaning up
The simplest way to avoid any unexpected billing charges is to delete your GCP project. You can do so by running the command below in cloud shell:
```
gcloud projects delete $PROJECT_ID
```