---
title:  Creating data visulaizations
description: Creating data visualtions in the application that we created.
hide:
     - toc
---

One of the benefits of structured data is that it can be rearranged, changes, and presented in different ways. For many use cases a visual represnetation of product data can cut down the time it takes to analyze and understand your product. In the prevbious lesson we created a viewing application ti display `featureVariant` data in a table. In this lesson we will create a dashboard that graphicaly shows the relationship between feature variants and software modules.

---


Exercises

Create a Feature Assist Dashboard. 
The Dashboard should show the relation of a Feature Variant to their Software Modules and Software Containers

App Setu

    Edit the Application Name

    Use the Theme Configuration from the Documentation  

    Import the JSON file. Leave only the Widgets that you’re going to use (i.E. the Top-Bar)

    Create a new Datasource > Authenticated GraphQL API

    Name it “graphQL_Data”

    The URL is: http://feature-assist-esf:8080/graphql

    Click on Save

    Filter the Feature Variants

        Create a new GraphQL query name it “get_feature_variants" and past the following query  to it
        query GetAllFeatureVariants {
          getAllFeatureVariant {
            value: id
            label: name
          }
        }

        Choose the Select Widget and drag it to the application

        Name the Widget “FeatureVariantSelect”

        Bind the Source that you’ve created to the Source Data in the Widget 
        {{get_feature_variants.data.data.getAllFeatureVariant}}

        Change the Label and Value (Dropdown Menu from Data) to Label = label, Value =  value 

        Remove the Default selected Value

        Change the Label Text 

    Show a Feature Variant in a Graph and Sankey diagram

        Create a new GraphQL query name it “get_feature_variant” and past the following query to it
        (Note that you need to extract from the code the Variables and add it to the Query variables)
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

        # Insert the following to the Variables Section

        {
          "findBy": {
            "type": "FeatureVariant",
            "id": {{FeatureVariantSelect.selectedOptionValue}}
          }
        }

        On the Select “FeatureVariantSelect“ Widget go to onOptionChange and execute the get_feature_variant query

        Create a new JS query name it “Graph” and paste the following code to it
        This Code will have functions to filter and sort the correct Data from the selected Feature Variant to have the correct dependencies and relations
        export default {
        	colorConf: [  {    "concept": "ComponentVariant",    "color": "#80ccff"  },  {    "concept": "ConnectorVariant",    "color": "#485162"  },  {    "concept": "FeatureSet",    "color": "#485162"  },  {    "concept": "HardwareVariant",    "color": "#485162"  },  {    "concept": "InternalCircuit",    "color": "#485162"  },  {    "concept": "LogicalConnection",    "color": "#485162"  },  {    "concept": "PhysicalConnection",    "color": "#485162"  },  {    "concept": "PinVariant",    "color": "#485162"  },  {    "concept": "Release",    "color": "#485162"  },  {    "concept": "SoftwareContainer",    "color": "#485162"  },  {    "concept": "SoftwareModule",    "color": "#0099ff"  },  {    "concept": "VehicleBus",    "color": "#485162"  },  {    "concept": "Vehicle",    "color": "#485162"  },  {    "concept": "Module",    "color": "#485162"  },  {    "concept": "Component",    "color": "#485162"  },  {    "concept": "ComponentType",    "color": "#485162"  },  {    "concept": "Connector",    "color": "#485162"  },  {    "concept": "Pin",    "color": "#485162"  },  {    "concept": "DataPoint",    "color": "#485162"  },  {    "concept": "OutputDriver",    "color": "#485162"  },  {    "concept": "SupplyVoltage",    "color": "#485162"  },  {    "concept": "PinInput",    "color": "#485162"  },  {    "concept": "Sensor",    "color": "#485162"  },  {    "concept": "OutputErrorDetection",    "color": "#485162"  },  {    "concept": "CurrentLoad",    "color": "#485162"  },  {    "concept": "SignalType",    "color": "#485162"  },  {    "concept": "ContactType",    "color": "#485162"  },  {    "concept": "ContactSurface",    "color": "#485162"  },  {    "concept": "InternalCircuitType",    "color": "#485162"  },  {    "concept": "Color",    "color": "#485162"  },  {    "concept": "Cable",    "color": "#485162"  },  {    "concept": "Wire",    "color": "#485162"  },  {    "concept": "Change",    "color": "#485162"  },  {    "concept": "VehicleVariant",    "color": "#485162"  },  {    "concept": "EquipmentPackage",    "color": "#485162"  },  {    "concept": "SaCode",    "color": "#485162"  },  {    "concept": "DiagnosisInformation",    "color": "#485162"  },  {    "concept": "BusSignal",    "color": "#858282"  },  {    "concept": "FeatureTargetArea",    "color": "#485162"  },  {    "concept": "Feature",    "color": "#485162"  },  {    "concept": "FeatureVariant",    "color": "red"  },  {    "concept": "SoftwareConfiguration",    "color": "#485162"  },  {    "concept": "Part",    "color": "#485162"  },  {    "concept": "Employee",    "color": "#485162"  },  {    "concept": "CompanyDepartment",    "color": "#485162"  },  {    "concept": "Company",    "color": "#485162"  },  {    "concept": "Harness",    "color": "#485162"  },  {    "concept": "Model",    "color": "#485162"  },  {    "concept": "System",    "color": "#485162"  }],
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

        Add a new Container Widget

        Insert a new Tab Widget and drag it into the Container Widget 

        In the Container Widget add the following code to the Visible Section. It will show the Graph and Sankey Diagram only when a Feature Variant is selected. 
        {{FeatureVariantSelect.selectedOptionLabel !== "" ? true : false}}

        In the Tab Widget adjust the Tabs Name (to Graph & Sankey) and change the Default Tab to Graph

        Add a Graph Widget to the Graph Tab and bind the Source in the Graph Widget to the Edges and Nodes as follows
        /* Edges */
        {{Graph.getAllEdges(Graph.prepareConfigs(get_feature_variant.data.data.entity))}}

        /* Nodes */
        {{Graph.getAllNodes(Graph.prepareConfigs(get_feature_variant.data.data.entity))}}

        In the style configuration panel, use the following setting
        Node figure: Rounded rectangle
        Mode: Hierarchical
        Direction: Down
        Tip: Change the properties from the Layering and Sizes to adjust the graph even more 

        Add another JS Object, name it “Sankey” and add the following code to it 
        export default {
        	generateFullSankey(dataInput) {

          var nodes = new Map();
          var relations = new Set();

          // Extract data
          var featureVariant = dataInput.data.entity;
          if (featureVariant) {
            featureVariant.realizedIn.forEach(function (realizedItem) {
              var softwareContainer = realizedItem.softwareContainer;
              var softwareModule = realizedItem.softwareModule;

              if (softwareContainer) {
                var scId = softwareContainer.id;
                nodes.set(scId, { label: softwareContainer.name || scId, id: scId });
                relations.add({ from: featureVariant.id, to: scId });
              }

              if (softwareModule) {
                var smId = softwareModule.id;
                nodes.set(smId, { label: softwareModule.name || smId, id: smId });
                relations.add({ from: scId, to: smId });

                softwareModule.requires.forEach(function (busSignal) {
                  var bsId = busSignal.id;
                  nodes.set(bsId, { label: busSignal.shortName || bsId, id: bsId });
                  relations.add({ from: smId, to: bsId });

                  busSignal.transportedBy.forEach(function (vehicleBus) {
                    var vbId = vehicleBus.id;
                    nodes.set(vbId, { label: vehicleBus.shortName || vbId, id: vbId });
                    relations.add({ from: bsId, to: vbId });

                    vehicleBus.connectedTo.forEach(function (pin) {
                      var pinId = pin.id;
        							nodes.set(pinId, { label: pin.refCode || pinId, id: pinId });
                      relations.add({ from: vbId, to: pinId });
                    });
                  });
                });
              }
            });
          }

          // Generate JSON arrays
          var nodesArray = Array.from(nodes.values());
          var linksArray = Array.from(relations).map(r => ({ from: r.from, to: r.to, value: 1 }));

         
          var finalJson = {
            type: "sankey",
            dataSource: {
              chart: {
                "nodeLabelPosition": "right",
                "nodeSpacing": "15",
                "enableDrag": 1,
                //caption: featureVariant ? featureVariant.name : "",
                //subCaption: featureVariant ? featureVariant.originalId : "",
                legendPosition: "bottom",
                linkcolor: "blend",
                theme: "fusion",
                showLegend: 0,
              },
              nodes: nodesArray,
              links: linksArray,
            },
          };
          return finalJson;
        },
        	generateSankeyJson(dataInput) {
        		var softwareModules = new Map();
        		var busSignals = new Map();
        		var relations = new Set();

        		// Extract data
        		var entity = dataInput.data.entity;
            var realizedIn = entity.realizedIn;
        		
        		if (realizedIn) {
        			realizedIn.forEach(function (module) {
        				var softwareModule = module.softwareModule;

        				// If softwareModule is null or undefined, skip this item
        				if (!softwareModule) {
        					return;
        				}

        				var softwareModuleId = softwareModule.id;
        				var softwareModuleName = softwareModule.name;

        				if (!softwareModules.has(softwareModuleId)) {
        					softwareModules.set(softwareModuleId, softwareModuleName);
        				}

        				var requires = softwareModule.requires;
        				if (requires) {
        					requires.forEach(function (busSignal) {
        						var busSignalId = busSignal.id;
        						var busSignalName = busSignal.shortName;

        						if (!busSignals.has(busSignalId)) {
        							busSignals.set(busSignalId, busSignalName);
        						}

        						// Create relation
        						var relationString = softwareModuleId + "," + busSignalId;
        						if (!relations.has(relationString)) {
        							relations.add(relationString);
        						}
        					});
        				}
        			});
        		}

        		// Generate JSON arrays
        		var nodesArray = [];
        		var linksArray = [];

        		softwareModules.forEach(function (value, key) {
        			nodesArray.push({ label: value, id: key });
        		});

        		busSignals.forEach(function (value, key) {
        			nodesArray.push({ label: value, id: key });
        		});

        		relations.forEach(function (relation) {
        			var ids = relation.split(",");
        			var fromId = ids[0];
        			var toId = ids[1];
        			linksArray.push({ from: fromId, to: toId, value: 1 });
        		});
        		
        	

        		var finalJson = {
        			type: "sankey",
        			dataSource: {
        				chart: {
        					"nodeLabelPosition": "right",
        					"nodeSpacing": "15",
        					"enableDrag": 1,
        					//caption: entity ? entity.name : "", // Loaded from the input data
        					//subCaption: entity ? entity.description : "", // Loaded from the input data
        					legendPosition: "bottom",
        					linkcolor: "blend",
        					theme: "fusion",
        					showLegend: 0,
        				},
        				nodes: nodesArray,
        				links: linksArray,
        			},
        		};

        		return finalJson;
        	},
        	generateSankeyVariant(dataInput) {

              var softwareContainers = new Map();
              var softwareModules = new Map();
              var componentVariants = new Map();
              var relations = new Set();
          
              var entity = dataInput.data.entity;
              var realizedIn = entity ? entity.realizedIn : [];
          
              if (realizedIn) {
                realizedIn.forEach(function (configuration) {
                  var softwareContainer = configuration.softwareContainer;
                  var softwareModule = configuration.softwareModule;
                  var componentVariant = configuration.componentVariant;
          
                  if (softwareContainer && softwareContainer.id && softwareContainer.name) {
                    softwareContainers.set(softwareContainer.id, softwareContainer.name);
                  }
          
                  if (softwareModule && softwareModule.id && softwareModule.name) {
                    softwareModules.set(softwareModule.id, softwareModule.name);
                  }
          
                  if (componentVariant && componentVariant.id && componentVariant.name) {
                    componentVariants.set(componentVariant.id, componentVariant.name);
                  }
          
                  if (softwareModule && softwareContainer) {
                    relations.add(softwareModule.id + "," + softwareContainer.id);
                  }
          
                  if (softwareContainer && componentVariant) {
                    relations.add(softwareContainer.id + "," + componentVariant.id);
                  }
                });
              }
          
              var nodesArray = [];
              var linksArray = [];
          
              softwareModules.forEach(function (value, key) {
                nodesArray.push({ label: value, id: key });
              });
          
              softwareContainers.forEach(function (value, key) {
                nodesArray.push({ label: value, id: key });
              });
          
              componentVariants.forEach(function (value, key) {
                nodesArray.push({ label: value, id: key });
              });
          
              relations.forEach(function (relation) {
                var ids = relation.split(",");
                var fromId = ids[0];
                var toId = ids[1];
                linksArray.push({ from: fromId, to: toId, value: 1 });
              });
          
              var finalJson = {
                type: "sankey",
                dataSource: {
                  chart: {
                    //caption: entity ? entity.name : "",
                    //subCaption: entity ? entity.description : "",
                    legendPosition: "bottom",
                    linkcolor: "blend",
                    theme: "fusion",
                    showLegend: 0,
                  },
                  nodes: nodesArray,
                  links: linksArray,
                },
              };
          
              
                  return JSON.stringify(finalJson, null, 2);
                }
        }

        Add a Chart Widget to the Sankey Tab and set the Chart type to “Custom chart”

        In the Custom fusion chart add the following code that will sort the Feature Variants to the Sankey Diagram with the correct dependencies and relations.
        {{Sankey.generateSankeyVariant(get_feature_variant.data)}}

        Adjust styling to the widgets

    Get Feature Variant Title / Description 

        Getting the Title: Add a new Text Widget and add the following Binding
        {{get_feature_variant.data.data.entity.name}}

        Adjust the Styling 

        Getting the Description: Add a new Text Widget and add the following Binding
        {{get_feature_variant.data.data.entity.description}}

        Adjust the Styling 

     Finalize your Application

        Go over the user journey and make sure that everything works

        Check your UI/UX in the Application


Resources 

 









---

<?quiz?>
question: Are you ready?
answer-correct: Yes!
answer: No!
answer: Maybe!
content:
<h2>Provide some additional content</h2>
<?/quiz?>