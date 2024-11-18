---
title: Understanding GraphQL mutations
description: Understanding how to make chjanges to a GraphQL schema.
---

In [Module 2](../module-2/querying-spread.md#finding-the-query) we covered finding data, but the reverse is also possible: we can write data to the Engineering Intelligence Graph. To write data to a GraphQL database we use _mutations_ in the similar way to a `PUT` or `PATCH` request in a REST API.

A GraphQL mutation contains the following:

<div class='grid' markdown>

!!! example "GraphQL mutation structure"

     ```json 
     query Battery($batteryId: ID!, $changesetId: ID) { // (1)
          battery(id: $batteryId, changesetId: $changesetId) { // (2)  
               createdAt // (3)
          }
     }
     ```

     1. The exclamation point in `ID!` tells us that this field is required for this query. The changeSetID is optional.
     2. The $ symbol is used to insert variables, such as the `batteryId` in this case.
     3. This query will return the value of the field `createdAt`.

!!! example "GraphQL mutation variables"

     ``` graphql
     {
          "batteryId": null,
          "changesetId": null
     }
     ```
</div>

## Finding the mutation

Like with [queries](../module-2/querying-spread.md) you can use the Schema Definition Language (SDL) reference to find the right mutation for your needs. For more on using the reference, see [Finding the query](../module-2/querying-spread.md#finding-the-query). To view the SDL reference select the **EIN** tile from the SPREAD Launcher.

---

{{ snippets.demoInstanceDetails }}

---

??? failure "Schema introspection failure"

     If you see a "Schema introspection failure" error when opening the EIN tile, go to the **Connection Settings** in the top-left and select **Include cookies** to resolve it.

     ![Schema introspection failure fix](../module-2/src/schema-introspection-fail.png)

For example, if you wanted to change the dimensions of a battery you may search the reference for something like `updateBattery.dimensions` and see what the search returns. Using search terms that describe the action (`update` or `create`), the object that that action is applied to (`battery`), and the field that you want to change (`dimensions`) helps to narrow down the list of possible mutations. Remember to select the **Mutations** (as highlighted) to get results for mutations.

<figure markdown="span">
     ![Searching for mutation to update the dimensions of a battery](src/search-update-battery.png)
     <figcaption>Searching for mutation to update the dimensions of a battery</figcaption>
</figure>

## Exploring the mutation

Like with queries, you can click through to the GraphQL Explorer to test the endpoint. Unlike queries, you need to add the new field values that you would like to update or create in the **Variables** window.

<figure markdown="span">
     ![Mutation values in the Variables window](src/add-mutation-values.png)
     <figcaption>Mutation values in the Variables window</figcaption>
</figure>
