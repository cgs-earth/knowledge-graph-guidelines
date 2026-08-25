# Architecture


<img width="6788" height="5620" alt="Ontology hierarchy" src="https://github.com/user-attachments/assets/2dee567f-a414-4e38-90c7-cebe25f2a0d2" />

1. External ontologies
Established standard vocabularies that CGS reused and extended as seen fit for the dataset/project.
Example:

``ex:WaterServiceAreaBoundary rdfs:subClassOf geo:Feature
ex:Dataset a dcat:Dataset .``

2. Domain Ontologies
Ontologies that CGS creates for specific datasets. Since CGS
creates it from the original dataset's metadata, use a cgs-controlled namespace
Example:
					``@prefix pwssab: <https://ontology.cgsearth.org/epa/pwssab/> .``

Then record the source and subject communicating where the dataset comes from, who constructed and governs the ontology.
``<https://ontology.cgsearth.org/epa/pwssab>
    a owl:Ontology ;
    dct:title "EPA Public Water System Service Area Boundary Ontology"@en ;
    dct:creator <https://cgsearth.org/> ;
    dct:source <https://github.com/USEPA/ORD_SAB_Model/tree/main/Metadata> ;
    dct:created "2026-08-24"^^xsd:date ;
    rdfs:seeAlso <https://github.com/USEPA/ORD_SAB_Model> .``

4. CGS Core Ontologies
   This layer contains stable, reusable concepts owned by CGS. For example,

   ``@prefix cgsm: <https://ontology.cgsearth.org/mapping/> .
@prefix cgsa: <https://ontology.cgsearth.org/annotation/> .``

5. Project and Application specific ontologies + SHACL profiles
   A project ontology combines only the terms and mappings needed for a particular use case. Project ontologies can define:
Project-specific aggregations
Analytical categories
Joined views over multiple datasets
Project-specific relationships
Derived indicators
Narrow application classes

6. Instance Graphs
Dataset records should normally use a separate data namespace: Keep ontology and data IRIs distinct:
