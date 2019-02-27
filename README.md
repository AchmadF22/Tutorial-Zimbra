# Tutorial-Zimbra

# zm-build

## Introduction

This repository contains the build script and supporting files required to create a [FOSS](https://en.wikipedia.org/wiki/Free_and_open-source_software) build of the [Zimbra Collaboration Suite](https://www.zimbra.com/). 

## Overview

* `build.pl` - Invoke this script to produce a build.  See the *Building* section 
  below for an example.
* `instructions/`
    * `FOSS_remote_list.pl` - Maps between remote label and URL
    * `FOSS_repo_list.pl` - Specifies which branches (or tags) are checked out to
      build each component repository.
    * `FOSS_staging_list.pl` - defines the staging order and details.

## Setup with Zimbra Development Images (used for building)

* Set up docker on your box
* You can then pull and run using development images (built from Zimbra/zm-base-os.git)
* In case you need to customze the images for your purposes, you could maintain your own Dockerfile such as this:


     cat Dockerfile
        FROM zimbra/zm-base-os:devcore-ubuntu-16.04
        RUN sudo apt-get install emacs my-special-tool etc..
        RUN ...

        docker build -t myuser/my-devcore-ubuntu-16 .
        docker run -it myuser/my-devcore-ubuntu-16 bash


### Ubuntu 16.04

    docker run -it zimbra/zm-base-os:devcore-ubuntu-16.04 bash

### Ubuntu 14.04

    docker run -it zimbra/zm-base-os:devcore-ubuntu-14.04 bash
