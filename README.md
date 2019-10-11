# p419dcatservices

## Axioms

1. primary audience for schema.org markup is harvesters
2. the common denominator across search interfaces of most harvesters is a single text box (for harvester-specific DSL queries)
3. a typical schema.org harvester should not be expected to understand other vocabularies outside of schema.org

## Analysis of Axioms

1. schema.org for Data Services should help harvesters find and understand how to present these services _as a search result_
2. for smart-handoffs from harvesters, schema.org for Data Services should help harvesters _pass along single text box query_ to the service
3. to support pass thru service calls for [schema.org] class-specific searches (such as the Dataset class), the schema.org markup describing services must express:
    1. _the result set is specific to the schema.org class_ being searched (i.e. Dataset objects are being returned as search results from executing a service call)
    2. the response is formatted as _parseable schema.org_ (JSON-LD or HTML response, to support RDFa, microformats, etc.)

## Issues

| Issue |
| ----- |
| [What is the schema.org model for offering Data Services and Continuous Feeds?](https://github.com/earthcubearchitecture-project418/p419dcatservices/issues/3) |
| [Can we use Wikidata for canonical data service types?](https://github.com/earthcubearchitecture-project418/p419dcatservices/issues/2) |

## References

* [DCAT Version 2](https://w3c.github.io/dxwg/dcat/) (https://w3c.github.io/dxwg/dcat/)
* [Machine Readable Web APIs with Schema.org Action Annotations](https://doi.org/10.1016/j.procs.2018.09.025) (https://doi.org/10.1016/j.procs.2018.09.025)

# Guidance

## Describing APIs

[schema:WebAPI](https://schema.org/WebAPI) extends the generic [schema:Service](https://schema.org/Service) by adding a single field [schema:documentation](https://schema.org/documentation) which links the 'Service' of the API to its documentation - either a [schema:CreativeWork](https://schema.org/CreativeWork) or a simple URL.

### WebAPI documentation as a URL:
<pre>
{
  "@context": "http://schema.org/",
  "@type": "WebAPI",
  "name": "Google Knowledge Graph Search API",
  "description": "The Knowledge Graph Search API lets you find entities in the Google Knowledge Graph. The API uses standard schema.org types and is compliant with the JSON-LD specification.",
  <strong>"documentation": "https://developers.google.com/knowledge-graph/",</strong>
  "termsOfService": "https://developers.google.com/knowledge-graph/terms",
  "provider": {
    "@type": "Organization",
    "name": "Google Inc."
  }
}
</pre>

### WebAPI documentation as a CreativeWork (example: OpenSearch API): 
<pre>
{
  "@context": "http://schema.org/",
  "@type": "WebAPI",
  "name": "Open Search API for Example Repository",
  "description": "The Open Search API lets you find entities in the Data Catalog of the Example Repository.",
  <strong>"documentation": {
    "@type": "HowTo",
    "additionalType": "http://www.wikidata.org/entity/Q1294021",
    "name": "Open Search API for Example Repository Data Catalog"
  },</strong>
  "provider": {
    "@id": "https://www.example-repository.org",
    "@type": "Organization",
    "name": "Example Repository"
  }
}
</pre>

For being more explicit about the type of [schema:documentation](https://schema.org/documentation), see the [sub types of a schema:CreativeWork](https://schema.org/CreativeWork#subtypes). Notable types: [Article](https://schema.org/Article), [DigitalDocument](https://schema.org/DigitalDocument), [HowTo](https://schema.org/HowTo), [WebPage](https://schema.org/WebPage), etc.

### Wikidata API types 

Note inn the above CreativeWork example, we specify the *type* of WebAPI by using the [schema:additionalType](https://schema.org/additionalType) field.

* SPARQL endpoint - http://www.wikidata.org/entity/Q26261192
* CSW - http://www.wikidata.org/entity/Q661823
* OAI-PMH - http://www.wikidata.org/entity/Q2430433
* JSON API - http://www.wikidata.org/entity/Q28758133
* OpenSearch - http://www.wikidata.org/entity/Q1294021
* WMS - http://www.wikidata.org/entity/Q974922
* WFS - http://www.wikidata.org/entity/Q2296308
* GeoNetwork - http://www.wikidata.org/entity/Q477787
* GeoServer - http://www.wikidata.org/entity/Q1502779
* OPeNDAP - http://www.wikidata.org/entity/Q7072878
* Apache SOLR - http://www.wikidata.org/entity/Q2858103

*Is an API type missing from this list?*
1. Check Wikidata: [https://www.wikidata.org/w/index.php?search=](https://www.wikidata.org/w/index.php?search=)
    
2. If no type at Wikidata, [create it](https://www.wikidata.org/wiki/Special:NewItem)
