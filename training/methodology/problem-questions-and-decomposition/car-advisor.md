# Car Advisor

This is a hands-on example that will teach principle of Top Down approach. In this case, learn how to create and application that will rank car makers based on reliability and brand image.

**Step by Step Instructions:**

**Step 1.** Create a new workspace. 

Search for following kinds and bring them onto your workspace:

* Vehicle
* ScoredVehicle
* BrandWords

Note: Vehicle and BranWords kinds are already preloaded with the data

* [ ] Explore content of Vehicle kind
* [ ] Explore content of BrandWords kind

**Step 2.** Create a top-level problem question

Say we have a list of carmakers and we want to know what are the top 5 best-ranked cars are. 

Our top level question will be **givenCarMakersWhatAreTheTopNBestRankedCars**

By phrasing it this way its is clear what the inputs and the outputs should be for this function. \(E.g. inputs are carMakers and topN and the output is RankedCars\)

Add following fields to **givenCarMakersWhatAreTheTopNBestRankedCars** function : 

1. **carMaker** and specify a value to be a list of type Vehicle, 
2. **topN** and specify the value to be required parameter and of type INT
3. Specify the output to be a list of type **ScoreVehicle**

Go inside of **givenCarMakersWhatAreTheTopNBestRankedCars** function

To know what are the topNbestRankedCars we need to know what is the score for each car maker. And then rank the desired amount of cars \( topN\) based on that score.

Step 3. Create function **scoreVehicle**:

* Input parameters: **vehicle** of type Vehicle. Required parameter
* Output: **ScoreVehicle**. Required parameter

Let's go inside of **scoreVehicle** function.  To calculate the score for each vehicle brand we will be using two scores: recall score and Brand Image score of that car maker from the news.

Let's create 2 functions to do exactly that:

1. Create function **getRecallScore**
   1. Input: **Vehicle**  of type vehicle kind. Required parameter
   2. Output: float. Required parameter
2. Create function **getBrandImageScore**

Now, let's go inside of **getRecallScore** function.

To calculate the Recall score we need a number of recalls and a number of sales.

Let's create functions for that:

1. Create function **getNumberOfRecalls**
   1. Input: **Vehicle** of type vehicle kind. Required parameter
   2. Output: INT. Required parameter
2. Create function **getVehicleSales**
   1. Input: **Vehicle** of type vehicle kind. Required parameter
   2. Output: INT. Required parameter

Once we know those two scores  we then need to normalize them by sales and by scale. 

Let's create those two functions as well.

1. Create function **normalizerecallScoreBySales**
   1. Input :
      1. **numberofRecalls**. Type: INT Required parameter
      2. **vehicleSales**. Type: INT Required parameter
   2. Output: Float. Required parameter
2. Create function **normalizeRecallScoreByScale**
   1. Input : **score**. Type: float. Required parameter
   2. Output: float. Required parameter

Step 4. Wire those functions up as:

* Input: Vehicle -&gt; **getNumberOfRecalls**: input
* Input: Vehicle -&gt; **getVehicleSales**: input
* **getNumberOfRecalls**: output -&gt; **normalizerecallScoreBySales**: input **numberofRecalls**
* **getVehicleSales**: output -&gt; **normalizerecallScoreBySales**: input **vehicleSales**
* **normalizerecallScoreBySales**: output -&gt; **normalizeRecallScoreByScale**: input **score**
* **normalizeRecallScoreByScale**: output -&gt; Output 

Now that the functions are wired, let's go inside of getNumberOfRecalls

Step 5. Bring in services.

We pre-wrote microservice that calculates a number of recalls, let's search for it. Find a service **getNumberOfRecall** and drag it into inventory. Drag it onto the workspace. Wire it with input and output. 

Let’s go one level up. \(Hint look for **getRecallScore** function in the left panel\)

1. Now let's go inside of **getVehicleSales** function.
2. Let's search for **getVehicleSales** service and bring it first to inventory and then onto the workspace.
3. Wire the input and output.
4. Let’s go one level up. To **getRecallScore** function

Go inside of **normalizerecallScoreBySales** function.

1. Let's search for **normalizeRecallScoreBySales** service and bring it first to inventory and then onto the workspace.
2. Wire the input and output. 
3. Let’s go one level up. To **getRecallScore** function

Go inside of **normalizeRecallScoreByScale** function.

1. Let's search for **normalizeRecallScoreByScale** service and bring it first to inventory and then onto the workspace.
2. Wire the input and output. 

At this point, we are solved all that is needed for getting **RecallScore**.

Let's go back to the **scoreVehicle** function.

Now we need to decompose **getBrandImageScore** function. Let's go inside this function. To get a brand image score we know that some sentiment analysis needs to be performed.

Let's create function: **EntityAnalysis**

* Input: **Vehicle** of type vehicle kind. Required parameter
* Output: Float. Required parameter

Lets wire input and output.

Let's go inside of **EntityAnalysis** function

For this function we would need to have several pieces of information: what is the maker, service that crawls through the news articles, brand words that were annotated as positive or negative.

Once we know the above we then can calculate positive and negative entity score and cumulative score for each brand.

First, let's extract brand names.

For that create function **getVehicleMake**

* Input: **Vehicle** of type vehicle kind. Required parameter
* Output: String, required parameter

Let's go inside of this function

1. Let's search for **getVehicleMake** service and bring it first to inventory and then onto workspace.
2. Wire the input and output. 
3. Let’s go one level up. To **EntityAnalysis** function

The next step is to crawl the news and extract key phrases from them for the brand names that we just extracted.

For that crate function **keyPhrasesFromNews**

* Input: **make** of type String. Required parameter
* Output: String, list, required parameter

Wire up the output of **getVehicle**&lt;Make and input of **keyPhrasesFromNews**

1. Let's go inside of **keyPhrasesFromNews** function.
2. Let's search for **allBrandWordss** and **randomKeyPhrases** services and bring them first to inventory and then onto the workspace.
3. Wire it up so:
   1. **allBrandWordss**: output -&gt;**randomKeyPhrases**: input-&gt;output
4. Let’s go one level up. To **EntityAnalysis** function

Now let's get **brandWords** 

Bring **allBrandWordss** service onto the workspace. 

Let's extract positive and negative words:

For that create function **getPositiveWords**

* Input: **allKeyWords** of type BrandWords kind, list, Required parameter
* Output: String, list, required parameter

1. Let's go inside of this function
2. Let's search for **getPositiveWords** service and bring it first to inventory and then onto the workspace.
3. Wire the input and output. 
4. Let’s go one level up. To **EntityAnalysis** function

Create function **getNegativeWords**

* Input: **allKeyWords** of type BrandWords kind, list, Required parameter
* Output: String, list, required parameter

1. Let's go inside of this function
2. Let's search for **getNegativeWords** service and bring it first to inventory and then onto the workspace.
3. Wire the input and output. 
4. Let’s go one level up. To **EntityAnalysis** function

Lets wire **allBrandWordss** output with inputs for **getPositiveWords** and **getNegativeWords**.

The next step is to calculate positive and negative entity scores. 

For that create function **calculatePositiveEntitiesScore**

* Input: **entities** of type string, list, Required parameter
* Output: String, list, required parameter

1. Let's go inside of this function. Let's search for **calculatePositiveEntitiesScore** service and bring it first to inventory and then onto the workspace.
2. Wire the input and output. 
3. Let’s go one level up. To **EntityAnalysis** function

Create function **calculateNegativeEntitiesScore**

* Input: **entities** of type string, list, Required parameter
* Output: String, list, required parameter

1. Let's go inside this function
2. Let's search for **calculateNegativeEntitiesScore** service and bring it first to inventory and then onto the workspace.
3. Wire the input and output. 
4. Let’s go one level up. To **EntityAnalysis** function

Now wire up output of **keyPhrasesFromNews** and input \(entities\) of **calculatePositiveEntitiesScore** and **calculateNegativeEntitiesScore**, as well as output of **getPositiveWords** and **getNegativeWords** with respective input parameters in **calculatePositiveEntitiesScore** and **calculateNegativeEntitiesScore**.

The last step in calculating the Brand image is to calculate the cumulative entity score. 

Lets create function **combinerEntityScore**.

* Input: 
  * **positiveEntityScore** of type float, Required parameter
  * **negativeEntityScore** of type float, Required parameter
* Output: float, list, required parameter

Wire up outputs of **calculatePositiveEntitiesScore** and **calculateNegativeEntitiesScore** with the inputs of **conbineEntityScore** function.

Let's go inside of this function

Let's search for **combineEntityScore** service and bring it first to inventory and then onto the workspace.

Wire the input and output. 

At this point, we are solved all that is needed for getting the BrandImage score.

Let's go back to **scoreVehicle** function.

Now that we have a recall score and brand image score calculated we need to calculate a compound score.

Create function **updateCompoundScore**

* Input: 
  * **vehicle** of type vehicle, Required parameter
  * **recallScore** of type float, Required parameter
  * **brandImageScore** of type float, Required parameter
* Output: of type **ScoredVehicle** kind, required parameter

Let's go inside of this function

Let's search for **updateCompoundScore** service and bring it first to inventory and then onto the workspace.

Wire the input and output. 

Let's go back to **scoreVehicle** function and wire input with inputs for getRecallScore and **getBrandImageScore**, and **updatedCompoundScore**; outputs of **getRecallScore** and **getBrandImageScore** with inputs for **updatedCompoundScore**. Output of **updateCompoundScore** with the output for **scoreVehicle** function.

The last step is to rank the cars by just calculated score.

For that lets go to **givenCarMakersWhatAreTheTopNBestRankedCars** function.

Create function **rankCarsByCompoundScores**

* Input: 
  * **scoredCars** of type ScoredVehicle, Required parameter
  * **nCars** of type int
* Output: of type **ScoredVehicle** kind, list, required parameter

1. Let's go inside this function
2. Let's search for **rankCarsByCompoundScore** service and bring it first to inventory and then onto the workspace.
3. Wire the input and output. 

lets go to **givenCarMakersWhatAreTheTopNBestRankedCars** function.

Wire inputs and outputs.

Let's go to the **Car Reliability** graph.

1. Click on **givenCarMakersWhatAreTheTopNBestRankedCars** function. 
2. Go to the right panel and click on the run button
3. Check the checkbox for **carMaker** and select instance \(i.e. Toyota\)
4. Check the checkbox for **topN** and enter 1
5. Click run
6. Observe the output of the function.

Voila you just solved the business problem. Now lets output score for all vehicles.

