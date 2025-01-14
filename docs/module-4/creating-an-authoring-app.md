---
title: Creating an authoring application
description: How to create a Studio application that writes to the EI Graph.
comments: true
hide:
     - toc
---

To write data to the Engineering Intelligence Graph (EI Graph) we need a user interface that accepts input from the user before writing it to the database. As we learned in the [previous lesson](understanding-graphql-mutations.md), _mutations_ allow us to edit, update, and create data in the Engineering Intelligence Graph (EI Graph).In this lesson we will use the example mutation from the last lesson to create a new software module. To create a new software module we need:

* An input accepting the new software module's `name`
* An input accepting a `description` of the new software module
* The `id` if the feature variant that the software module is atteched to

{{ snippets.demoInstanceDetails }}

## Creating the UI

Drag and drop three text input widgets and a submit button onto the Studio canvas of the appluications we created in the last module. Reminder: you can find widgets in the **UI** tab on the left-hand side.

<figure markdown="span">
     ![Creating the display app UI](src/creating-display-ui.png)
     <figcaption>Creating the display app UI</figcaption>
</figure>

Add labels for each text input. To add a label ...

## Creating the mutation

To create the mutation we will use from within Studio go to the **Queries** tab and select **New Query/API**. Select **EIN API** in the **Quick actions** section. Use the mutation we created in the last lesson:

<div class='grid' markdown>

!!! example "Query"

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
     
!!! example "Query variables"

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

<figure markdown="span">
     ![Run API on page load](src/api-page-load.png){ .img-medium }
     <figcaption>Run API on page load</figcaption>
</figure>

To get the values from the text input boxes we need to bind the output of the widgets to the Query variables.

## Binding the mutation

Switch back to the **UI** tab on the top-left and ...

## Publishing and sharing the application

When the application is complete, select the **Publish** button in the top-right corner to make it available from the SPREAD Platform launcher page. To share the application with other users select the **Share** button (next to the **Publish** button) and add users who can either have **Developer** rights to edit the application or **Viewer** rights to just view it.

<figure markdown="span">
     ![Sharing your application](src/share-application.png){ .img-medium }
     <figcaption>Sharing your application</figcaption>
</figure>

1. We recommend that you write this out to see all the options that are available to you to use as the value of the text widget. In this case we're just syncing to the table. -->
