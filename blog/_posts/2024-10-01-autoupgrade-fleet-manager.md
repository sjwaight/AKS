---
title: "Automatically update your AKS clusters with Azure Kubernetes Fleet Manager's Autoupgrade capability"
description: "Keep your Kubernetes and node images up to date across your entire fleet."
date: 2024-10-01
author: Simon Waight
categories:
- operations
- security
tags:
- fleet-manager
- updates
- multi-cluster
---

## Introduction

A common challenge for cluster administrators is ensuring that Kubernetes and node image versions are updated across all their clusters as new releases are published. 

Today, Azure Kubernetes Fleet Manager (Fleet) provides administrators with the ability to configure and manually execute [Update Runs](https://learn.microsoft.com/azure/kubernetes-fleet/concepts-update-orchestration) for their Fleet-managed clusters.

Administrators can elect to update clusters one-by-one, or control the order by defining a Staged run that contains Groups and Stages. The rules for Staged runs are:

- Stages run in sequence.
- Groups run in parallel.
- Clusters run one-by-one.

Update runs [honor maintenance windows](https://learn.microsoft.com/azure/aks/planned-maintenance) configured at the individual cluster level.

A sample Staged update run definition is shown below.

![Update run showing two Stages with two Groups in each.](/AKS/assets/images/fleet-autoupgrade/update-run-sample.png)
_Update run showing two Stages with two Groups in each_

Using update runs, administrators must still monitor for new releases and then manually execute an update run to publish the update their clusters.

## Automatically trigger update runs

In October 2024, Azure Kubernetes Fleet Manager introduced a new feature that provides fleet administratrors with a mechanism to automatically execute update runs when new Kubernetes of node images are publised by Azure.

Let's take a look at how to use the new `autoupgrade profile` to trigger update runs in certain scenarios.


## Summary

TBC

**Resources**

- [Kubernetes Fleet Roadmap](https://aka.ms/fleet/roadmap)
