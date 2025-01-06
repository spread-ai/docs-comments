---
title: Creating an authoring application
description: How to create a Studio application that writes to the EI Graph.
hide:
     - toc
---

To write data to the Engineering Intelligence Graph (EI Graph) we need a user interface that accepts input from the user before writing it to the database. As we learned in the [previous lesson](understanding-graphql-mutations.md), _mutations_ allow us to edit, update, and create data in the Engineering Intelligence Graph (EI Graph).

{{ snippets.demoInstanceDetails }}

## Creating the UI

Drag and drop a text input widget onto the Studio canvas from the **UI** tab on the left-hand side. The highlighted options on the right-hand side are where we will get the data to use for the mutation query.

<figure markdown="span">
     ![Creating the display app UI](src/creating-display-ui.png)
     <figcaption>Creating the display app UI</figcaption>
</figure>

<!-- ## Creating the mutation

To create the query we will use from within Studio go to the **Queries** tab and select **New Query/API**.Select **EIN API** in the **Quick actions** section. Here you can see all the same objects that are in the Schema Definition Language (SDL) reference from the [previous lesson](querying-spread.md).

<figure markdown="span">
     ![Creating a query in the Studio interface](src/studio-ein-api.png)
     <figcaption>Creating a query in the Studio interface</figcaption>
</figure>

Select the `featureVariants` object in the **Explorer** window and select the `name`, `description`, and `createdAt` fields underneath. Then select the **Run** button to confirm that the query works as expected.

!!! info "Example dataset ID"

     For the demonstration we have set up a dataset with the ID: `"EsfDatasets/de892a79-efab-4176-a282-e2c117cd1e23"`. Use that as the `datasetId` in the query.

<figure markdown="span">
     ![Creating a query in the Studio interface](src/create-query-in-studio.png)
     <figcaption>Creating a query in the Studio interface</figcaption>
</figure>

The results will appear in the bottom window under the heading **Response** > **JSON**.

Switch to the **Settings** tab and set **Run API on page load**.

<figure markdown="span">
     ![Run API on page load](src/api-page-load.png){ .img-medium }
     <figcaption>Run API on page load</figcaption>
</figure>

## Binding the mutation

Switch back to the **UI** tab on the top-left and select the table widget that you dropped on to the canvas earlier. Select the **Table data** dropdown menu on the right-hand side and select the query you created.

<figure markdown="span">
     ![Binding the query to the table](src/binding-query-to-table.png)
     <figcaption>Binding the query to the table</figcaption>
</figure>

The fields returned by the query are mapped as columns and you can edit them in the section below **Table data**. For example, let's hide the **description** column from the table by selecting the **👁️** icon in the **Table** section. You can also edit each column by selecting the **⛭** icon.

<figure markdown="span">
     ![Editing columns in a table](src/column-settings.png){ .img-medium }
     <figcaption>Editing columns in a table</figcaption>
</figure>

## Publishing and sharing the application

When the application is complete, select the **Publish** button in the top-right corner to make it available from the SPREAD Platform launcher page. To share the application with other users select the **Share** button (next to the **Publish** button) and add users who can either have **Developer** rights to edit the application or **Viewer** rights to just view it.

<figure markdown="span">
     ![Sharing your application](src/share-application.png){ .img-medium }
     <figcaption>Sharing your application</figcaption>
</figure>

1. We recommend that you write this out to see all the options that are available to you to use as the value of the text widget. In this case we're just syncing to the table. -->
