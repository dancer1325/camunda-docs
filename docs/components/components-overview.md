---
id: components-overview
title: Introduction to Components
sidebar_label: Introduction to Components
slug: /components/
description: "This section contains product manual content for each component in Camunda 8, including conceptual content."
keywords: ["process automation tools"]
---
 
* Camunda 8 SaaS' components
  * [Concepts](concepts/what-is-camunda-8.md)
    * main concepts
      * clusters,
      * processes,
      * job workers,
      * workflow patterns
  * [Console](console/introduction-to-console.md)
    * allows
      * management application for the included products,
      * create and delete clusters,
      * manage API clients and alerts
      * ...
  * [Modeler](modeler/about-modeler.md)
    * Design and implement diagrams -- via -- Camunda's modeling tools
      * Web Modeler
      * Desktop Modeler
  * [Connectors](connectors/introduction.md)
    * == reusable building blocks / -- allows integrating with -- external systems
  * [Zeebe](zeebe/zeebe-overview.md)
    * allows
      * defining processes graphically | BPMN 2.0
        * choose any gRPC-supported programming language -- to implement your -- workers
        * processes -- can react to -- events (_Example:_ from Apache Kafka)
  * [Operate](operate/operate-introduction.md)
    * allows
      * monitoring and troubleshoot process instances / running | Zeebe,
      * carrying out key operations
        * _Example:_ resolving incidents, updating process instance variables
  * [Tasklist](tasklist/introduction-to-tasklist.md)
    * == interface / -- for -- manual work
    * allows
      * implementing business processes + user tasks | Zeebe,
      * orchestrating human workflows / critical to your business to
        * -> reduce time-to-value 
  * [Optimize]($optimize$/components/what-is-optimize)
    * uses
      * business stakeholders
    * == business intelligence tooling -- for -- Camunda enterprise customers
    * -- based on -- data collected during process execution

![Architecture diagram for Camunda including all the components for SaaS](./img/ComponentsAndArchitecture_SaaS.png)

* [Best Practices](./best-practices/best-practices-overview.md)
* [Deployment guides for Camunda 8 components](/self-managed/about-self-managed.md)
