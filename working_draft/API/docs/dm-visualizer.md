# Introduction
While the Data Model is primarly defined in the ontology in TTL format, there is a demand to have a visual version of the ONE Record Data Model. 

Our objective is to have an automated tool that allows to transcribe the ontology into a visual version.

# Data Model Visualizer
The tool is based on:
- The open-source DBML language as described here: https://dbml.dbdiagram.io/home/
- The open-source SQL Schema Visualizer available here: https://github.com/sqlhabit/sql_schema_visualizer

We host the tool on GitHub: https://aloccid-iata.github.io/ontology_visualizer/ (temporary repository)

The tool has been customized to fit our needs in terms of visual and features.

# Ontology to DBML
The first step is to put the ontology, or at least the part we want to disaply in DBML format.

*to be further documented as relevant*

# Data Mdodel Visualizer in details
## Main aspects

*to be further documented as relevant*  

## Additional features
Additional features have been added to enhance the user experience and facilitate the understanding of the data model.

### Navigation between objects
When looking at an object, you can click on the data type of a property if it's another object. The interface will directly zoom on that object to facilitate navigation among objects.

### Descriptions and comments
Descriptions of objects and properties are within the ontology, along with some comments when relevant. These can be also found in the visualizer by hovering over a property pressing shift.

![hover](https://github.com/lambertciata/ONE-Record/assets/58464775/3243253e-343c-4625-9ce1-c22e0dd6c6f3)

### Search
Search is possible within the visualizer. When text is entered, all objects and properties containing the text are displayed. When clicking on a result the relevant oject is displayed. Note that clicking on a property will display the object containing that property.

![search](https://github.com/lambertciata/ONE-Record/assets/58464775/b99dc784-7f33-47bb-a07d-5c051bbd5e45)
