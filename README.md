# aac-url-rewrite

Apache configuration files to create per-hostname URL mapping. 

## Goals

Rewrites URLs to account for AAC institutionally-branded URLs so that if a hostname has a DNS entry to a SPARQL/Pubby endpoint, returned results appear with the appropriate hostname.

If it works correctly `http://data.instituion.org/XXX` will serve data from `http://data.americanartcollaborative.org/inst/XXX` without a redirect. 

## Usage

Provided you have apache and mod_rewrite installed, move `shortnames.txt` to `/etc/apache2` and copy `000-default.conf` to `/etc/apache2/sites-enabled`, restart apache.