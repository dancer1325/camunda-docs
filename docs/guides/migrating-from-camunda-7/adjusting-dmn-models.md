---
id: adjusting-dmn-models
title: Adjust DMN models
description: "Learn how to adjust your DMN models when migrating from Camunda 7 to Camunda 8."
---

* [former community extension](https://github.com/camunda-community-hub/dmn-scala)
  * -- built by -- core Camunda developers
  * -- integrated with -- Camunda 8
* To evaluate Camunda 7 DMN files | Camunda 8 -> change the following | XML
  * `modeler:executionPlatform=Camunda Platform` -> `modeler:executionPlatform=CamundaCloud` (?)
    * `Camunda Platform` == compatibility with Camunda 7
  * `modeler:executionPlatformVersion=7.Y.Z` -> `modeler:executionPlatformVersion=8.2.0`
* Web Modeler
  * once you upload a DMN file -- will automatically update to the -- correct values for
    * `modeler:executionPlatform`
    * `modeler:executionPlatformVersion`
* elements/attributes are **NOT** supported | Camunda 8
  * `Version Tag`
  * `History Time to Live`
  * `Expression Language`
    * can NOT be selected
    * ONLY FEEL is supported
  * `Input Variable`
    * removed
    * 's value -- can be accessed by using -- `?` | FEEL 
* data types | Camunda 8
  * `integer` + `long` + `double` -- are replaced by -- `number` | inputs and outputs
    * == 1! number type (`BigDecimal`) | FEEL
