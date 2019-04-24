# Dimensionally Safe Computations with Measurements

## About this Tutorial <a id="about-this-tutorial"></a>

The Maana Physical Quantity service provides extensive capabilities for extracting physical quantities, or measured quantities, from text, and performing arithmetic, unit conversions and comparisons with them. This service uses a proprietary symbolic computing engine built on top of Stanford CoreNLP's named entity recognition library \([https://nlp.stanford.edu/software/](https://nlp.stanford.edu/software/)\).

The service provides a graphQL interface which can be used in conjunction with functional composition to rapidly deploy scientific and engineering solutions. The system ensures that all computations are consistent and comes pre-installed with familiar metric, Imperial and oil and gas units of measure.

## How to Use Physical Quantities With Functional Composition <a id="how-to-use-physical-quantities-with-functional-composition"></a>

In this example, you will create a new function that uses the physical quantity service to parse physical quantities from strings, and perform a consistent computation with them.

### The Problem <a id="the-problem"></a>

You would like to know the gauge pressure at the bottom of a well, and are given strings containing the atmospheric pressure, the depth of the well, the mud weight and the acceleration due to gravity. The computation that you would like to perform is described by the following formula:

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LWSKjuJIsK0lFXCaEtL%2F-LX6Nttp7x0SWcLjSZ5u%2F-LX6OIMOZTCY9CjHuWvO%2Fimage.png?alt=media&token=280a3cf5-fb71-4363-a71e-68e3874bab4d)

![Equation 1: Hydrostatic Pressure Computation](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LWSKjuJIsK0lFXCaEtL%2F-LX6Nttp7x0SWcLjSZ5u%2F-LX6OXAucUT21WF5VeyT%2Fimage.png?alt=media&token=cc834262-37d9-4320-9107-6c21493094c2)

For dimensional consistency, the gauge pressure, the atmospheric pressure and the hydrostatic head \(ρgh\) all have to have a physical dimension of FORCE/AREA. Furthermore, for unit consistency they all must have the same unit of measure. For this example, we will assume that you want the final pressure to be in the same unit of measure as the atmospheric pressure that is provided.

### The Solution <a id="the-solution"></a>

1. Create a new workspace and ensure that the Physical Quantity service is registered and appears in the "Inventory" panel:

![Figure 1: Ensure that the Physical Quantity service is in the Inventory](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LWSKjuJIsK0lFXCaEtL%2F-LX6Nttp7x0SWcLjSZ5u%2F-LX6OamrGJbLq2SZjB7i%2Fimage.png?alt=media&token=77e1e90c-7df9-47c3-9001-c94509ebfa4a)

2. If the physical quantity service is not in the inventory of your workspace, perform a search for "Physical Quantity" and drag the service from the search results onto the inventory.

3. Create a new function by clicking on the add function button \(the green "Σ"\) on the workspace toolbar.

4. Name it "hydrostaticPressure" and configure it with four mandatory STRING! inputs: atmosphericPressure, depth, mudWeigth and gravitationalAcceleration.

5. Change the output type to "Maana Physical Quantity:PhysicalQuantity".

When you are done, it should look like the Figure 2.

![Figure 2: Create a new Function on the Canvas](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LWSKjuJIsK0lFXCaEtL%2F-LX6Nttp7x0SWcLjSZ5u%2F-LX6OgpVsBiS0e7A-XH9%2Fimage.png?alt=media&token=2baf22c9-3a3d-4cc4-8a64-e26aa144537b)

6. Save the function and then open up its function graph.

7. Before you can perform the arithmetic computations with the physical quantities, you must deserialize them from the strings that you are given. The deserialization is performed by the physical quantity service's "parse" function. Find the parse function in the inventory, and drag four copies of it onto the canvas.

8. Connect each of the function's STRING! valued inputs to the "source" argument of a different parse function.

When you are done, your query graph should look like figure 3.

![Figure 3: Parse the Physical Quantities from the Provided Strings.](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LWSKjuJIsK0lFXCaEtL%2F-LX6Nttp7x0SWcLjSZ5u%2F-LX6OlYOcpYOLpjC3Whp%2Fimage.png?alt=media&token=ca5c5e69-1996-475e-862e-f1136e7308ac)

{% hint style="info" %}
Note that the parse function has optional parameters that allow you to restrict which system of units and physical dimensions are used when parsing. You will demonstrate the use of these optional parameters in a future tutorial.
{% endhint %}

9. Next drag a copy of the "negate" and "add" functions onto the canvas.

10. Connect the parsed atmospheric pressure to the input of the negate function, and then connect the output of that to the input of the add function.

11. Connect the output of the add function to the Output of the function.

Since the "add" function will have the same unit of measure as its first argument, this ensure that the output will be in the desired unit of measure.

When you are done, the function graph should look like figure 4:

![Figure 4: Negate the Atmospheric Pressure.](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LWSKjuJIsK0lFXCaEtL%2F-LX6Nttp7x0SWcLjSZ5u%2F-LX6Oq5_J4H1Me17uEOs%2Fimage.png?alt=media&token=2bec0793-e5fe-4fbc-beac-ac5de95c8f5e)

12. To complete the function, you need to multiply the depth, mudWeight and gravitationalAcceleration together, and add this to the negated atmospheric pressure. Multiplication is performed by the physical quantity's "mul" function. Drag two copies onto the canvas and connect them as depicted in figure 4.

![Figure 4: Negate the Atmospheric Pressure.](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LWSKjuJIsK0lFXCaEtL%2F-LX6Nttp7x0SWcLjSZ5u%2F-LX6OuLaKyJWpZY33KZC%2Fimage.png?alt=media&token=4c8c438e-29aa-45f4-a134-2cc54a142cd3)

### Using the Function <a id="using-the-function"></a>

1. Close the function graph by selecting the Knowledge Graph of your workspace.

2. Click on the hydrostaticPressure function and then select the "Run" tab on the context panel. You will be prompted to enter in values for the atmospheric pressure, depth, mud density and gravitational acceleration.

3. Fill in the values below and then press the run button:

![Figure 5: Entering Parameters for the Hydrostatic Pressure Function.](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LWSKjuJIsK0lFXCaEtL%2F-LX6Nttp7x0SWcLjSZ5u%2F-LX6OzGmS7CVaRKcyYKy%2Fimage.png?alt=media&token=9145e919-793c-4fb2-a48f-cb2beb9fdcdb)

4. After a short period of time, the results from the computation will be displayed in the context panel.

![Figure 5: Hydrostatic pressure results](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LWSKjuJIsK0lFXCaEtL%2F-LX6Nttp7x0SWcLjSZ5u%2F-LX6P4CVTOsA2rm4W0e9%2Fimage.png?alt=media&token=a35af820-320e-4fe9-8e0a-acc4ef1905b4)

