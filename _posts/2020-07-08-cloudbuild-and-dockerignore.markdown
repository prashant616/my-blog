---
title: "Google Cloud Build ignores .dockerignore"
layout: post
date: 2020-07-07 17:26
image: 
headerImage: false
tag:
- gcloud
- cloudbuild
- dockerignore
- gcloudignore
star: false
category: blog
author: prashant
hidden: false
description: Reducing the size of archive uploaded by `gcloud` commands.
---

I often use Google Cloud Build for building docker images in my projects. To submit a cloudbuild job, [`gcloud builds submit`](https://cloud.google.com/sdk/gcloud/reference/builds/submit) command is used.

## Problem

If you have some files or directories inside your project that you have added to `.dockerignore`, `gcloud` will still upload these files/directories as build context. This will make the size of archive that is uploaded larger and thus increasing your build time. This is because `gcloud` by default only ignores the files present in [`.gcloudignore`](https://cloud.google.com/sdk/gcloud/reference/topic/gcloudignore) and if, `.gcloudignore` file is not present, it will automatically generate a `.gcloudignore` file that respects `.gitignore` but not `.dockerignore`.

## Solution

Add a `.glcloudignore` file in the root of your project directory with contents as follow:

```
.gcloudignore
#!include:.gitignore
#!include:.dockerignore
```

Now, `gcloud` will not upload the files and directories listed in `.gitignore` as well as `.dockerignore` and the `.gcloudignore` file itself.  
This will work not only for `gcloud builds submit` command but other gcloud commands that upload the contents of the project directory, as well like `gcloud container builds submit` and `gcloud app deploy` commands.
