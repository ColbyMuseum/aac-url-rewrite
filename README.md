# aac-url-rewrite

Apache and Pubby configuration files enabling branded linked data repository URLs served from a single Pubby instance and SPARQL endpoint.

## Goals
When an instituion creates a DNS entry that points to the AAC pubby instance, requests to that hostname (eg `http://data.museum.colby.edu/object/4`) should return data from the AAC dataset, served by the Pubby instance at `http://data.americanartcollaborative.org`.

## Example 
[http://aac-test.weichbild.com/ccma/object/4](http://aac-test.weichbild.com/ccma/object/4) returns data directly from the Pubby instance, [http://rewritten.weichbild.com/object/4](http://rewritten.weichbild.com/object/4) returns the same data on requests from a different hostname.

## Usage
Assuming Ubuntu:
- Install apache (`apt-get update ; apt install apache2`)
- Enable mass proxying (`a2enmod proxy_express`)
- Put `000-default.conf` in `/etc/apache2/sites-available/`
- Edit the proxy mapping, `express-map.txt` as needed
- Compile the proxy mapping: `httxt2dbm -v -f SDBM -i express-map.txt -o /etc/apache2/conf-available/emap`
- Restart apache (and tomcat)


## FIXME:
- Each instituion still needs a multiURIMapping entry in the pubby configuration.