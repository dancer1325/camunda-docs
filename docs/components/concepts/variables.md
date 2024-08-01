---
id: variables
title: "Variables"
description: "Variables are part of a process instance and represent the data of the instance."
---

* Variables
  * == part of a process instance
  * == instance's data
    * == name + JSON value
    * == key / value
  * visibility
    * -- defined by -- its variable scope
    * uses
      * customize how variables -- are merged -- | process instance
    * use cases
      * [automating a process using BPMN](../../guides/automating-a-process-using-bpmn.md) or
      * [orchestrating human tasks](../../guides/getting-started-orchestrate-human-tasks.md) 
  

## Variable names

* allowed
  * ANY alphanumeric string
  * `_`
  * if you want to combine words -> use
    * `camelCase` or
    * `snake_case`
    * ❌`kebab-case` NOT allowed ❌
      * Reason: 🧠 contains the operator `-` 🧠
* restrictions
  * NOT start / **number** -- _Example:_ `1stChoice` --
  * NOT contain / 
    * **whitespaces**  -- _Example:_ `choice other` --
    * **operator** -- _Example:_ `+`, `-`, `*`, `/`, `=`, `>`, `?`, `.` --
  * NOT **literal** -- _Example:_ `null`, `true`, `false` --
  * NOT **keyword**  -- _Example:_ `function`, `if`, `then`, `else`, `for`, `between`, `instance`, `of`, `not` --
* case-sensitive


## Variable values

* stored - as a -- JSON value
* allowed types
  * String -- _Example:_ `"John Doe"` --
  * Number -- _Example:_ `123`, `0.23` --
  * Boolean -- _Example:_ `true` or `false` --
  * Array -- _Example:_ `["item1" , "item2", "item3"]` --
  * Object -- _Example:_ `{ "orderNumber": "A12BH98", "date": "2020-10-15", "amount": 185.34}` --
  * Null  == `null`

## Variable size limitation

* process instance's payload / include variables + workflow engine internal data <= 4 MB
  * == NOT ALL can be used by variables JUST
  * average allowed variable's size <= 3 MB 
  * [Check best practice | handling data in processes](/components/best-practices/development/handling-data-in-processes.md) 
  * workflow engine internal data's size -- depends on -- factors

## Variable scopes

* == variable's  _visibility_
  * defined | variable creation 
* root scope
  * == process instance itself
  * variables | root scope -> visible EVERYWHERE | process
  * default scope | variables are created
* once process instance enters | subprocess or activity -> new scope is created
  * activities | this scope -- can observe -- ALL variables parent scopes (== this & higher scopes)
  * activities / outside of this scope -- can NOT observe -- variables / defined | this scope
* if variableName == variableName / higher scope -> it covers this variable
  * activities | this scope -- observe -- 
    * ONLY the value of this variable
    * NOT the one / higher scope
* _Example:_

    ![variable-scopes](assets/variable-scopes.png)

    * process instance's variables
      * `a` and `b`
        * defined | root scope
        * -- can be seen by --
          * **Task A**,
          * **Task B**,
          * **Task C**
      * `c`
        * defined | subprocess scope
        * -- can be seen by --
          * **Task A**
          * **Task B**
      * `b`
        * defined | **Task A**'s activity scope
        * -- can be seen --
          * ONLY by **Task A**

### Variable propagation

* == from the scope of the activity -- variable is propagated to -- its higher scopes 
  * use cases
    * variables -- are merged into -- process instance ( _Example:_ | job completion, | message correlation)  
  * if scope / contains a variableName = variableToPropagateName -> propagation ends
    * ->  variable value is updated
  * if NO scope / contains this variableToPropagate -> new variable is created | root scope
* _Example:_
    ![variable-propagation](assets/variable-propagation.png)
  * **Task B** jobs -- is completed with the -- variables `b`, `c`, and `d`
    * Reason: 🧠 variables `b` and `c` are ALREADY defined | higher scopes & are updated with the new values 🧠
    * Variable `d` does NOT exist before and is created | root scope

### Local variables

* == variables set | given scope
  * even if they do NOT exist | this scope, before
* allows
  * deactivating the variable propagation

## Input/output variable mappings

* allows
  * creating NEW variables or 
  * customizing how variables -- are merged -- into the process instance
* defined as extension elements | `ioMapping`
* == `source`expression + `target` expression
  * `source`expression
    * -- defines the -- **value** of the mapping
    * uses
      * [accesses a variable](/components/modeler/feel/language-guide/feel-variables.md#access-variable) of the process instance / holds the value
        * if the variable or the nested property does NOT exist -> value `null`
  * `target` expression
    * -- defines -- **where** the value of the `source` expression is stored
    * It can reference a variable by its name or a nested property of a variable. If the variable or the nested property doesn't exist, it's created.
* evaluated | defined order
  * `source` expression -- can access the -- previous mapping's target variable 

![variable-mappings](assets/variable-mappings.png)

**Input mappings**

| Source          | Target      |
| --------------- | ----------- |
| `customer.name` | `sender`    |
| `customer.iban` | `iban`      |
| `totalPrice`    | `price`     |
| `orderId`       | `reference` |

**Output mapping**

| Source   | Target          |
| -------- | --------------- |
| `status` | `paymentStatus` |

### Input mappings

* TODO:
Input mappings can be used to create new variables. They can be defined on service tasks and subprocesses.

When an input mapping is applied, it creates a new **local variable** in the scope where the mapping is defined.

For string literals containing escaped characters (e.g., a newline character `\n`), the string is returned in its original form as expected (without double escaping).

Examples:

| Process instance variables             | Input mappings                                                                                               | New variables                               |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------ | ------------------------------------------- |
| `orderId: "order-123"`                 | **source:** `=orderId`<br/> **target:** `reference`                                                          | `reference: "order-123"`                    |
| `customer:{"name": "John"}`            | **source:** `=customer.name`<br/>**target:** `sender`                                                        | `sender: "John"`                            |
| `customer: "John"`<br/>`iban: "DE456"` | **source:** `=customer`<br/> **target:** `sender.name`<br/>**source:** `=iban`<br/>**target:** `sender.iban` | `sender: {"name": "John", "iban": "DE456"}` |

### Output mappings

Output mappings can be used for several purposes:

- To customize how variables are merged into the process instance.
- They can be defined on service tasks, receive tasks, message catch events, and subprocesses.
- They can be used in script and user tasks.

If **one or more** output mappings are defined, the results variables are set as **local variables** in the scope where the mapping is defined. Then, the output mappings are applied to the variables and create new variables in this scope. The new variables are merged into the parent scope. If there is no mapping for a job/message variable, the variable is not merged.

If **no** output mappings are defined, all results variables are merged into the process instance.

In the case of a subprocess, the behavior is different. There are no results variables to be merged. However, output mappings can be used to propagate **local variables** of the subprocess to higher scopes. By default, all **local variables** are removed when the scope is left.

Examples:

| Results variables                                    | Output mappings                                                                                                                      | Process instance variables                         |
| ---------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------- |
| `status: "Ok"`                                       | **source:** `=status`<br/>**target:** `paymentStatus`                                                                                | `paymentStatus: "OK"`                              |
| `result: {"status": "Ok", "transactionId": "t-789"}` | **source:** `=result.status`<br/>**target:** `paymentStatus`<br/>**source:** `=result.transactionId`<br/>**target:** `transactionId` | `paymentStatus: "Ok"`<br/>`transactionId: "t-789"` |
| `status: "Ok"`<br/>`transactionId: "t-789"`          | **source:** `=transactionId`<br/>**target:** `order.transactionId`                                                                   | `order: {"transactionId": "t-789"}`                |

### Context variable

A context variable is a reserved variable that describes the context of a task. It can group variables together to provide a detailed description of the task or offer more descriptive data about it.
The reserved variable name for a context variable is `taskContextDisplayName`. This name is reserved exclusively for this purpose and should not be used for other variables.

Example:

| Input variable           | Example                              |
| ------------------------ | ------------------------------------ |
| `taskContextDisplayName` | `This is a context variable example` |

The data from the variable will be shown on the task tile, as shown in the example below:

![context-variables](assets/context-variables.png)

## Next steps

- [Access variables](/components/modeler/feel/language-guide/feel-variables.md#access-variable)
