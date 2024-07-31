---
id: processes
title: "Processes"
description: "Processes are flowchart-like blueprints that define the orchestration of tasks."
---

* processes
  * := flowchart-like blueprints / -- define the -- orchestration of **tasks**
    * _Example:_ you can [orchestrate human tasks](../../guides/getting-started-orchestrate-human-tasks.md) -- via -- Camunda
    * task
      * == piece of business logic / ordered execution -- produces a -- meaningful result
    * steps to run a process
      * deploy a process | Camunda 8
      * implement and register job workers -- for -- tasks | workflows
      * create new instances -- of -- said process
* **[job worker](./job-workers.md)**
  * implements the business logic / -- required to -- complete a task
  * requirements 
    * -- able to communicate with -- Camunda 8
      * Reason: 🧠 otherwise, there are NO restrictions | its implementation 🧠
  * ways to write a worker
    * as a microservice
    * as part of a classical 3-tier application,
    * as a \(lambda\) function,
    * via command line tools,
    * etc.
* ways to design the process

## BPMN 2.0
* := industry standard /
  * -- widely supported by -- different vendors and implementations
* used by
  * Zeebe ->
    * Zeebe <- can interchange processes with -> other process systems
* allows
  * representing processes
* [BPMN 2.0](http://www.bpmn.org/)

## BPMN modeler
* := BPMN modeling tool / 
  * == desktop application
  * -- based on the -- [bpmn.io](https://bpmn.io)
  * free 
  * open source
  * provided by Zeebe
  * allows
    * creating BPMN diagrams
    * configuring their technical properties
    * [automating a process using BPMN](../../guides/automating-a-process-using-bpmn.md) 
  * [downloaded from GitHub](https://camunda.com/download/modeler/)


## Sequences (of tasks)

* ordered sequence of tasks == simplest kind of process
* whenever process execution -- reaches a -- task -> Zeebe creates a job / can be
  * requested -- by a -- job worker
  * completed -- by a -- job worker

![process-sequence](assets/order-process.png)

* Zeebe's process orchestration
  * == state machine / steps
    1. As soon as process instance -- reaches a -- task -> Zeebe -- creates a -- job / -- can be requested by a -- worker
    2. Zeebe -- waits for the -- worker /
       1. request a job
       2. complete the work
    3. Once the work is complete -> flow -- continues to the -- next step
    4. If the worker -- fails to complete the -- work ->
       1.  process remains | current step
       2. job -- could be -- retried / until it's successfully completed

## Data flow
* Zeebe can move custom data (👁️-- via -- variables 👁️) | progress from one process' task -- to the -- next process's task
  * as soon as the job is completed -> job worker can read the variables and modify them
    * -> process's task1 <-- can share data with -> process's task2 

![data-flow](assets/process-data-flow.png)

## Data-based conditions

* 👁️some processes do NOT ALWAYS execute the same tasks 👁️
  * -> need to choose different tasks / -- based on --
    * variables and
    * conditions
  * diamond shape -- **X** --
    * := element / process can take >= 1 several paths  

![data-conditions](assets/processes-data-based-conditions.png)

## Events

* == things / happen
* process can
  * catching event
    * == react to events 
  * throwing event
    * == emit events 
* types
  * message
  * timer
  * error

![process](assets/process-events.png)

## Parallel execution
* multiple tasks / in parallel
  * diamond shape -- **+** --
    * == ALL outgoing paths are activated
  * JUST after both tasks have completed -> order is fulfilled  
* way to achieve it
  * parallel gateway

![data-conditions](assets/processes-parallel-gateway.png)

## Next steps
* [About Modeler](/components/modeler/about-modeler.md)
* [Automating a process using BPMN](/guides/automating-a-process-using-bpmn.md)
