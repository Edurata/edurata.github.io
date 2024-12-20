---
layout: default
title: Metering
has_children: true
nav_order: 9
---

# Metering

In order to run any workflow in a [deployment](../deployments/index.md) or use storage (for artefacts or function code) so-called `execution units` or runner units need to be available which act as the "currency" in which processes on the `Edurata workflows` platform are measured.

The "exchange rate" of `execution units` are the following:

1 unit = `1 minute` of used runner time = `10 MB` new used storage. 

The storage is only used for artefacts and function code and the limit will rarely be met for normal sized applications. 

## Calculation of Runner Time and used units

{: .info}
The runner time is the time that the runner is actually executing a function. The time that the runner is waiting for a function to be executed is not counted towards the runner time. In the same way, time that steps are running in parallel or in loops is counted towards the runner time. The runner time might therefore be higher or lower than the actual time that the workflow takes to execute.

### Rounding

The runner time is measured in seconds and rounded up to the next minute. For example, if a function runs for 1 minute and 1 second, it will be counted as 2 minutes. 

All steps will be added together for the runner time before rounding. For example, if a function runs for 1 minute and 1 second in step 1 and 1 minute and 1 second in step 2, the total execution time is 2 minutes and 2 seconds which will be rounded up to 3 minutes.

### Foreach loops
 
In the case of foreach steps the time is counted for each iteration of the loop. For example, if a foreach loop runs for 1 minute and 1 second in each iteration and there are 3 iterations, the total execution time is 3 minutes and 3 seconds which will go into the calculation of the total runner time.

### Scaling factor for resources

If a step uses different resources than the default (e.g. more memory or more CPU) the runner time will be scaled accordingly. For example, if a step uses 2 CPUs and 4 GB of memory, the runner time of the step will be multiplied by 2 before being included in the calculation of the total runner time.