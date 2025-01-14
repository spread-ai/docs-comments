---
title: Understanding GraphQL mutationshe feature 
description: Understanding how to make chjanges to a GraphQL schema.
comments: true
hide:
     - toc
---

In [Module 2](../module-2/querying-spread.md#finding-the-query) we covered finding data, but the reverse is also possible: we can write data to the Engineering Intelligence Graph (EI Graph). To write data to a GraphQL database we use _mutations_ in the similar way to a `PUT`, `DELETE`, or `PATCH` request in a REST API.

<figure markdown="span">
     ![Mutations write to the EI Graph](src/mutation-dataset-diagram.png)
     <figcaption>Mutations write to the EI Graph</figcaption>
</figure>

As a reminder: Changesets are the versions of a dataset. Over time the data contained in a dataset may change and each iteration of the dataset is know as a changeset. In the diagram there are four changesets: Changeset A1 and Changeset A2 for Dataset A, and Changeset B1 and Changeset B2 for Dataset B.

!!! info "Publishing changes"

     With mutations changes that aren't published only apply to changesets, changes that are published apply to datasets as a whole.

Published changes can be fetched with queries to the dataset, but unpublished changes need a query that reads changesets to fetch. In a more advanced course, we will cover the difference - but in this course we will only apply changes to changesets.

For example, a GraphQL mutation for creating a software module with the name `LIDAR` looks like the following:

<div class='grid' markdown>

!!! example "GraphQL mutation structure"

     This muatation uses `$datasetID` as the `$datasetID` and and data of the feature variant to create is provided by `$data` variable.
     ---

     ```json
     mutation CreateSoftwareModule($name: String, $desc: String) {
          createSoftwareModule(datasetId: "EsfDatasets/de892a79-efab-4176-a282-e2c117cd1e23", data: {
               name: {
                    en: $name
               }
               description: {
                    en: $desc
               }
          }) {
               id
          }
     }
     ```
     
!!! example "GraphQL variables"

     The values for the fields to create are provided in the **Variables** window in EIN Explorer.
     ---

     ```json
     {
          "data": [
               {
                    "name": {
                         "en": "LIDAR"
                    }
               },
               {
                    "desc": "Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. "
               }, 
               {
                    "id": "FeatureVariants/08992c5e-522c-44a0-965f-72f83622c496"
               }
          ]
     }
     ```
</div>

!!! info "What is a Software Module?"

     A software module contains the software for completing a certain task, such as receiving inouts from sensors and determing that a car crah has occured. Another software module would initiate actions to deploy the airbag when that happens.

[Open the demo GraphQL mutation](https://app.spread.ai/ein?explorerURLState=N4IgJg9gxgrgtgUwHYBcQC4QAI4xQQxQEsIksBhAJwUIQGUIAzFAd32oFkIwYAbBABQASJPkTosdFJSJIA5gBosQsAgDOUCVJnyAlFmAAdMllNmzUarQbM2nbn0FhC%2BNQhQBJMBMMgAomqMACIubihqAPSqABwAnABM%2BADssQC0CIz4AEapACwAjEkAbKn48dHx6fFQ%2BYVQYPkI8QDMvkrOBBJGJua95qLiBsZ9IyPIEiJiCMOjfQC%2BM7PmqhoyAA7EpF2LS2NIEytQO7sLPSNz%2Bt275kRgx72nDyAKIABu7ETZ-GoY2ENnfV8HXwvgkAG17rMrtcRr4BtMMP8YddfMhQVhfAAZDxBACCACVfJCYY9kXMFMSRtDkeYgeojojfHQEGAsHgsGsEJQ1GsiFBPsQ1GykKosBA4EgiEKpSgEFhRCgYEKuZQIJQsGoiCgsK8ILwYBtaHAsPgoLA1PhUER4FhILw1Qg4ABHGBy3j4GDOK3wJQoCAEY3UY34TkyMRKGguuVENYWrAu-By7JYIi8e0ppCvZB%2B6g6rlawhSrDueMwVxEE2UKAACy1CCgfqwWRoBDlrwLcrAfIIGpgqGLAA81rw%2BdkIAA6LAAOUdEGLkuNMYtxt1%2BsNsuNLs%2BOr1BoIQs12tcoYVMHVHu13C1JvZjBgci1SjcrK3%2BCwUFIbhdfcV6rg%2BDkSVbT1B1lQgIUtywShC1INtd3XR0NQQSCkHpa1UEnIkASWckMWwqFKV2XxbnRXwADEWzPBAADUPktcIIgABjiBIoAAVgQVI2Piao8lyfBGNSWIijYxhUiSeJGGiZoih4qBcmErCaVJUYAF1jjmEA5iAA){ .md-button .md-button--primary }
<br>
<br>

## Finding the mutation

Like with [queries](../module-2/querying-spread.md) you can use the Schema Definition Language (SDL) reference to find the right mutation for your needs. For more on using the reference, see [Finding the query](../module-2/querying-spread.md#finding-the-query). To view the SDL reference select the **EIN** tile from the SPREAD Launcher.

{{ snippets.demoInstanceDetails }}

??? failure "Schema introspection failure"

     If you see a "Schema introspection failure" error when opening the EIN tile, go to the **Connection Settings** in the top-left and select **Include cookies** to resolve it.

     ![Schema introspection failure fix](../module-2/src/schema-introspection-fail.png)

If you wanted to create a new software module you may search the reference for something like `createSoftwareModule.name` and see what the search returns. Using search terms that describe the action (`update`, `delete`, or `create`), the object that that action is applied to (`softwareModule`), and the field that you want to create (`name`) helps to narrow down the list of possible mutations. Remember to select the **Mutations** tabs (as highlighted in the red box) to get results for mutations.

<figure markdown="span">
     ![Searching for mutation to create a new software module](src/search-create-featurevariants.png){ .img-medium }
     <figcaption>Searching for mutation to create a new software module</figcaption>
</figure>

## Exploring the mutation

Like with queries, you can click through to the GraphQL Explorer to test the endpoint. For usability, we recommend that you add the new field values that you would like to update or create in the **Variables** window.

<figure markdown="span">
     ![Mutation values in the Variables window](src/add-mutation-values.png)
     <figcaption>Mutation values in the Variables window</figcaption>
</figure>

Remember that any fields that have an exclamation point in the SDL reference are required fields, so you need to supply a value for them when performing a mutation. In this case the ID field is required to create a new software module.

!!! abstract "Task 1: Check that the software module has been created"

     Check that the software module has been created by making a query to find all software modules.

<?quiz?>
question: What is the command to make changes to a GraphQL database?
answer: put
answer: patch
answer-correct: mutation
answer: edit
answer: change
content:
<p></p>
<?/quiz?>

<blockquote class="next-lesson">In the <a href="creating-an-authoring-app.html">next lesson</a> we will write data back to the Engineering Intelligence Graph from our application.</blockquote>
