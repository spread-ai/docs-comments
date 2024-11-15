---
title: Querying SPREAD in Studio
description: How to query the EI Graph when creating Studio applications.
hide:
     - toc
---

To get data from the Engineering Intelligence Graph we need to query the GraphQL database. GraphQL is a graph-based database that allows us to fetch only the data we need, unlike with REST APIs. In this lesson we will learn how to make a query from within SPREAD Studio and use the results in a [table](#) widget.

## GraphQL queries

To fetch data from a GraphQL database we use _queries_ in the similar way we would use a `GET` request in a REST API. The key difference being that we can define the response from the GraphQL database and get only the data we want. A REST API request might return a JSON object that we need to parse afterwards to get to the information we need.

<div class='grid' markdown>

!!! example "Example GraphQL query"

     ``` graphql 
     query Battery($batteryId: ID!, $changesetId: ID) {
          battery(id: $batteryId, changesetId: $changesetId) {
               createdAt
          }
     }
     ```

!!! example "Example variables for GraphQL query"

     ``` graphql
     {
     "batteryId": null,
     "changesetId": null
     }
     ```
</div>

## Finding the data

## Binding data to widgets
