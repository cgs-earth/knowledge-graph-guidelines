## 7. Local-name conventions

CGS ontology terms **SHOULD** follow these conventions:

| Term type | Convention | Example |
|---|---|---|
| Class | UpperCamelCase noun phrase | `WaterServiceAreaBoundary` |
| Object property | lowerCamelCase relational phrase | `hasWaterSource` |
| Datatype property | lowerCamelCase noun or relational phrase | `pwsIdentifier` |
| Named individual | UpperCamelCase or stable source code | `GroundWater` or `GW` |
| Concept scheme | lower-kebab-case path | `water-source` |

Local names **SHOULD NOT** contain spaces, punctuation, or source-system formatting such as `PWS_Name`. Original field names can be retained as metadata or mapping declarations without becoming canonical ontology term names.

## 8. Version IRIs

  Compatible releases **MUST NOT** change the namespace or existing term IRIs. Each release should use an immutable `owl:versionIRI`:

  ```text
  Ontology IRI:
  https://ontology.cgsearth.org/agency/epa/pwssab

  Version IRI:
  https://ontology.cgsearth.org/agency/epa/pwssab/version/1.0.0

  Stable term IRI:
  https://ontology.cgsearth.org/agency/epa/pwssab/WaterServiceAreaBoundary
  ```

  Example:

  ```turtle
  <https://ontology.cgsearth.org/agency/epa/pwssab>
      a owl:Ontology ;
      owl:versionInfo "1.0.0" ;
      owl:versionIRI
          <https://ontology.cgsearth.org/agency/epa/pwssab/version/1.0.0> .
  ```

  Version numbers must not be embedded in ordinary class, property, or instance IRIs.


  ## 6. Prefix policy

Every ontology **MUST** declare one preferred prefix. Prefixes should be short, recognizable, and unique within the CGS registry.

Examples:

| Ontology | Preferred prefix |
|---|---|
| PWSSAB | `pwssab` |
| CGS mapping ontology | `cgsm` |
| CGS annotation ontology | `cgsa` |
| PWSSAB–GeoConnex alignment | `pwssab-gcx` |

Prefixes are abbreviations used in RDF serializations and queries; they are not globally unique identifiers and must not replace full IRIs in governance records.


# References

- [OWL 2 Web Ontology Language Structural Specification](https://www.w3.org/TR/owl2-syntax/)
