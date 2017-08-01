# aac-url-rewrite

Apache and Pubby configuration files enabling branded linked data repository URLs served from a single Pubby instance and SPARQL endpoint.

## Goals
When an instituion creates a DNS entry that points to the AAC pubby instance, requests to that hostname (eg `http://data.museum.colby.edu/object/4`) should return data from the AAC dataset, served by the Pubby instance at `http://data.americanartcollaborative.org`.

## Example 
[](http://aac-test.weichbild.com/ccma/object/4) returns data directly from the Pubby instance, [](http://rewritten.weichbild.com/object/4) returns the same data only from a different hostname.

## Usage
Just a demo, not really meant for use just yet.

## FIXME:
- Maintenance: each instituion needs a VirtualHost term (Apache) and a multiURIMapping term (Pubby).