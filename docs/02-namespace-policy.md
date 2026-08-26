# CGS Namespace Policy

## Purpose

This document defines how CGS assigns and manages IRIs for ontologies, controlled vocabularies, and instance resources. It is intended to provide stable identifiers, communicate ownership accurately, and keep ontology terms distinct from instance resources.

## 1. Namespace ownership

Namespace authority follows ontology governance. The organization that creates, maintains, and publishes an ontology should control its namespace.

The publisher of a source dataset does not automatically own an ontology derived from that dataset's metadata. When CGS constructs and governs an ontology from federal agency metadata, the ontology **MUST** use a CGS-controlled namespace unless the agency formally accepts responsibility for publishing and maintaining the ontology.

For example, an ontology developed by CGS for [EPA's public water system service are boundary dataset](https://www.epa.gov/ground-water-and-drinking-water/public-water-system-service-areas) should use:

```text
https://ontology.cgsearth.org/epa/pwssab/
```

## 2. General IRI requirements

CGS IRIs **MUST**:

- use HTTPS;
- use a domain controlled by CGS;
- remain stable after publication;
- avoid implementation-specific file extensions;
- avoid repository branch names such as `main`;
- avoid embedding the serialization format; and
- distinguish ontology terms from instance-data resources.

IRIs **SHOULD** use lowercase path segments. Class and property local names may use UpperCamelCase and lowerCamelCase respectively.

Examples:

```text
Class:
https://ontology.cgsearth.org/epa/pwssab/WaterServiceAreaBoundary

Property:
https://ontology.cgsearth.org/epa/pwssab/pwsIdentifier
```

## 3. Approved namespace patterns

| Resource category | Namespace pattern |
|---|---|
| CGS core ontology | `https://ontology.cgsearth.org/{name}/` |
| Agency-derived ontology | `https://ontology.cgsearth.org/agency/{agency}/{name}/` |
| Alignment ontology | `https://ontology.cgsearth.org/alignment/{source}-{target}/` |
| Project ontology | `https://ontology.cgsearth.org/project/{project}/` |
| Application profile | `https://profiles.cgsearth.org/{domain-or-project}/{profile}/` |
| Controlled vocabulary | `https://vocab.cgsearth.org/{scheme}/` |
| Dataset | `https://data.cgsearth.org/{dataset}` |
| Dataset resource | `https://data.cgsearth.org/{dataset}/resource/{identifier}` |


## 4. Ontology, namespace, and term IRIs

An ontology document has an ontology IRI, while its terms use the corresponding term namespace.

Recommended pattern:

```text
Ontology IRI:
https://ontology.cgsearth.org/agency/epa/pwssab

Term namespace:
https://ontology.cgsearth.org/agency/epa/pwssab/

Class IRI:
https://ontology.cgsearth.org/agency/epa/pwssab/WaterServiceAreaBoundary
```

Example declaration:

```turtle
@prefix pwssab:
    <https://ontology.cgsearth.org/agency/epa/pwssab/> .
@prefix owl: <http://www.w3.org/2002/07/owl#> .

<https://ontology.cgsearth.org/agency/epa/pwssab>
    a owl:Ontology .

pwssab:WaterServiceAreaBoundary
    a owl:Class .
```

## 5. Slash namespaces

CGS ontologies **SHOULD** use slash namespaces:

```text
https://ontology.cgsearth.org/agency/epa/pwssab/WaterServiceAreaBoundary
```

Slash namespaces support independent resolution and documentation of individual terms. A hash namespace may be approved for a small ontology that will always be published as a single document, but the selected style must remain consistent within that ontology.

The following styles must not be mixed within one ontology:

```text
https://ontology.cgsearth.org/example/ClassA
https://ontology.cgsearth.org/example#ClassB
```





## 9. Instance identifier construction

Instance IRIs should be deterministic and based on stable source identifiers where possible:

```text
https://data.cgsearth.org/pwssab/resource/AZ0410100
```

When a source identifier is not globally unique, the IRI **MUST** include sufficient context to prevent collisions. Identifier-generation rules must document:

- the source field or fields;
- normalization and escaping rules;
- case sensitivity;
- handling of missing identifiers; and
- treatment of changed or reassigned source identifiers.

Blank nodes should be reserved for resources that do not require persistent identity outside their containing graph.


## References

- [W3C Best Practice Recipes for Publishing RDF Vocabularies](https://www.w3.org/TR/swbp-vocab-pub/)
- [Cool URIs for the Semantic Web](https://www.w3.org/TR/cooluris/)
