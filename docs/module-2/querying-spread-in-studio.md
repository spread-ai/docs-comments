---
title: Querying SPREAD in Studio
description: How to query the EI Graph when creating Studio applications.
hide:
     - toc
---

To get data from the Engineering Intelligence Graph we need to query the GraphQL database. GraphQL is a graph-based database that allows us to fetch only the data we need, unlike with REST APIs. In this lesson we will learn how to make a query from within SPREAD Studio and use the results in a [table](#) widget.

## GraphQL queries

To fetch data from a GraphQL database we use _queries_ in the similar way we would use a `GET` request in a REST API. The key difference being that we can define the response from the GraphQL database and get only the data we want. A REST API request might return a JSON object that we need to parse afterwards to get to the information we need.

A GraphQL query contains 

<div class='grid' markdown>

!!! example "GraphQL query structure"

     ``` graphql 
     query Battery($batteryId: ID!, $changesetId: ID) { // (1) The exclamation point in `ID!` tells us that this field is required for this query. The changeSetID is optional.
          battery(id: $batteryId, changesetId: $changesetId) { // (2) The $ symbol is used to insert variables, such as the `batteryId` in this case. 
               createdAt // (3) This query will return the value of the field `createdAt`.
          }
     }
     ```

!!! example "GraphQL query variables"

     ``` graphql
     {
          "batteryId": null,
          "changesetId": null
     }
     ```
</div>

## Finding the data

## Binding data to widgets
