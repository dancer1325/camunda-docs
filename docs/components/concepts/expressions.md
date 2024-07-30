---
id: expressions
title: "Expressions"
description: "Expressions can be used to access variables and calculate values dynamically."
---

* uses
  * access variables
  * calculate values dynamically
* use cases
  * [automating a process using BPMN](../../guides/automating-a-process-using-bpmn.md)
  * [orchestrating human tasks](../../guides/getting-started-orchestrate-human-tasks.md)
  * BPMN elements' some attributes
    * _Example1:_ [sequence flow condition | exclusive gateway](/components/modeler/bpmn/exclusive-gateways/exclusive-gateways.md#conditions) 
    * _Example2:_ as an alternative to a static value -- [timer catch event's timer definition](/components/modeler/bpmn/timer-events/timer-events.md#timers) --

## Expressions vs. static values

* BPMN elements's some attributes can be defined in 2 ways -- _Example:_ timer catch event's timer definition -- :
  * As an expression (e.g. `= remainingTime`)
    * `= actualExpression`
      * syntax
        * 👁️`=` is mandatory as start 👁️
          * ⚠️if it's NOT used -> static value ⚠️
        * _Example:_ `= order.amount > 100`
    * if you use literals -> define static values -- _Example:_ `= "foo"`, `= 21`, `= true`, `= [1,2,3]`, `= {x: 22}` -- 
  * As a static value (e.g. `PT2H`)
    * allowed types
      * string -- _Example:_ `job type` --
        * ⚠️ NOT enclosed under quotes (' or ") ⚠️
      * number -- _Example:_ `job retries` --

## The expression language

* written in **Friendly Enough Expression Language (FEEL)**
  * Check [what's FEEL](../modeler/feel/what-is-feel.md) 
  * FEEL's properties
    * Free of side effects
    * Simple data model / JSON-like object types
      * numbers,
      * dates,
      * strings,
      * lists,
      * contexts
    * Syntax / -- designed for -- business professionals and developers
    * 3-valued logic (true, false, null)


## Next steps

* [Data types](/components/modeler/feel/language-guide/feel-data-types.md)
* [Expressions and operators](/components/modeler/feel/language-guide/feel-expressions-introduction.md)
* [Available built-in functions](/components/modeler/feel/builtin-functions/feel-built-in-functions-introduction.md)
* [FEEL](/components/modeler/feel/what-is-feel.md)
* [DMN specification](https://www.omg.org/spec/DMN/About-DMN/)
