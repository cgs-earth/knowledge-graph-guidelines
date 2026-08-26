# CGS Knowledge Graph and Ontology Architecture

## Purpose

This document defines the architecture for ontologies, mappings, and RDF instance graphs developed or integrated by CGS. Its goals are to:

- establish clear ownership and governance boundaries;
- keep ontology terms separate from dataset resources;
- promote reuse of established standards;
- isolate cross-ontology mappings from source ontologies;
- support project-specific extensions without destabilizing reusable models; and
- provide consistent namespace, dependency, publication, and versioning conventions.


<!-- <img width="3220" height="2900" alt="Ontology hierarchy (1)" src="https://github.com/user-attachments/assets/d62bbdb4-9cec-4049-b61a-b8b2040eba59" /> -->
<p align="center">
<img width="65%" alt="Ontology hierarchy (2)" src="https://github.com/user-attachments/assets/2d6594db-6bf8-4148-945d-2ad01ae55460" />
</p>

## Architectural principles
### Namespace authority follows governance

The organization that governs and publishes an ontology should control its namespace. If CGS constructs and maintains an ontology, the ontology should use a CGS-controlled namespace. When the ontology is constructed for a specific dataset, source organization provenance (e.g., EPA for SDWIS) must be recorded in the namespace. For more details on namespace generation, please refer to the namespace guidelines document.

### Reuse before extension

CGS should reuse established ontology terms when their semantics fit the intended meaning. CGS must not redefine or alter externally governed terms. When an external vocabulary is insufficient, CGS should create an extension term in a CGS-controlled namespace and relate it to the external term where appropriate.


### Meaning, mapping, and validation are separate concerns

- OWL and RDFS ontologies define shared meaning.
- Alignment ontologies state correspondences between independently governed models.
- Mapping specifications describe operational transformations from source data to RDF.
- SHACL shapes define data expectations for a particular application or exchange profile.
- Instance graphs contain assertions about dataset resources.

Keeping these concerns separate allows the same domain ontology to support multiple projects and validation profiles.


## 1. External standards and ontologies

External ontologies are established vocabularies governed outside CGS. Examples include:

- RDF, RDFS, OWL, and XML Schema datatypes
- SKOS for controlled vocabularies
- PROV-O for provenance
- DCAT and Dublin Core Terms for dataset metadata
- GeoSPARQL for geospatial features and geometries
- SOSA/SSN for observations, samples, sensors, and procedures
- Schema.org for metadata

CGS ontologies may reference and extend these ontologies as seen fit for the dataset/project. For example,

```turtle
@prefix dcat: <http://www.w3.org/ns/dcat#> .
@prefix geo:  <http://www.opengis.net/ont/geosparql#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<https://ontology.cgsearth.org/agency/epa/pwssab/WaterServiceAreaBoundary>
    rdfs:subClassOf geo:Feature .

<https://data.cgsearth.org/pwssab/dataset>
    a dcat:Dataset .
```

## 2. Domain ontologies

A domain ontology is a formal and structured framework that defines specific concepts, properties, and relationships within a particular field of interest, for example, surface hydrology, groundwater hydrology. Examples include:

- HY-Features
- GWML
- ??

## 3. CGS core ontologies

CGS core ontologies define stable concepts reused across datasets and projects. Examples include annotation, mapping, sintegration, and CGS-specific provenance concepts. A CGS core ontology should be independent of any single dataset or project. For example, 

   ``<https://ontology.cgsearth.org/annotation> 
   		a owl:Ontology ;
    	dct:title "Ontology that annotate classes and properties in CGS dataset ontologies with original dataset attributes"@en ;
    	dct:creator <https://cgsearth.org/> .
	# Annotation property preserving the source layer's exact column name.
	<https://ontology.cgsearth.org/annotation/sourceFieldName> a owl:AnnotationProperty ;
    	rdfs:label "source field name"@en ;
    	rdfs:comment "Exact column name used in the source layer metadata."@en . ``

## 4. CGS Dataset Ontologies
Ontologies that CGS creates for specific datasets. Since CGS creates it from the original dataset's metadata, use a cgs-controlled namespace
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


## 5. Project and application ontologies (including SHACL profiles)

A project ontology combines reusable domain and core terms for a particular use case. It may define:

- project-specific aggregations;
- analytical categories;
- joined or derived views over multiple datasets;
- cross-dataset mappings;
- derived indicators; and
- narrow application classes.

## 6. Instance Graphs
Instance graphs contain assertions about dataset records, physical or conceptual entities, observations, and derived resources. They should use a data namespace distinct from all ontology namespaces.
