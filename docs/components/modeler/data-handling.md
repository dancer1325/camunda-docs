---
id: data-handling
title: Data handling
description: "Get editor support for variables by defining the variables in the process model."
---

* <span class="badge badge--cloud">Camunda 8 only</span>
* FEEL editor
  * TODO: Which one?
  * once you define input and output mappings | process -> will suggest variables | current element's scope
    * variables / created by the mapping -> are automatically picked up and added to the suggestions
    * if you want editor support -- for -- 
      * variables / 
        * created by your [job workers](../concepts/job-workers.md) or 
        * passed as process start variables
      * -> define the variables | process model

## Defining additional data

* schema for this data
  * way to add
    * add a JSON / return 
      * value | properties panel's `Data` section
        * use of values
          * derive variable names | FEEL editor 
          * derive types | FEEL editor
      * nested objects
  * uses of the schema
    * by the FEEL editor -- to provide -- variable suggestions / modeling
    * by Play -- to prefill -- variable forms
    * NOT | process execution
* provide this data
  * optional, BUT it's recommended
    * Reason: 🧠take full advantage of the FEEL editor's suggestions 🧠
* uses of this data
  * during [playing your process](/components/modeler/web-modeler/play-your-process.md) -- allows -- prefilling the modal
    * requirements
      * being performing the actions
        * Start a new instance with variables
        * Complete job with variables
        * Publish message with variables
    * added | scope of the element
      * Check [variable concepts page](../concepts/variables.md) 
    * if you want to use | other parts of your process -> use output mappings (-> variables | parent scope) 

![Variable suggestions with additional Variables](img/data-handling-example-json.png)
