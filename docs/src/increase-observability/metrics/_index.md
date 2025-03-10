---
title: Monitor metrics
weight: 5
description: See all of the live infrastructure metrics available to give you an overview of resource usage.
aliases:
  - /dedicated/architecture/metrics.html
---

Platform.sh projects are accompanied by live infrastructure metrics that provide an overview of resource usage for environments.  

Within the console, metrics can be found for an environment under **Metrics**.

The information under **Metrics** shows usage metrics for:

[Dedicated environments](../../dedicated/overview/_index.md):
each of the three hosts in your [N+1 configuration](../../dedicated/architecture/_index.md)
and their average for the Production environment.

![A screenshot of what the metrics dashboard displays for Dedicated environments](/images/metrics/all-dedicated.png "0.45")

Grid environments: your service, app, and worker containers.

![A screenshot of what the metrics dashboard displays for Grid environments](/images/metrics/all-grid.png "0.45")

{{% legacy-regions featureIntro="Infrastructure metrics" featureShort="infrastructure metrics" plural=true %}}

## Default thresholds

All of the graphs show labels for the following thresholds:

* Usage that crosses _80%_ results in a **warning** label.
* Usage that crosses _90%_ results in a **critical** label.
* On Grid environments only, usage that crosses _100%_ results in a **burst** label.

  The burst capability is available for containerized environments
  and allows a container to get more resources than it's allocated.
  Burst is considered useful for infrequent activities that cause usage spikes,
  but these additional resources aren't guaranteed.

### Recommendations

The default thresholds aim to give you an idea of when your hosts/containers are close to running out of resources.
The impact differs based on your specific apps and service.
The values of the thresholds is purely informational.

#### Dedicated environments

For Dedicated environments, the thresholds are set for each host.
If the resources are high and hovering close to the 100% threshold,
you might want to consider:

* [Optimizing your code](../integrate-observability/_index.md) (if possible)
* [Increasing your plan](../../overview/pricing/_index.md)

#### Grid environments
  
For Grid environments, the thresholds are set for each container.
If the resources are high and hovering close to the 100% threshold,
you might want to consider:

* [Optimizing your code](../integrate-observability/_index.md) (if possible)
* Changing your [app size](../../create-apps/app-reference.md#sizes)
  or [service size](../../add-services/_index.md#size)
* [Increasing your plan](../../overview/pricing/_index.md)

If your containers are in a prolonged burst state,
review your configuration or plan size because burst isn't guaranteed for long periods.
If the burst threshold is triggered for short, infrequent activities,
it might not be an issue as long as the site is functioning properly.
Burst allows your container to use additional resources when they aren't required on the container's host.

## Time intervals

Measurements are taken for each metric _every ten seconds_ for Dedicated environments and _every 1 minute_ for Grid environments.
You can select a time frame over which to see these measurements for the entire **Metrics** view.
In the primary three views, averages are shown over larger intervals.

| View                                                                  | Time between measurements                     | Example                      |
| :-------------------------------------------------------------------- | :-------------------------------------------- | :--------------------------- |
| The last 15 minutes (*15m*)                                           | 10 seconds for Dedicated, 1 minute for Grid   | 10:00:10, 10:00:20, 10:00:30 |
| The last hour (*1hr*)                                                 | 1 minute                                      | 10:00, 10:01, 10:02          |
| The last 24 hours (*24hr*) for Dedicated and 8 hours (*8hr*) for Grid | 20 minutes for Dedicated, 10 minutes for Grid | 10:00, 10:20, 10:40, 11:00 |

To zoom in on smaller intervals, select specific ranges in a graph.

{{< video src="videos/metrics/metrics-zoom.mp4" >}}

The interval between measurements then changes based on the range you choose.

| View                  | Time between measurements                   |
| :-------------------- | :------------------------------------------ |
| < 30 minutes          | 10 seconds for Dedicated, 1 minute for Grid |
| 30 minutes to 2 hours | 1 minute                                    |
| 2 to 5 hours          | 5 minutes                                   |
| 5 to 8/24 hours       | 20 minutes                                  |
