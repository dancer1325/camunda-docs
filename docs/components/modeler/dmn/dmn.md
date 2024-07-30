---
id: desktop-modeler-dmn
title: DMN in Modeler
description: "Camunda Desktop and Web Modeler both offer the same Modeling experience for DMN 1.3 models: Modeling starts in the Decision Requirements Diagram (DRD) view."
---

## Start modeling

![Start Modeling](assets/desktop-modeler-dmn/main.png)

* Modeling experience for DMN 1.3 models
  * ways
    * Camunda Desktop
    * Camunda Web Modeler  
  * views
    * Decision Requirements Diagram (DRD) view
      * view / Modeling starts
      * DMN elements
        * can be added -- via --
          * the palette | the left side / dragging and dropping them
          * context menu / appears if you select an element in the diagram
        * can be modified their properties -- via -- panel | right side

## Demo

![Demo](assets/desktop-modeler-dmn/demo.gif)

* how to model a decision table
  * if clicking the overlay | upper left corner of the decision -> you can edit it

## DMN coverage

* supported Modeler's DMN elements
  * Decision (tables and literal expressions)
  * Input data
  * Knowledge source
  * Business knowledge model

## Decision tables

![Decision Table](assets/desktop-modeler-dmn/decision-table.png)

* decision table view
  * if you click | blue icon on a decision table in the DRD -> it's open it
  * if you click the plus signs -> you can add elements
    * **Input**,
    * **Output**,
    * **Rule** 
  * tabulator and enter keys -- can be used to walk through the -- table cells
  * if you right click | cell -> you can about columns or rules
    * delete
    * copy
    * insert

![Delete or copy rules](assets/desktop-modeler-dmn/dmn-modeler-right-click.png)

  * if you double click | header row -> you can adjust the details of an
    * input or
    * output column 

![Change input or output column](assets/desktop-modeler-dmn/dmn-modeler-double-click.png)

  * jump between decision tables or literal expressions

![Jump between decision tables](assets/desktop-modeler-dmn/dmn-modeler-toggle-overview.png)

## Literal expressions

![New DMN Literal Expression](assets/desktop-modeler-dmn/literal-expression.png)

* allows
  * being edited
* click the blue icon to _drill-down_ | decision requirement diagram view 

## Business knowledge models

* TODO: 
A _business knowledge model_ (BKM) is a reusable function containing a piece of decision logic. Typically, a BKM instantiates business logic that is required in multiple decisions, such as a common computation. For example, an amortization formula might be used in different loan application processes.

You can make BKM elements executable using literal expressions written in FEEL, in almost the same way you would create a decision using a literal expression. A BKM literal expression can optionally accept parameters to be used as inputs to the FEEL expression, and it returns a single result whose name is the same as the BKM element name. Once you’ve created a BKM, it appears in autosuggestions when you’re using literal expressions to create decision logic.

Currently, you can only reuse BKMs within the same decision.

To create an executable BKM:

1. Add a BKM element to the canvas.
2. Name the BKM element. This name will be used for the result variable.
3. On the context menu, select **Change type > Literal expression**.
4. Click the blue literal expression icon (**{}**) on the BKM element.
5. Add parameters by hovering over the **()** and clicking the edit button. All changes to the BKM are saved automatically.
6. Enter a FEEL expression in the expression box.
7. Select a type for the result.
