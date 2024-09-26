---
title: "Automatically update your AKS clusters with Azure Kubernetes Fleet Manager Autoupgrade"
description: "Keep your Kubernetes and node images up to date across your entire fleet."
date: 2024-09-26
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

Today, Azure Kubernetes Fleet Manager (Fleet) provides administrators the ability to configure and manually execute [update runs](https://learn.microsoft.com/azure/kubernetes-fleet/concepts-update-orchestration) for their Fleet-managed clusters.

These update runs can sequentially update all clusters in a fleet, or use a administrator-defined staged process to determine the ordering of updates.

In all cases, update runs [honor maintenance windows](https://learn.microsoft.com/azure/aks/planned-maintenance) configured at the individual cluster level.

A sample staged update run definition is shown below.

![Update run showing two Stages with two Groups in each.](/AKS/assets/images/fleet-autoupgrade/update-run-sample.png)
_Update run showing two Stages with two Groups in each_

Staged update runs can be saved as strategies which act as a reusable process template  

When using update runs, administrators must still manually execute an update run to publish updates when new Kubernetes or node images are released.

## Autoupgrade - automatically trigger update runs

In October 2024, Azure Kubernetes Fleet Manager introduced a new feature that provides automatic execution of update runs when new Kubernetes of node images are publised to Azure.

This capability was first introduced in the v1.3 release of the Azure CLI fleet extension.

Let's take a look at what's involved in setting up an autoupgrade when using the Azure CLI. For the purpose of this post we'll configure autoupgrade as follows:

- Run using a staged strategy based on the above sample.
- Update clusters on a Stable Kubernetes release (if latest Kubernetes minor release is 1.31, Stable is 1.30)

```bash
export GROUP=<resource-group>
export FLEET=<fleet-name>
export AUTOUPGRADEPROFILE=<upgrade-profile-name>

STRATEGYID=$(az fleet updatestrategy show --resource-group <my-fleet-rg> --fleet-name <my-fleet-name> --name "update-run-01" --query "id")

az fleet autoupgradeprofile create \
  --resource-group $GROUP \
  --fleet-name $FLEET \
  --name $AUTOUPGRADEPROFILE \
  --update-strategy-id $STRATEGYID \
  --channel Stable
```

At this stage we now have an `autoupgradeprofile` that will ensure the next time Azure publishes a new release to the Stable channel the the selected update strategy will be used to push the update through the fleet's clusters.

TODO: add updaterun view


## Summary

TBC

**Resources**

- [Kubernetes Fleet Roadmap](https://aka.ms/fleet/roadmap)
