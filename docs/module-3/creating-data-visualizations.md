---
title:  Creating data visulaizations
description: Creating data visualtions in Studio.
hide:
     - toc
---

In the previous module we created a viewing application to display `featureVariant` data in a table. In this lesson we will create a dashboard that graphically shows the relationship between feature variants and software modules.

{{ snippets.demoInstanceDetails }}

To open Studio, select the **Studio** tile in the SPREAD Platform Launcher.

## Create the UI

Drag and drop the following widgets onto the Studio canvas:

- A [Text]({{ config.site_url }}platform-tools/using-studio/reference/widgets/text.html) widget for the title of the application.
- A [Select]({{ config.site_url }}platform-tools/using-studio/reference/widgets/select.html) widget to select the feature variant.
- A [Container]({{ config.site_url }}platform-tools/using-studio/reference/widgets/container.html) widget to hold the data visualization widget.
- A [Graph]({{ config.site_url }}platform-tools/using-studio/reference/widgets/tab.html) widget onto the Container widget.

Remember that widgets can be found in the **UI** tab of the **Editor** view on the left-hand side.

<figure markdown="span">
	![Widgets for the data visualization application](src/widgets-data-viz-application.png){ .img-medium }
	<figcaption>Widgets for the data visualization application</figcaption>
</figure>

Now that we've set the UI foundation we can look at how to get data from the feature variant we select in the UI.

## Create the feature variants filter query

This GraphQL query accepts whatever is inputted into the Select widget as parameters to use to find the right feature variants to display.

Go to the **Queries** tab of the **Editor** view on the left-hand side and select **New query/API**. Under **Quick actions** select **EIN API**. In the middle **Query** window enter this GraphQL query.

```json
query GetAllFeatureVariants {
     getAllFeatureVariant {
          value: id
          label: name
     }
}
```

Name the query `get_feature_variants` at the top.

<figure markdown="span">
	![Creating a query to get feature variants](src/get-feature-variants-query.png){ .img-medium }
	<figcaption>Creating a query to get feature variants</figcaption>
</figure>

## Edit the Select widget settings

Go back to the Studio canvas by selecting the **UI** tab and select the **Select** widget. To pass data to the query and back we need to bind it to this widget. Rename the widget `FeatureVariantSelect` by double-clicking on it in the **UI** window or by using the three-dot menu.

<figure markdown="span">
	![Renaming the Select widget](src/rename-select-widget.png){ .img-medium }
	<figcaption>Renaming the Select widget</figcaption>
</figure>

Then change the following settings in the properties window on the right-hand side:

- **Source Data:** `{{ "{{get_feature_variants.data.data.getAllFeatureVariant}}" }}`
- **Label key:** `label`
- **Value key:** `value`

You may also change the **Default selected value** and the label text.

<figure markdown="span">
	![Select widget properties](src/select-widget-properties.png){ .img-medium }
	<figcaption>Select widget properties</figcaption>
</figure>

## Create the feature variant query

Once a feature variant has been identified, this query fetches data about it to populate the Graph widget.

Go to the **Queries** tab of the **Editor** view on the left-hand side and select **New query/API**. Under **Quick actions** select **EIN API**. In the middle **Query** window enter this GraphQL query.

```json
query getFeatureVariant($findBy: FetchEntityInput) {
  entity(findBy: $findBy) {
    ... on FeatureVariant {
      id
      name
      description
      realizedIn {
        id
				
        softwareModule {
          id
          name
		  description
        }
        softwareContainer {
          id
          name
		  description
        }
        componentVariant {
          id
          name
        }
      }
      realizedInComponentVariant {
        id
        name
      }
      originalId
			realizes {
        hasResponsible {
          firstName
          lastName
        }
      }
    }
  }
}
```

In the variable window, insert these variables that are provided to the query as parameters:

```json
{
  "findBy": {
    "type": "FeatureVariant",
    "id": {{ "{{FeatureVariantSelect.selectedOptionValue}}" }}
  }
}
```

Name the query `get_feature_variant` at the top.


## Parse the query output
 
The response returned by the GraphQL query needs to be parsed before it can be used by the Graph widget. This JavaScript code parses the data and returns the nodes and edges that the Graph widget uses to visualize the data.

Copy the code below, select the **JS** tab in the **Editor** view and paste it into the window.

??? "JavaScript code to parse query response"

     ```js 
     export default {
          colorConf: [{"concept": "ComponentVariant","color": "#80ccff"}, {"concept": "ConnectorVariant","color": "#485162"}, {"concept": "FeatureSet","color": "#485162"}, {"concept": "HardwareVariant","color": "#485162"}, {"concept": "InternalCircuit","color": "#485162"}, {"concept": "LogicalConnection","color": "#485162"}, {"concept": "PhysicalConnection","color": "#485162"}, {"concept": "PinVariant","color": "#485162"}, {"concept": "Release","color": "#485162"}, {"concept": "SoftwareContainer","color": "#485162"}, {"concept": "SoftwareModule","color": "#0099ff"}, {"concept": "VehicleBus","color": "#485162"}, {"concept": "Vehicle","color": "#485162"}, {"concept": "Module","color": "#485162"}, {"concept": "Component","color": "#485162"}, {"concept": "ComponentType","color": "#485162"}, {"concept": "Connector","color": "#485162"}, {"concept": "Pin","color": "#485162"}, {"concept": "DataPoint","color": "#485162"}, {"concept": "OutputDriver","color": "#485162"}, {"concept": "SupplyVoltage","color": "#485162"}, {"concept": "PinInput","color": "#485162"}, {"concept": "Sensor","color": "#485162"}, {"concept": "OutputErrorDetection","color": "#485162"}, {"concept": "CurrentLoad","color": "#485162"}, {"concept": "SignalType","color": "#485162"}, {"concept": "ContactType","color": "#485162"}, {"concept": "ContactSurface","color": "#485162"}, {"concept": "InternalCircuitType","color": "#485162"}, {"concept": "Color","color": "#485162"}, {"concept": "Cable","color": "#485162"}, {"concept": "Wire","color": "#485162"}, {"concept": "Change","color": "#485162"}, {"concept": "VehicleVariant","color": "#485162"}, {"concept": "EquipmentPackage","color": "#485162"}, {"concept": "SaCode","color": "#485162"}, {"concept": "DiagnosisInformation","color": "#485162"}, {"concept": "BusSignal","color": "#858282"}, {"concept": "FeatureTargetArea","color": "#485162"}, {"concept": "Feature","color": "#485162"}, {"concept": "FeatureVariant","color": "red"}, {"concept": "SoftwareConfiguration","color": "#485162"}, {"concept": "Part","color": "#485162"}, {"concept": "Employee","color": "#485162"}, {"concept": "CompanyDepartment","color": "#485162"}, {"concept": "Company","color": "#485162"}, {"concept": "Harness","color": "#485162"}, {"concept": "Model","color": "#485162"}, {"concept": "System","color": "#485162"  }],
          getAllNodes(obj) {
               const ids = [];

               function traverse(obj) {
                    if (obj.hasOwnProperty("id")) {
                         let shortName = obj.id;
                         if (obj.hasOwnProperty("name")) {
                              shortName = obj.name;
                         } else if (obj.hasOwnProperty("shortName")) {
                              shortName = obj.shortName;
                         }
                         let id_concept = obj.id.split("/")
                         let node = {id: obj.id, 
                                                       label: shortName}
                         if (id_concept.length > 1) {
                              node["color"] = Graph.colorConf.find(e => id_concept[0].startsWith(e.concept)).color
                         }
                         if (obj.hasOwnProperty("description")) {
                              node["description"] = obj.description
                         }
                         if (obj.hasOwnProperty("transportedBy")) {
                              node["transportedBy"] = obj.transportedBy
                         }

                         ids.push(node);
                    }

                    for (const key in obj) {
                         if (typeof obj[key] === "object" && obj[key] !== null) {
                              traverse(obj[key]);
                         }
                    }
               }

               traverse(obj);
               return Array.from(new Set(ids.map(obj => obj.id))).map(id => {
                    return ids.find(obj => obj.id === id);
               });
          },
          getAllEdges(obj) {
               const edges = [];
               let edgeId = 1;

               function traverse(obj, parent) {
                    if (obj.hasOwnProperty("id")) {
                         if (parent) {
                              edges.push({ id: edgeId++, from: parent.id, to: obj.id });
                         }
                         parent = obj;
                    }

                    for (const key in obj) {
                         if (typeof obj[key] === "object" && obj[key] !== null) {
                              traverse(obj[key], parent);
                         }
                    }
               }

               traverse(obj);
               return edges;
          },
          prepareConfigs(data) {
               let returnVariant = {}
               console.log(data)
               returnVariant ['id'] = data ['id']
               returnVariant ['name'] = data ['name']
               returnVariant ['description'] = data ['description']
               returnVariant ['originalId'] = data ['originalId']
               returnVariant ['realizedIn'] = data.realizedIn.reduce( function (acc, cur) {
                    if (!cur.componentVariant) {
                         cur.softwareModule ["includedIn"] = cur.softwareContainer
                         acc.push(cur.softwareModule)
                    } else if (!cur.softwareContainer) {
                         cur.softwareModule ["runsOn"] = cur.componentVariant
                         acc.push(cur.softwareModule)
                    }

                    return acc;
               }, []);

               let returnCompontents = data.realizedIn.reduce( function (acc, cur) {
                    if (cur.componentVariant && cur.softwareContainer) {
                         cur.softwareContainer ["runsOn"] = cur.componentVariant
                         acc.push(cur.softwareContainer)
                    }
                    return acc;
               }, []);

               return [returnVariant,returnCompontents]
          },
          singleEdges(data){
               let returnData = {}

               returnData ['id'] = data ['id']
               returnData ['name'] = data ['name']
               var list_of_modules = []
               returnData ['realizedIn'] = data.realizedIn.reduce( function (acc, cur) {

                    if (cur.softwareModule) {
                         if (-1 === list_of_modules.indexOf(cur.softwareModule.id)) {
                              list_of_modules.push(cur.softwareModule.id)
                              acc.push (cur.softwareModule)
                         }

                    }


                    return acc;
               }, []);

               return returnData
          }
     }
     ```

Name the JavaScript code `Graph` at the top.

### Apply bindings to the Graph widget

The parsed output should be bound to the Graph widget by using these values in the properties window on the right-hand side:

- **Edges:** `{{ "{{Graph.getAllEdges(Graph.prepareConfigs(get_feature_variant.data.data.entity))}}" }}`
- **Nodes:** `{{ "{{Graph.getAllNodes(Graph.prepareConfigs(get_feature_variant.data.data.entity))}}" }}`

<figure markdown="span">
	![Binding nodes and edges in the Graph widget](src/nodes-edges-graph-widget.png){ .img-medium }
	<figcaption>Binding nodes and edges in the Graph widget</figcaption>
</figure>

In the style configuration tab, use the following settings:

- **Node figure:** Rounded rectangle
- **Mode:** Hierarchical
- **Direction:** Down

## Publish the application

{{ snippets.publishApp }}
