---
title: "Collection of commands and utilities for quick look-up"
layout: post
date: 2021-02-04 07:17
image: 
headerImage: false
tag:
- bash
star: true
category: blog
author: prashant
hidden: false
description: Collection of commands and utilities for quick look-up.
---

- Cleaning resources in kubernetes namespace:

  ```bash
  kubectl get pods -n mynamespace --no-headers=true | awk '/pattern1|pattern2/{print $1}'| xargs kubectl delete -n mynamespace pod
  ```

  [Source](https://medium.com/faun/delete-kubernetes-pods-with-a-regex-f396291bba0e)

- Yes/no prompt in bash.
  
  This snippet will give a yes/no prompt if `INPUT_PATH` variable is a directory.

  ```bash
  if [ -d "$INPUT_PATH" ]; then
    read -r -p "Given path is a directory. Continue? [Y/n] " input
    case $input in
        [yY][eE][sS]|[yY])
    echo "Yes"
    # add commands that you want to run when user says yes here
    ;;
        [nN][oO]|[nN])
    echo "No"
    echo "Aborting"
    exit 0
    ;;
        *)
    echo "Invalid input..."
    exit 1
    ;;
    esac
  fi
  ```

- *Add more here*
