---
title: "Creating GKE cluster using command line"
layout: post
date: 2020-02-10 22:32
image: 
headerImage: false
tag:
- kubernetes
- GKE
- GCP
star: false
category: blog
author: prashant
hidden: false
description: How to create a GKE cluster using gcloud from command line
---

1. Enable the [Kubernetes Engine API](https://console.cloud.google.com/apis/api/container.googleapis.com/overview) for your GCP project from <https://console.cloud.google.com>

2. Install the [Google Cloud SDK](https://cloud.google.com/sdk/docs/#install_the_latest_cloud_tools_version_cloudsdk_current_version) which includes gcloud command line tools.

3. Install `kubectl` which is a command line tool for controlling Kubernetes clusters. To install it as part of the Google Cloud SDK, use:

   ```bash
   gcloud components install kubectl
   ```

   otherwise, visit <https://kubernetes.io/docs/tasks/tools/install-kubectl/>

4. Set default GCP project:

   ```bash
   gcloud config set project <YOUR-GCP-PROJECT-ID>
   ```

6. Set default compute zone:

   ```bash
   gcloud config set compute/zone <COMPUTE-ZONE>
   ```

7. Create a 3 node cluster with `n1-standard-1` machine type:

   ```bash
   gcloud container clusters create <CLUSTER-NAME> \
      --num-nodes=3 \
      --machine-type=n1-standard-1 
   ```

8. Get authentication credentials for the cluster to configure `kubectl` to use the created cluster:

   ```bash
   gcloud container clusters get-credentials <CLUSTER-NAME>
   ```

9. Check if cluster is initialized:

   ```bash
   kubectl get node
   ```

   You will see output something like:

   ```raw
   NAME                                         STATUS   ROLES    AGE   VERSION
   gke-dev-cluster-default-pool-8206a99e-0shr   Ready    <none>   16h   v1.13.11-gke.23
   gke-dev-cluster-default-pool-8206a99e-d9f6   Ready    <none>   16h   v1.13.11-gke.23
   gke-dev-cluster-default-pool-8206a99e-fcfk   Ready    <none>   16h   v1.13.11-gke.23
   ```