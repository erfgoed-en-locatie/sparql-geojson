sparql-geojson
==============

A SPARQL+JSON to GeoJSON adapter

RATIONALE
SPARQL-GeoJSON adapter bridges the gap between the application/sparql-results+json MIME type and GeoJSON encoding format by supplying a Javascript conversion library. It handles GeoJSON serialising of application/sparql-results+json results in the
<http://www.w3.org/2003/01/geo/wgs84_pos#> vocabulary using lat/long WGS84 point notation;
<http://www.opengis.net/ont/geosparql#> vocabulary using the well-known text literal notation. 

GeoJSON is a geographical Javascript Object Notation (JSON) encoding format endorsed by the Open Geospatial Consortium, supported by OpenLayers, Leaflet, Google Maps and many other web mapping libraries and API’s. It is the premier interoperability standard for Javascript geometric feature integration in web mapping components.  

Enter the Semantic Web. The Semantic Web is a movement led by W3C promoting the use (or conversion) of web content in an interoperable data exchange domain, rather than a semi-structured collection of web pages. Linked data is the implementation of the semantic web, using the Resource Description Framework as its main instrument to interlink knowledge triples with common vocabularies, it allows users to query data across domains, throughout the web. Most ‘endpoints’ - access nodes to linked data - employ SPARQL as query language for the underlying data set, hence the common name ‘SPARQL endpoint’. Most SPARQL endpoints support output of JSON as MIME type application/sparql-results+json for easier integration into (web) applications. 

Currently, there are two main vocabularies for supplying geometries in RDF. The first originates at W3C as the Basic Geo (WGS84 Lat/Long) Vocabulary, the second was issued by the Open Geospatial Consortium as the GeoSPARQL vocabulary. The former only supports point geometries, the latter supports the full OGC Simple Features Specification of geometries in the form of well-known text literals. 

There are no SPARQL endpoints with direct output support for GeoJSON, yet there are sufficient methods for querying geometric features using SPARQL. SPARQL-GeoJSON aims to bridge this gap by providing a conversion library, allowing direct integration of SPARQL endpoints in web mapping applications.

Input
SPARQL-GeoJSON provides the function toGeoJSON(var objSparqljson, var projection) 
arguments: 
objSparqljson: a JSON object containing a sparql query result in application/sparql-results+json MIME type. 

projection: optional, either empty, null or integer. 
Default (empty) is urn:ogc:def:crs:OGC:1.3:CRS84 as specified for GeoJSON. 
JSON null specifies that no known projection method is used. No crs clause is specified in the GeoJSON output.
If otherwise specified, projection refers to the EPSG projection identifier. For example, if for projection value 28992 is given, the GeoJSON object will have a named CRS as follows:
"crs": {
  "type": "name",
  "properties": {
    "name": "urn:ogc:def:crs:EPSG::28992"
    }
  }
Output
SPARQL-GeoJSON returns the sparql/json input as a GeoJSON object according to the specified format.

Roadmap
Milestone: 0.1
Extracts datatype <http://www.opengis.net/ont/geosparql#wktLiteral> from a SPARQL/JSON object and returns GeoJSON output only as EPSG:4326/urn:ogc:def:crs:OGC:1.3:CRS84 geometries. Ignores all other Sparql/JSON data, no feature attributes other than geometries are returned. Has JQuery dependency.
Milestone: 0.2
Extracts datatype <http://www.opengis.net/ont/geosparql#wktLiteral> and <http://www.w3.org/2003/01/geo/wgs84_pos#> from a SPARQL/JSON object and returns GeoJSON output only as EPSG:4326/urn:ogc:def:crs:OGC:1.3:CRS84 geometries. Ignores all other Sparql/JSON data, no feature attributes other than geometries are returned. Has JQuery dependency.

