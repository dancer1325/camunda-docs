---
id: decision-table-input
title: Input
description: Specify the inputs of decision tables.
---

![Input](assets/decision-table/input.png)

* input clause
  * == input of a decision table  
  * allowed >= 1
  * properties
    * id
    * label
    * expression
    * type
  * if you double-click | column header -> you can edit it
  * -- represented by -- `<input>` | `<decisionTable>`

    ```xml
    
    <definitions xmlns="https://www.omg.org/spec/DMN/20191111/MODEL/" id="definitions" name="definitions"
                 namespace="http://camunda.org/schema/1.0/dmn">
        <decision id="dish" name="Dish">
            <decisionTable id="decisionTable">
                <input id="input1" label="Season">
                    <inputExpression id="inputExpression1" typeRef="string">
                        <text>season</text>
                    </inputExpression>
                </input>
                <!-- ... -->
            </decisionTable>
        </decision>
    </definitions>
    ```

## Input id

* == unique identifier
* := decision table input's property / id
  * mandatory
  * uses
    * -- reference the -- input clause
  * -- represented by -- `<input id>` | `<decisionTable>`

    ```xml
    
    <input id="input1" label="Season">
        <inputExpression id="inputExpression1" typeRef="string">
            <text>season</text>
        </inputExpression>
    </input>
    ```

## Input label

![Input Label](assets/decision-table/input-label.png)

* := decision table input's property / short description
  * recommended, but NOT mandatory 
  * -- represented by -- `<input label>` | `<decisionTable>`

    ```xml
    
    <input id="input1" label="Season">
        <inputExpression id="inputExpression1" typeRef="string">
            <text>season</text>
        </inputExpression>
    </input>
    ```

## Input expression

![Input Expression](assets/decision-table/input-expression.png)

* := decision table input's property / -- how to generate the -- value of the input
  * usually
    * simple
    * -- references a -- variable / available | evaluation
  * Check input expression language -- [FEEL](/components/modeler/feel/language-guide/feel-expressions-introduction.md) --
  * -- represented by -- `<input><inputExpression><text>` | `<decisionTable>`

    ```xml
    
    <input id="input1" label="Season">
        <inputExpression id="inputExpression1" typeRef="string">
            <text>season</text>
        </inputExpression>
    </input>
    ```

## Input type definition

![Input Type Definition](assets/decision-table/input-type-definition.png)

* := decision table input's property / type 
  * recommended, but NOT mandatory
  * [allowed data types](dmn-data-types.md)
  * once input expression is evaluated -> it's checks if the result -- converts to the -- specified type
  * -- represented by -- `<input><inputExpression typeRef>` | `<decisionTable>`

    ```xml
    
    <input id="input1" label="Season">
        <inputExpression id="inputExpression1" typeRef="string">
            <text>season</text>
        </inputExpression>
    </input>
    ```
