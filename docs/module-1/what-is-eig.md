---
title: What is the Engineering Intelligence Graph?
description: A course module explaining what the SPREAD Engineering Intelligence Graph is.
comments: true
hide:
     - toc
---

The central feature of SPREAD is the Engineering Intelligence Graph (EI Graph), which is also referred to as the Engineering Intelligence Network. The EI Graph is a GrapQL-based database where structured product data is stored. Graph databases are different from relational databases, such as MySQL, in that they use graph structures with nodes, edges, and properties to represent and store data. Relationships between nodes are key and in this way SPREAD is able to contextualize the relationships between the interactions of complex products.

## Product data cycle

<figure markdown="span" class="noborder">
	![The SPREAD product data cycle](src/product-data-cycle.png){ .skip-lightbox }
	<figcaption>The SPREAD product data cycle</figcaption>
</figure>

The cycle roughly consists of three parts:

* **Ingesting data**: As this stage we import product data into the EI Graph. Product data such as: CAD files, Bill of Material, electronics, wiring, diagnostic, signals data, DTCs, component IDs, configuration codes, 3D models, communication matrix and more.
* **Contextualizing data**: The data is integrated into the structured SPREAD information model, which enables data insights. For example, this allows you to match PR-Nr and BoM to provide VIN-specific troubleshooting recommendations.
* **Data insights**: From a base of structured knowledge we can create a multitude of applications for data visualization, predictive analytics, and automated insights. These applications enable you to interpret complex product data and make informed decisions.

## Example scenario

An automotive company

<div class='grid cards' markdown>

* :material-list-status:{ .lg .middle } **Quiz**

    ---

</div>
