---
title: Creating a display application
description: Taking our previous lessons' knowledge and creating a Studio applicationn that displays data.
hide:
     - toc
---

Now that we know how to fetch data from the Engineering Intelligence Graph we can create an application to display it. We're going to create an application that displays the dimensions of a battery within a table.

---

{{ snippets.demoInstanceDetails }}

---

## Creating the UI

Drag and drop a table widget onto the Studio canvas from the **UI** tab on the left-hand side. The highlighted options on the right-hand side is where we will add data from the query that we will bind to the table.

<figure markdown="span">
     ![Creating the display app UI](src/creating-display-ui.png)
     <figcaption>Creating the display app UI</figcaption>
</figure>

## Creating the query

To create the query we will use from within Studio go to the **Queries** tab and select **New Query/API**.Select **EIN API** in the **Quick actions** section. Here you can see all the same objects that are in the Schema Definition Language (SDL) reference from the [previous lesson](querying-spread.md).

<figure markdown="span">
     ![Creating a query in the Studio interface](src/studio-ein-api.png)
     <figcaption>Creating a query in the Studio interface</figcaption>
</figure>

Select the `battery` object in the **Explorer** window and select the `height`, `length`, and `width` fields. Add `{"id": xxxxxxxxx}` as the query variable (the ID is required for the query to work). Then select the **Run** button to confirm that the query works as expected.

<figure markdown="span">
     ![Creating a query in the Studio interface](src/studio-ein-api.png)
     <figcaption>Creating a query in the Studio interface</figcaption>
</figure>

Swith to the **Settings** tab and set **Run API on page load**.

<figure markdown="span">
     ![Run API on page load](src/api-page-load.png)
     <figcaption>Run API on page load</figcaption>
</figure>

## Binding the query

Switch back to the **UI** tab on the top-left and select the table widget that you dropped on to the canvas earlier. Select the **Table data** dropdown menu on the right-hand side and select the query you created.

<figure markdown="span">
     ![Binding the query to the table](src/binding-query-to-table.png)
     <figcaption>Binding the query to the table</figcaption>
</figure>

The fields returned by the query are default mapped as columns and you can edit them in the section below **Table data**. For example, let's hide the **length** column from the table by selecting the **👁️** icon in the **Table** section. You can also edit each column by selecting the **⛭** icon.

<figure markdown="span">
     ![Editing columns in a table](src/column-settings.png)
     <figcaption>Editing columns in a table</figcaption>
</figure>

## Syncing data across widgets

Data can also be synced between widgets. We have hidden the **length** column but we can display it in another connected widget. Drag and drop the [container](../) widget on to the Studio canvas. Then drag and drop a [text]() widget on top of the container.

<figure markdown="span">
     ![The container and text widgets below the table](src/container-with-text.png)
     <figcaption>The container and text widgets below the table</figcaption>
</figure>

Select the text widget and in the **Text** input field in the settings on the left-hand side enter: `{{ '{{Table1.selectedRow.length }}' }}` (1). This sets the value of the text field to the selected row in `Table1` and `length` column value of that row.
{ .annotate }

<figure markdown="span">
     ![Set the value of the text field](src/set-text-value.png)
     <figcaption>Set the value of the text field</figcaption>
</figure>

Similarly, you can set the value of fields in other widgets to sync with each other.

## Publishing and sharing the application

When the application is complete, select the **Publish** button in the top-right corner to make it available from the SPREAD Platform launcher page. To share the application with other users select the **Share** button (next to the **Publish** button) and add users who can either have **Developer** rights to edit the application or **Viewer** rights to just view it.

<figure markdown="span">
     ![Sharing your application](src/share-application.png)
     <figcaption>Sharing your application</figcaption>
</figure>

1. We recommend that you write this out to see all the options that are available to you to use as the value of the text widget. In this case we are just syncing to the table.