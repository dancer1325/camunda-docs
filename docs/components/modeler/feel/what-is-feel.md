---
id: what-is-feel
title: What is FEEL?
description: "FEEL is a part of DMN specification of the Object Management Group."
---

import { MarkerCamundaExtension } from "@site/src/mdx/MarkerCamundaExtension";

* **Friendly Enough Expression Language (FEEL)**
  * specified in [Object Management Group - DMN specification](https://www.omg.org/spec/DMN/) 
  * allows
    * writing expressions / easily understood
  * uses | Camunda
    * define expressions | [BPMN diagrams](/components/modeler/bpmn/bpmn.md), [DMN diagrams](/components/modeler/dmn/dmn.md), and [Forms](/components/modeler/forms/camunda-forms-reference.md)

## Learning FEEL

* [Expressions in Camunda 8](/components/concepts/expressions.md)
* [FEEL syntax and operators](./language-guide/feel-expressions-introduction.md)
  * how to write basic expression
* [Built-in functions](./builtin-functions/feel-built-in-functions-introduction.md)


## FEEL engines
* TODO:
To evaluate your expressions, Camunda employs two distinct FEEL engines depending on the use-case: FEEL Scala (the Java FEEL engine) and feelin (the JavaScript FEEL engine). Both support the basic FEEL syntax and functions. You can try out your expressions in our playgrounds outlined below.

### FEEL Scala (Java FEEL engine)

[**FEEL Scala**](https://github.com/camunda/feel-scala) is a Java-based FEEL engine integrated into the backend of our platform. It is primarily responsible for evaluating expressions in BPMN diagrams and DMN tables.

:::info <a id="camunda-extensions">info</a>

The FEEL Scala engine supports a set of extensions to standard DMN FEEL. The documentation marks them via the following tag:

<MarkerCamundaExtension />
:::

Try out expressions in the [FEEL Scala Playground](https://camunda.github.io/feel-scala/docs/playground/).

### feelin (JavaScript FEEL engine)

[**feelin**](https://github.com/nikku/feelin) is a JavaScript-based FEEL engine designed for use in the browser is used for [Camunda Forms](../forms/camunda-forms-reference.md) and [templating](../forms/configuration/forms-config-templating-syntax.md). [Camunda extensions](#camunda-extensions) are **not** currently supported by feelin.

Try out expressions in the [feelin Playground](https://nikku.github.io/feel-playground/).
