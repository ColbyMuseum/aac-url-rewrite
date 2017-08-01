# aac-url-rewrite

A speculative set of Apache and Pubby files enabling branded linked data repository URLs with just a DNS entry. 

## Goals
When an instituion creates a DNS entry that points to the AAC pubby instance, requests to the hostname (eg `http://data.museum.colby.edu/object/4`) should return data from the AAC dataset without any additional work on their part. Server-side configuration should be minimal, reasonable, and maintainable (ie, not a giant blob of Apache configuration and possibly automated).

## How it works
The AAC endpoint is (probably) running as a proxy internal to the server, proxying requests to a local pubby instance (that then makes requests to a locally-hosted SPARQL endpoint). ISI has already modified Pubby to understand that certain paths indicate different URI constructions: when it receives a request for '/cbm/object/40', it checks its configuration to see how URLs should be constructed (in this case as `http://data.crystalbridges.org/object/40`) and runs a SPARQL query for data about that URL.

This configuration extends this behavior to the HTTP routing layer using `mod_proxy_express` to make Apache act like a inbound hostname-based switch, proxying traffic to the Pubby repo name paths it already uses to construct URIs. The mappings from hostname to repo name are managed in a text file list (`express-map.txt`) of hostnames and proxy paths. Each entry in the mapping is equivalent to:

```
<VirtualHost *:80>
	ServerName hostname.to.map
    ProxyPass / http://destination:port/path
    ProxyPassReverse / http://desitination:port/path
</VirtualHost>
```

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