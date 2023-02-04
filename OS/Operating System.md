---
title: Operating System
created: '2021-07-09T01:12:29.013Z'
modified: '2021-07-13T01:42:25.532Z'
---

# Operating System

## Strategies for handling deadlock

1. Deadlock ignorance
2. Deadlock prevention
3. Deadlock avoidance
4. Deadlock detection and recovery

## Deadlock Prevention

Disabling or preventing the conditions that can lead to deadlock will prevent deadlock.

Condition | Approach

1. Mutual Exclusion - resource can only be used by one process | Spool everything - drop all jobs in pool and resource will be processing them one by one
2. Hold and wait - hold the remaining resources and wait for others | Request all resources initially - neither hold nor wait. It's difficult to know what resources may be needed beforehand.
3. No preemption | take resources away
4. Circular wait | order resources numerically and allocate resources in increasing order. So, there will be no cycle.

Preventing circular wait is only possible for prevention of deadlock.
