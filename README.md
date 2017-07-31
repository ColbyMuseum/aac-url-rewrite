# aac-url-rewrite

Apache configuration files rewriting linked data repository URLs (eg, 'http://data.americanartcollaborative.org/ccma/object/4') into museum-branded URLs (eg, `http://data.museum.colby.edu/object/4`). Uses a mapping file, `shortnames.txt`, to match the hostnames to repo names.

## Goals
If I go to `http://data.instituion.org/XXX` return data from `http://data.americanartcollaborative.org/inst/XXX` without a redirect. 

## Usage
Provided you have apache and mod_rewrite installed, put `shortnames.txt` in `/etc/apache2` and copy `000-default.conf` in `/etc/apache2/sites-available`, put some files in `/var/www/html/rewritten`, and restart apache.

## FIXME:
- Does not account for proxying beneath the hostname map. Should work with `[L,P]` as the option term as long as the proxy is set up correctly?
- Relative URL madness. Fix by only enabling the rule only if the repo-name appears in the path.
- Check other accept-types/content-types. It would be nice to pass along Pubby's raw data dump, eg.