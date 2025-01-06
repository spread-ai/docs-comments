---
title: What is SPREAD?
description: A course module explaining what SPREAD is and how it can help you manage and visualize product data.
comments: true
hide:
     - toc
---

SPREAD is a platform that provides a suite of tools for data analysis, visualization, and collaboration. The platform you work with product data more efficiently and effectively.

The key features of SPREAD include:

* **Data import and integration:** You can import data from various sources, including spreadsheets, databases, and cloud storage services.
* **Data visualization:** SPREAD provides visualization tools, including charts, tables, and maps.
* **Collaboration:** You can share data and visualizations with others in real-time, making it easier to work together on projects.
* **Data analysis:** SPREAD provides a range of analysis tools, including filtering, sorting, and grouping, to help you get insights from your data.

<figure markdown="span" class="noborder">
	![The SPREAD Studio, where you can create applications that visialize data](src/spread-studio-collaboration.png){ .skip-lightbox }
	<figcaption>The SPREAD Studio</figcaption>
</figure>

The types of data that can be imported into SPREAD include:

| Data type | Description | Data format |
| --- | --- | --- |
| 2D wiring harness | Technical documentation of wiring harness data: connections between electric components from terminal to terminal incl. module part numbers, connectors, terminals, wires and auxiliary information. Contains only 2D coordinates for harness supplier's layout board. | kbl, vec |
| 3D model | The 3D CAD model of a product, assembly or part. | jt, step, x3d, and more |
| 3D wiring harness | Technical documentation of wiring harness data: connections between electric components from terminal to terminal incl. module part numbers, connectors, terminals, wires and auxiliary information. Additionally contains 3D coordinates for connectors and b-splines and control points for 3D positioning of single wires. | kbl, vec |
| Bill of Material (BoM) | List with part numbers, quantities, descriptions, configuration codes (code rules) for a product and its parts/assemblies. Usually, there are different BoMs per department with different detail levels and structures. For example: engineering, manufacturing, or retail. | xls, xml |
| Bus Communication | The K-Matrix describes which protocol/bus (for example, CAN, or FlexRay) sends which message in which frame and what the single bits and bytes mean. | xml, arxml, xlsx |
| Component ID mapping | Mapping and translation of harness component identifiers, for example, Reference ID from wiring harness data to Diagnosis ID from test reports, diagnosis address from test reports to Component identifier from odx data, and so on. | xlsx or similar |
| Component specification | Component specifications, including matching of signals and error codes to pins. | xlsx, xml, csv or similar |
| Configuration code translation | Translation of configuration codes used in BoM and order data into natural language, for example: L0L = left-steering. | xlsx or similar |
| Connector housing pictures | 2D pictures of connector housing showing terminal positions within the connector housing (usually black-and-white pictures), mapped via connector housing part numbers. | svg |
| Diagnosis specification | Specification of diagnosis behavior for diagnosis-relevant components - mostly ECUs - including diagnostic trouble codes (DTCs), error messages, repair messages, error triggering conditions. | pdx, odx |
| DTC Mapping | Mapping of DTCs to either their start terminal or end component for error cause predictions. | xlsx or similar |
| ECUs | A decsription of the Electronic Control Units (ECUs). | arxml |
| Functions | Customer or Vehicle functions that descibe a behavior of a feature. | xml, csx, xlsx |
| Harness data documentation | Documentation for client-specific logic for wiring harness development and documentation, for example, for distinguishing component types by their Reference ID. | pdf |
| Issue tickets | Raised tickets for issues with electric components, functions and/or software modules. | |
| Regulations | | |
| Requirements | | |
| Signal communication | Description of electric communication between ECUs based on system and bus signals. | arxml |
| Technology data | 3D co-ordinates of electric connectors. | xml |
| Test reports | Test reports and protocols from diagnosis tests based on OBD diagnosis with ECU identifiers and reported DTCs (error codes). | xml, json |
| Vehicle order data | Vehicle order reports with configuration specification of a unique vehicle (VIN) based on configuration codes (code rules) from Bill of Material incl. additional information such as production number, production date, and so on. | xml, json |
| Wiring harness diagrams | Wiring harness diagrams from legacy systems for harness design and visualization. | png, pdf, tif, or similar |


In this course, we will learn how to ingest data, display data using SPREAD Studio, and also write data. To ask questions about the content, leave a comment in the section below. In both cases, you will need a GitHub account. To sign up for an account, go to [GitHub](https://github.com).

<?quiz?>
question: Are you ready?
answer-correct: Yes!
answer: No!
answer: Maybe!
content:
<p></p>
<?/quiz?>

!!! question "Q&A"

    To ask a question, leave a comment in the comments section of the relevant page. Before asking a question, we kindly ask that you search the comments to see if your questions is already answered.
