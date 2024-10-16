---
icon: elementor
---

# Knowlg mirco-services: Open questions

## Background <a href="#knowlgmirco-services-openquestions-background" id="knowlgmirco-services-openquestions-background"></a>

Present(in the year 2022) the sunbird knowledge setup is not adoptor friendly to setup/deploy. The reason is because of the cost involved in setup & complexity of the multiple DB’s invovled.

How to make knowlg micro-services easy to install & bare minimum cost to setup/deploy by any adoptor.

At present, the sb-knowlg setup requires the below DB’s

* Neo4J
* Cassandra
* Redis
* ElasticSearch

## Open questions for minimal set-up <a href="#knowlgmirco-services-openquestions-openquestionsforminimalset-up" id="knowlgmirco-services-openquestions-openquestionsforminimalset-up"></a>

* Why Cassandra & Redis is mandatory for smaller projects? Can’t we setup with Neo4j & ES as primary DB’s?
* Is Redis DB can be made optional to improve the performance of caching the data?
* What happens if we store the large data in Neo4J? Can we skip this large data sync to ES even though we store it in Neo4J?

## Schema <a href="#knowlgmirco-services-openquestions-schema" id="knowlgmirco-services-openquestions-schema"></a>

* schema to have separation of[ behavioral properties from direct metadata/tags properties.](https://docs.google.com/presentation/d/130zIDMayAMuFqHkhpAnWYwfVJXDgGLHcijsKQwLDNA0/edit#slide=id.g11ff05fa5be\_8\_0)

## Lifecycle <a href="#knowlgmirco-services-openquestions-lifecycle" id="knowlgmirco-services-openquestions-lifecycle"></a>

* Separate the lifecycle with the core code of micro-services. So that any adopter can opt for the existing lifecycle or can customize it as per their need.
