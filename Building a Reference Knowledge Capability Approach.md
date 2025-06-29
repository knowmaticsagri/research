# Building a Reference Knowledge Capability: An Approach to Curated Semantic Assertions for R&D Data Pipelines

## Abstract

This paper outlines an approach for developing a reference knowledge capability that bridges the gap between reference data (SKOS vocabularies) and reference models (OWL ontologies). The proposed system enables curation and delivery of domain-specific semantic assertions that support machine learning, regulatory compliance, analytics, and knowledge reuse across R&D organisations. We present modelling approaches, implementation considerations, and real-world applications for managing curated, trusted assertions about relationships between controlled vocabulary concepts.

## 1. Introduction

Modern R&D organisations face increasing challenges in managing and leveraging their knowledge assets across diverse applications - from machine learning model training to regulatory submissions. Whilst controlled vocabularies (SKOS) provide standardised terminologies and formal ontologies (OWL) offer logical frameworks, there exists a critical gap: the systematic capture and governance of domain-specific semantic facts that are neither purely taxonomic nor requiring full logical inference.

This paper introduces **Reference Knowledge** as a curated layer of semantic assertions that addresses this gap, enabling organisations to systematically capture, validate, and reuse domain expertise in machine-actionable form.

## 2. Defining Reference Knowledge

### 2.1 Conceptual Definition

Reference Knowledge refers to curated, trusted assertions about relationships between concepts in controlled vocabularies. These assertions are characterised by:

- **Expert validation**: Asserted and reviewed by domain experts
- **Semantic expressiveness**: Expressed using meaningful, domain-specific properties
- **Governed curation**: Subject to formal review and versioning processes  
- **Cross-application reusability**: Designed for use across analytics, ML/AI, and regulatory contexts

### 2.2 Distinguishing Characteristics

Reference Knowledge occupies a distinct position in the knowledge representation spectrum:

| Knowledge Type | Scope | Formality | Use Cases |
|----------------|-------|-----------|-----------|
| **Reference Data (SKOS)** | Terminological relationships | Low | Standardisation, search |
| **Reference Knowledge** | Domain semantic facts | Medium | ML training, analytics, regulation |
| **Reference Models (OWL)** | Logical constraints & inference | High | Automated reasoning, validation |

### 2.3 Working Definition

> **Reference Knowledge** is a curated layer of semantic assertions made between reference data concepts (SKOS), using domain-relevant relationships, to encode canonical business facts that are trusted, reusable, and semantically governed.

## 3. Value Proposition for R&D Organisations

### 3.1 Cross-Functional Benefits

The Reference Knowledge capability delivers value across multiple organisational functions:

**Machine Learning & Generative AI**
- Provides domain-grounded assertions for model training and prompt engineering
- Enables semantic grounding of AI-generated content
- Supports knowledge-augmented generation workflows

**Regulatory Compliance**
- Establishes traceable, curated fact bases for evidence submissions
- Enables consistent representation of domain knowledge across regulatory documents
- Supports audit trails for knowledge-based decisions

**Analytics & Data Science**
- Powers semantic joins across heterogeneous datasets
- Enables knowledge graph queries and graph-based analytics
- Supports entity resolution and data integration workflows

**Search & Interoperability**
- Enhances cross-dataset linking and entity matching
- Enables controlled query expansion using semantic relationships
- Improves discoverability of related concepts and datasets

*Example Competency Questions:*
- "Find all crops that are affected by fungal pathogens" (using `isPathogenOf` relationships)
- "What water bodies flow into the Thames River system?" (using `flowsInto` properties)
- "Which pharmaceutical compounds interact with aspirin?" (using `interactsWith` assertions)
- "What are all the parts of a turbine assembly across different datasets?" (using `hasPart` relationships)
- "Find treatments for conditions that are caused by bacterial infections" (combining `treatsCondition` and `causes` properties)
- "Which crops require similar soil types for cultivation?" (using `requiresSoilType` to find agricultural similarities)

### 3.2 Knowledge Reuse & Organisational Learning

Reference Knowledge serves as institutional memory, capturing domain expertise in reusable form for:
- New employee onboarding and training
- Cross-project knowledge transfer
- Systematic capture of expert knowledge before retirement
- Consistent application of domain knowledge across teams

## 4. Real-World Applications

### 4.1 Domain Examples

Several established vocabularies demonstrate the practical application of reference knowledge principles:

**Agricultural Sciences (AGROVOC/FAO)** (Caracciolo et al., 2013)
```turtle
agrovoc:c_4eecc350 agrontology:isDiseaseFor agrovoc:c_1612 .
# chickpea blight is disease for Cicer arietinum

agrovoc:c_4eecc350 agrontology:isCausedBy agrovoc:c_34509 .
# chickpea blight is caused by Ascochyta rabiei
```

**Chemical Biology (ChEBI/OBO)** (Degtyarenko et al., 2008)
```turtle
chebi:15377 chebi:hasRole chebi:24664 .
# Aspirin hasRole Analgesic

chebi:15377 chebi:isConjugateAcidOf chebi:30089 .
# Aspirin isConjugateAcidOf Aspirin anion
```

**Biomedical Sciences (UBERON/OBO)** (Mungall et al., 2012)
```turtle
uberon:UBERON_0002048 uberon:develops_from uberon:UBERON_0003082 .
# lung develops_from respiratory primordium

uberon:UBERON_0001264 uberon:adjacent_to uberon:UBERON_0001017 .
# frontal bone adjacent_to central nervous system

uberon:UBERON_0000948 bfo:BFO_0000050 uberon:UBERON_0001017 .
# heart part_of central nervous system
```

**Financial Services (FIBO)** (Enterprise Data Management Council, 2024)
```turtle
fibo-be-oac-opty:hasDirectOwnership fibo-fbc-fct-usfsind:BloombergFinanceOwnership .
# Bloomberg Finance L.P. hasDirectOwnership Bloomberg Finance Ownership

fibo-fbc-fct-ra:isRegisteredIn fibo-fbc-fct-usjrga:DelawareBusinessEntitiesRegistry .
# Bloomberg Finance L.P. isRegisteredIn Delaware Business Entities Registry
```

### 4.2 Implementation Patterns

These examples demonstrate common patterns in reference knowledge implementation:
- Use of public identifiers (LEI, DOI, ORCID) for entity resolution
- Domain-specific relationship vocabularies
- Integration with existing controlled vocabularies
- Support for provenance and validation metadata

## 5. Modelling Approaches

### 5.1 Technical Options Analysis

| Approach | Key Features | Strengths | Limitations | Best Fit |
|----------|--------------|-----------|-------------|----------|
| **RDF + SHACL** | Validation rules and constraints | Strong governance, QA support | No automated inference | Quality-focused curation |
| **Named Graphs** | Separate graphs with metadata | Excellent provenance tracking | Requires graph-aware tooling | Complex curation workflows |
| **Nanopublications** | Atomised assertions with full provenance | Research-grade provenance | Verbose, specialised tools | High-value, citable facts |
| **SKOS+** | Extended SKOS with domain properties | Lightweight, familiar | Informal constraints | Existing vocabulary workflows |

### 5.2 Recommended Implementation Approaches

Given the organisational context and existing capabilities, two approaches emerge as most viable:

**SKOS+ Pattern**
Simple extension of existing SKOS vocabularies with domain-specific object properties:
```turtle
# Basic assertion using SKOS+
agrovoc:Abelmoschus_esculentus agrovoc:produces agrovoc:fruit .
agrovoc:Botrytis_cinerea agrovoc:isPathogenOf agrovoc:Dahlia_pinnata .
```

**Nanopublication Pattern**  
Structured approach providing explicit provenance and trust metadata:
```turtle
# Nanopublication structure
:nanopub123456 a np:Nanopublication ;
  np:hasAssertion :assertion123456 ;
  np:hasProvenance :provenance123456 ;
  np:hasPublicationInfo :pubinfo123456 .

# The assertion (same as SKOS+)
:assertion123456 {
  agrovoc:Abelmoschus_esculentus agrovoc:produces agrovoc:fruit .
}

# Provenance (who, when, confidence)
:provenance123456 {
  :assertion123456 prov:wasAttributedTo <orcid:0000-0002-1825-0097> ;
    prov:generatedAtTime "2025-06-27T10:30:00Z"^^xsd:dateTime ;
    :reviewedBy <http://example.org/working-group/plant-biology> ;
    :confidence "high" .
}
```

**Why These Approaches Work:**
- Leverage existing reference data management capabilities and processes
- Avoid bottlenecks in specialised modelling teams
- Work within established domain expert workflows
- Provide appropriate levels of trust and governance

## 6. Implementation Strategy

### 6.1 Organisational Alignment

**Positioning Within Existing Capabilities**

The Reference Knowledge capability should be positioned as an extension of existing reference data management processes, not as a separate modelling initiative. This approach:

- **Builds on established processes**: Leverages existing SKOS curation workflows and domain working groups
- **Avoids modelling bottlenecks**: Enables domain experts to make assertions without requiring specialised ontology modelling skills
- **Maintains governance**: Uses proven reference data quality and review processes
- **Scales naturally**: Works within current organisational structures and tooling

**Key Principle**: Reference Knowledge represents expert assertions *about* the data (SKOS concepts), rather than formal modelling *of* the domain. This distinction is crucial for organisational acceptance and sustainable implementation.

### 6.2 Role of the Editorial Office

The Editorial Office serves as the coordination point between modelling teams and reference data curation teams, providing:

**Advisory Function**
- Guidance on when assertions require formal modelling input
- Consultation on complex semantic relationships
- Resolution of conflicts between modelling and curation perspectives

**Property Palette Development**
- Collaborative development of object property vocabularies
- Standardisation of relationship types across domains
- Maintenance of property definitions and usage guidelines

**Quality Assurance**
- Cross-team review of assertion patterns
- Consistency checking across domain working groups
- Integration testing with downstream applications

### 6.3 Implementation Approaches Analysis

| Aspect | SKOS+ Pattern | Nanopublication Pattern |
|--------|---------------|------------------------|
| **Complexity** | Low - extends existing workflows | Medium - structured but manageable |
| **Trust Level** | Medium - relies on SKOS governance | High - explicit provenance and confidence |
| **Tooling Requirements** | Minimal - existing SKOS tools | Moderate - may need tool extensions |
| **Expert Adoption** | High - familiar pattern | Medium - requires training |
| **Downstream Value** | Good for basic applications | Excellent for high-trust scenarios |

**Recommended Hybrid Approach**: Start with SKOS+ for rapid deployment, migrate high-value assertions to nanopublication pattern as tooling matures.

### 6.4 Tooling Considerations

**Current State Challenge**: Existing vocabulary management tools (VocBench, TopBraid) may not natively support nanopublication creation, requiring either:
- Tool extensions or plugins
- Workflow adaptations using export/import processes
- Development of lightweight assertion authoring interfaces

**Mitigation Strategy**: Implement nanopublication templates that can be populated through existing SKOS interfaces, with post-processing to generate proper nanopublication structures.

## 7. Implementation Considerations

### 7.1 Organisational Impact

**People**
- **Domain Experts**: Continue working within familiar SKOS workflows, with expanded property vocabularies
- **Reference Data Curators**: Enhanced role in semantic assertion validation and quality control  
- **R&D Data Office**: Coordination of assertion requirements and downstream application needs
- **Editorial Office**: New collaborative function bridging curation and modelling teams
- **Modelling Teams**: Advisory role rather than implementation bottleneck

**Process**
- **Assertion Workflows**: Extension of existing SKOS curation processes with property selection
- **Review Cycles**: Integration with established domain working group review processes
- **Quality Control**: Enhanced validation including semantic consistency checking
- **Version Management**: Extension of SKOS versioning to include assertion history
- **Training**: Focused on property selection and usage rather than semantic modelling

**Technology**
- **SKOS Tool Enhancement**: Extensions to support object property assertion and nanopublication templates
- **Property Palette Management**: Centralised vocabulary for assertion relationships
- **Quality Assurance**: Automated consistency checking and validation workflows
- **Integration APIs**: Seamless connection with existing reference data delivery systems

### 7.2 Development Artefacts

**Property Vocabularies**
- Core assertion properties (produces, isPathogenOf, hasRole, causedBy)
- Domain-specific property extensions developed with working groups
- Property usage guidelines and examples for each domain
- Mapping relationships to existing ontology properties where relevant

**Process Templates**
- Nanopublication templates for different assertion types
- Review workflow templates adapted from SKOS processes  
- Quality criteria specific to semantic assertions
- Escalation procedures for complex or disputed assertions

**Technical Components**
- Property palette management system
- Assertion validation and consistency checking tools
- Nanopublication generation utilities
- Integration adapters for downstream consumption

## 8. Success Metrics and Evaluation

### 8.1 Quantitative Metrics

- **Coverage**: Percentage of key domain concepts with semantic assertions
- **Usage**: API calls, query frequency, downstream application adoption
- **Quality**: Expert validation rates, consistency scores, error rates
- **Efficiency**: Time reduction in knowledge-intensive tasks

### 8.2 Qualitative Indicators

- **Expert satisfaction**: Ease of assertion creation and maintenance
- **Reusability**: Cross-project and cross-team knowledge sharing
- **Decision support**: Improved quality of knowledge-based decisions
- **Innovation enablement**: New applications and insights generated

## 9. Conclusion and Next Steps

The Reference Knowledge capability represents a pragmatic approach to capturing and leveraging organisational domain expertise within existing processes and capabilities. By positioning semantic assertions as expert statements *about* reference data rather than formal domain modelling, the approach avoids common implementation barriers whilst delivering significant value across R&D applications.

**Critical Success Factors:**
- **Process Integration**: Building on established SKOS curation workflows rather than creating parallel processes
- **Organisational Alignment**: Leveraging existing domain working groups and reference data management capabilities
- **Incremental Implementation**: Starting with SKOS+ patterns and evolving toward nanopublications as needs and capabilities mature
- **Editorial Office Coordination**: Ensuring collaboration between modelling and curation teams without creating dependencies

**Immediate Next Steps:**
1. **Pilot Selection**: Identify domain with active working group and clear assertion requirements
2. **Property Palette Development**: Collaborate with domain experts to define initial assertion relationship vocabulary
3. **Tooling Assessment**: Evaluate current SKOS tools for assertion capabilities and identify extension requirements
4. **Process Adaptation**: Modify existing curation workflows to include semantic assertion review and validation
5. **Pilot Implementation**: Deploy initial assertions using SKOS+ pattern with selected domain working group

**Long-term Vision:**
The Reference Knowledge capability should evolve as a natural extension of reference data management, seamlessly integrated with existing curation processes whilst providing rich semantic assertions that support advanced analytics, AI applications, and regulatory requirements. Success will be measured not by the sophistication of the underlying technology, but by the extent to which domain experts can efficiently create and maintain trusted semantic assertions within their familiar workflows.

---

## References

- Berners-Lee, T., Hendler, J., & Lassila, O. (2001). The semantic web. Scientific American, 284(5), 34-43.
- Caracciolo, C., Stellato, A., Morshed, A., Johannsen, G., Rajbhandari, S., Jaques, Y., & Keizer, J. (2013). The AGROVOC linked dataset. Semantic Web, 4(3), 341-348.
- Degtyarenko, K., de Matos, P., Ennis, M., Hastings, J., Zbinden, M., McNaught, A., ... & Steinbeck, C. (2008). ChEBI: a database and ontology for chemical entities of biological interest. Nucleic acids research, 36(suppl_1), D344-D350.
- Enterprise Data Management Council. (2024). Financial Industry Business Ontology (FIBO). Available at: https://spec.edmcouncil.org/fibo/
- Isaac, A., & Summers, E. (2009). SKOS simple knowledge organisation system primer. W3C working group note, 18.
- Knublauch, H., & Kontokostas, D. (2017). Shapes constraint language (SHACL). W3C recommendation, 20.
- Kuhn, T., et al. (2016). Nanopublications: A growing resource of provenance-centric scientific linked data. IEEE 12th International Conference on e-Science.
- Mungall, C. J., Torniai, C., Gkoutos, G. V., Lewis, S. E., & Haendel, M. A. (2012). Uberon, an integrative multi-species anatomy ontology. Genome biology, 13(1), 1-20.
- Object Management Group. (2023). Commons Roles and Compositions Ontology. Available at: https://www.omg.org/spec/Commons/RolesAndCompositions/

## Appendix A: Classified Property Palette for Reference Knowledge

The following property palette provides a structured collection of relationships for asserting reference knowledge across different contexts. Properties are classified into domain-agnostic relationships that apply universally and contextual properties that are specific to particular domains.

### A.1 Domain-Agnostic Properties

These properties have universal semantic applicability across any domain, from anatomy to engineering to artwork construction.

```turtle
@prefix rk: <http://example.org/reference-knowledge/> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix dcterms: <http://purl.org/dc/terms/> .

# 1. Part-Whole Relationships
rk:hasPart a rdf:Property ;
    rdfs:label "has part" ;
    rdfs:comment "Relates an entity to its constituent components or sub-elements." ;
    dcterms:source "Dublin Core Metadata Terms. https://www.dublincore.org/specifications/dublin-core/dcmi-terms/" .

rk:isPartOf a rdf:Property ;
    rdfs:label "is part of" ;
    rdfs:comment "Relates a component or sub-element to the larger entity it belongs to." ;
    dcterms:source "Dublin Core Metadata Terms. https://www.dublincore.org/specifications/dublin-core/dcmi-terms/" .

# 2. Temporal Relationships  
rk:precedes a rdf:Property ;
    rdfs:label "precedes" ;
    rdfs:comment "Indicates that one event, process, or entity occurs before another in time." ;
    dcterms:source "GIST Core Ontology. https://github.com/semanticarts/gist" .

rk:follows a rdf:Property ;
    rdfs:label "follows" ;
    rdfs:comment "Indicates that one event, process, or entity occurs after another in time." ;
    dcterms:source "GIST Core Ontology. https://github.com/semanticarts/gist" .

# 3. Causal Relationships
rk:causes a rdf:Property ;
    rdfs:label "causes" ;
    rdfs:comment "Indicates that one entity brings about or results in another entity or event." ;
    dcterms:source "Simple Knowledge Organisation System (SKOS). https://www.w3.org/2004/02/skos/" .

rk:isEffectOf a rdf:Property ;
    rdfs:label "is effect of" ;
    rdfs:comment "Indicates that one entity or event is the result or consequence of another." ;
    dcterms:source "GIST Core Ontology. https://github.com/semanticarts/gist" .

# 4. Compositional Relationships
rk:contains a rdf:Property ;
    rdfs:label "contains" ;
    rdfs:comment "Indicates that one entity physically or logically holds another entity within it." ;
    dcterms:source "Dublin Core Metadata Terms. https://www.dublincore.org/specifications/dublin-core/dcmi-terms/" .

rk:isContainedIn a rdf:Property ;
    rdfs:label "is contained in" ;
    rdfs:comment "Indicates that one entity is physically or logically held within another entity." ;
    dcterms:source "Dublin Core Metadata Terms. https://www.dublincore.org/specifications/dublin-core/dcmi-terms/" .

# 5. Dependency Relationships
rk:dependsOn a rdf:Property ;
    rdfs:label "depends on" ;
    rdfs:comment "Indicates that one entity requires another entity for its existence, function, or operation." ;
    dcterms:source "GIST Core Ontology. https://github.com/semanticarts/gist" .

rk:supports a rdf:Property ;
    rdfs:label "supports" ;
    rdfs:comment "Indicates that one entity provides the necessary foundation or assistance for another entity." ;
    dcterms:source "GIST Core Ontology. https://github.com/semanticarts/gist" .
```

### A.2 Agri-Food Domain Properties

These properties are contextually relevant within agricultural, food production, and nutrition domains.

```turtle
# Plant-Organism Relationships
rk:isPathogenOf a rdf:Property ;
    rdfs:label "is pathogen of" ;
    rdfs:comment "Indicates that one organism causes disease in another organism." ;
    dcterms:source "AGROVOC Thesaurus. http://aims.fao.org/aos/agrovoc" .

rk:isPestOf a rdf:Property ;
    rdfs:label "is pest of" ;
    rdfs:comment "Indicates that one organism causes damage or harm to crops or agricultural products." ;
    dcterms:source "AGROVOC Thesaurus. http://aims.fao.org/aos/agrovoc" .

# Production Relationships
rk:produces a rdf:Property ;
    rdfs:label "produces" ;
    rdfs:comment "Indicates that one agricultural entity yields or generates another entity as output." ;
    dcterms:source "AGROVOC Thesaurus. http://aims.fao.org/aos/agrovoc" .

rk:isProducedBy a rdf:Property ;
    rdfs:label "is produced by" ;
    rdfs:comment "Indicates the agricultural source or process that generates a particular product." ;
    dcterms:source "AGROVOC Thesaurus. http://aims.fao.org/aos/agrovoc" .

# Agricultural Process Relationships
rk:requiresSoilType a rdf:Property ;
    rdfs:label "requires soil type" ;
    rdfs:comment "Indicates the soil conditions necessary for optimal growth of a particular crop." ;
    dcterms:source "AGROVOC Thesaurus. http://aims.fao.org/aos/agrovoc" .

rk:hasGrowingSeason a rdf:Property ;
    rdfs:label "has growing season" ;
    rdfs:comment "Indicates the seasonal period during which a crop is typically cultivated." ;
    dcterms:source "AGROVOC Thesaurus. http://aims.fao.org/aos/agrovoc" .

# Nutritional Relationships
rk:containsNutrient a rdf:Property ;
    rdfs:label "contains nutrient" ;
    rdfs:comment "Indicates that a food product contains a specific nutritional component." ;
    dcterms:source "FoodEx2 Classification System. https://www.efsa.europa.eu/en/data/data-standardisation" .

rk:hasNutritionalValue a rdf:Property ;
    rdfs:label "has nutritional value" ;
    rdfs:comment "Relates a food product to its quantified nutritional content or benefit." ;
    dcterms:source "FoodEx2 Classification System. https://www.efsa.europa.eu/en/data/data-standardisation" .

# Processing Relationships
rk:isProcessedInto a rdf:Property ;
    rdfs:label "is processed into" ;
    rdfs:comment "Indicates the food product that results from processing a raw agricultural material." ;
    dcterms:source "AGROVOC Thesaurus. http://aims.fao.org/aos/agrovoc" .

rk:requiresProcessing a rdf:Property ;
    rdfs:label "requires processing" ;
    rdfs:comment "Indicates the processing method or technique needed to transform raw materials into food products." ;
    dcterms:source "AGROVOC Thesaurus. http://aims.fao.org/aos/agrovoc" .
```

### A.3 Pharmaceutical R&D Properties

These properties are contextually relevant within pharmaceutical research, drug development, and clinical applications.

```turtle
# Therapeutic Relationships
rk:treatsCondition a rdf:Property ;
    rdfs:label "treats condition" ;
    rdfs:comment "Indicates that a therapeutic agent is used to treat or manage a specific disease or medical condition." ;
    dcterms:source "Medical Subject Headings (MeSH). https://www.nlm.nih.gov/mesh/" .

rk:hasTherapeuticTarget a rdf:Property ;
    rdfs:label "has therapeutic target" ;
    rdfs:comment "Relates a therapeutic agent to the biological target it acts upon, such as a protein or pathway." ;
    dcterms:source "Chemical Entities of Biological Interest (ChEBI). https://www.ebi.ac.uk/chebi/" .

# Pharmacological Relationships
rk:metabolisedBy a rdf:Property ;
    rdfs:label "metabolised by" ;
    rdfs:comment "Indicates the enzyme, organ system, or biological process responsible for breaking down a substance." ;
    dcterms:source "Chemical Entities of Biological Interest (ChEBI). https://www.ebi.ac.uk/chebi/" .

rk:interactsWith a rdf:Property ;
    rdfs:label "interacts with" ;
    rdfs:comment "Indicates a pharmacological interaction between substances that may affect efficacy or safety." ;
    dcterms:source "DrugBank Database. https://go.drugbank.com/" .

# Safety and Regulatory Relationships
rk:causesAdverseEvent a rdf:Property ;
    rdfs:label "causes adverse event" ;
    rdfs:comment "Indicates that a substance or intervention may result in an unwanted or harmful medical occurrence." ;
    dcterms:source "Medical Dictionary for Regulatory Activities (MedDRA). https://www.meddra.org/" .

rk:contraIndicatedWith a rdf:Property ;
    rdfs:label "contraindicated with" ;
    rdfs:comment "Specifies that a treatment should not be used in combination with another treatment or condition." ;
    dcterms:source "Medical Subject Headings (MeSH). https://www.nlm.nih.gov/mesh/" .

# Mechanism and Pathway Relationships
rk:inhibitsPathway a rdf:Property ;
    rdfs:label "inhibits pathway" ;
    rdfs:comment "Indicates that a molecular entity blocks or reduces the activity of a specific biological pathway." ;
    dcterms:source "Reactome Pathway Database. https://reactome.org/" .

rk:activatesPathway a rdf:Property ;
    rdfs:label "activates pathway" ;
    rdfs:comment "Indicates that a molecular entity stimulates or enhances the activity of a specific biological pathway." ;
    dcterms:source "Reactome Pathway Database. https://reactome.org/" .

# Clinical and Research Relationships
rk:testedInPopulation a rdf:Property ;
    rdfs:label "tested in population" ;
    rdfs:comment "Indicates the demographic or patient group in which a treatment or intervention has been studied." ;
    dcterms:source "ClinicalTrials.gov. https://clinicaltrials.gov/" .

rk:hasEvidenceLevel a rdf:Property ;
    rdfs:label "has evidence level" ;
    rdfs:comment "Indicates the strength or quality of evidence supporting a particular clinical assertion." ;
    dcterms:source "Oxford Centre for Evidence-Based Medicine. https://www.cebm.ox.ac.uk/" .
```

### A.4 Environmental Water Management Properties

These properties are contextually relevant within water resource management, hydrology, and aquatic ecosystem domains.

```turtle
# Hydrological Relationships
rk:flowsInto a rdf:Property ;
    rdfs:label "flows into" ;
    rdfs:comment "Indicates the water body that receives flow from another water body or watercourse." ;
    dcterms:source "HydroSHEDS Database. https://www.hydrosheds.org/" .

rk:drainedBy a rdf:Property ;
    rdfs:label "drained by" ;
    rdfs:comment "Indicates the watercourse or drainage system that collects water from a particular area or basin." ;
    dcterms:source "Global Runoff Data Centre (GRDC). https://www.bafg.de/GRDC/" .

# Water Quality Relationships
rk:containsContaminant a rdf:Property ;
    rdfs:label "contains contaminant" ;
    rdfs:comment "Indicates that a water body contains a substance that may pose risks to environmental or human health." ;
    dcterms:source "Water Quality Portal. https://www.waterqualitydata.us/" .

rk:hasWaterQualityParameter a rdf:Property ;
    rdfs:label "has water quality parameter" ;
    rdfs:comment "Relates a water body to a specific measurable characteristic of its chemical or physical properties." ;
    dcterms:source "EPA Water Quality Standards. https://www.epa.gov/wqs-tech/" .

# Ecological Relationships
rk:supportsSpecies a rdf:Property ;
    rdfs:label "supports species" ;
    rdfs:comment "Indicates that a water body or aquatic habitat provides necessary conditions for a particular species." ;
    dcterms:source "IUCN Red List. https://www.iucnredlist.org/" .

rk:isHabitatFor a rdf:Property ;
    rdfs:label "is habitat for" ;
    rdfs:comment "Indicates that an aquatic environment serves as the natural home for specific organisms or communities." ;
    dcterms:source "Encyclopedia of Life (EOL). https://eol.org/" .

# Management and Infrastructure Relationships  
rk:regulatedBy a rdf:Property ;
    rdfs:label "regulated by" ;
    rdfs:comment "Indicates the infrastructure, authority, or mechanism that controls water flow or quality in a water body." ;
    dcterms:source "Global Reservoir and Dam Database (GRanD). https://sedac.ciesin.columbia.edu/data/set/grand-v1-dams-rev01" .

rk:suppliesWaterTo a rdf:Property ;
    rdfs:label "supplies water to" ;
    rdfs:comment "Indicates the recipient system, area, or use that receives water from a particular source." ;
    dcterms:source "FAO AQUASTAT. https://www.fao.org/aquastat/" .

# Operational Relationships
rk:hasWaterRights a rdf:Property ;
    rdfs:label "has water rights" ;
    rdfs:comment "Indicates the legal entity or authority that holds allocation rights for water use from a particular source." ;
    dcterms:source "Water Law and Policy. Multiple jurisdictional sources" .

rk:monitoredBy a rdf:Property ;
    rdfs:label "monitored by" ;
    rdfs:comment "Indicates the organisation, agency, or system responsible for ongoing observation and data collection." ;
    dcterms:source "Global Water Monitoring Networks. Multiple agency sources" .
```

### A.5 Usage Guidelines

**Domain-Agnostic Properties** should be used when the relationship has universal applicability and the semantics remain consistent across different contexts. For example, `hasPart` applies equally to anatomical structures, mechanical assemblies, and organisational hierarchies.

**Contextual Properties** should be used when the relationship semantics are specific to a particular domain and may not be meaningful or applicable outside that context. For example, `isPathogenOf` has specific meaning in plant pathology that doesn't translate to other domains.

**Property Selection Criteria:**
- Choose the most specific applicable property for precise semantic expression
- Use domain-agnostic properties for cross-domain integration scenarios  
- Ensure property selection aligns with existing domain working group practices
- Consider downstream application requirements when selecting property granularity

**Extension Patterns:**
- Domain working groups can propose additional contextual properties following established patterns
- New properties should include clear definitions and reference authoritative sources
- Property hierarchies can be established using `rdfs:subPropertyOf` relationships
- Regular review cycles should evaluate property usage and effectiveness

---

**Document Version**: 2.0  
**Last Updated**: June 2025  
**Authors**: Derek Scuffell, Knowmatics  
**Status**: For Review and Comment