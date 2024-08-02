---
id: index
title: Pre-migration details
description: "Migrate process solutions developed for Camunda 7 to run them on Camunda 8."
keywords:
  [
    Camunda 8,
    Camunda 7,
    migration guide,
    transition,
    transition guide,
    Camunda 7,
  ]
---

* existing projects | Camunda 7 -- to -- Camunda 8 is OPTIONAL
* Camunda 7 still has ongoing [support](https://docs.camunda.org/enterprise/announcement/)
* Guide to migrate process solutions | Camunda 7 -> | Camunda 8 / topics
  * compare application architecture
  * migration can be done
    * for
      * process models
      * code
    * NOT for
      * runtime
      * history data
  * complexity of the migration -- depends on -- process models
  * code / uses the workflow engine API -- need to be -- adjusted
  * community extensions / can help with migration
  * Clean Delegate approach,
    * which helps you write Camunda 7 solutions that are easier to migrate


## What to expect

- [Conceptual differences](./conceptual-differences.md)
- [Migration readiness](./migration-readiness.md)
- [Adjusting BPMN models](./adjusting-bpmn-models.md)
- [Adjusting DMN models](./adjusting-dmn-models.md)
- [Adjusting source code](./adjusting-source-code.md)

## Open issues

* this guide is FAR from complete
  * Open issues
    * implications | testing
    * adapters for Java or REST client
    * more concepts around BPMN:
      * [Field injection](https://docs.camunda.org/manual/latest/user-guide/process-engine/delegation-code/#field-injection) that is using `camunda:field` available on many BPMN elements.
      * Multiple instance markers available on most BPMN elements.
      * `camunda:inputOutput` available on most BPMN elements.
      * `camunda:errorEventDefinition` available on several BPMN elements.
    * workload migrations (operations)
    * Eventual consistency

[Reach out to us](/contact/) to discuss your specific migration use case.
