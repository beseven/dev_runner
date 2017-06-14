# Docker-compose files for local development for C2S repos

## Pre-requisites:

* Clone all dependent service repos into `~/code`
  * `cd ~/code && git clone https://github.com/nhsuk/connecting-to-services.git`
  * `cd ~/code && git clone https://github.com/nhsuk/nearby-services-api.git`
  * `cd ~/code && git clone https://github.com/nhsuk/pharmacy-db.git`
  * `cd ~/code && git clone https://github.com/nhsuk/profiles.git`
  * `cd ~/code && git clone https://github.com/nhsuk/profiles-db.git`
  * `cd ~/code && git clone https://github.com/nhsuk/gp-finder.git`
  * `cd ~/code && git clone https://github.com/nhsuk/profiles-db-elastic.git`

* Create an .env file based on the .env_sample

## Steps for local development:

Use scripts to run the development environment as well as the tests for each of the applications from [scripts](scripts/README.md)

## Optional tools for debugging:

* For the Profiles and Pharmacy Finder stack when using MongoDB, you can use [Robomongo](https://robomongo.org/) 

* For the GP Finder an alternative to using `curl` for ES config, querying and also for visualisation is [kibana](https://www.elastic.co/products/kibana).
  For the latest version go [here](https://www.elastic.co/guide/en/kibana/current/install.html) or your OS package manager. 

Troubleshooting ES:
* In case you have any issues of compatibility, please check [here](https://www.elastic.co/support/matrix#show_compatibility).

Quickstart ES: 
* On first use please remember the default port for ES is `9200` and the default index is `profiles`. [Here](https://www.youtube.com/watch?v=mMhnGjp8oOI) is a comprehensive intro.
* The examples for the `Dev Tools` tab are the same as the ones using [`curl`](https://github.com/nhsuk/profiles-db-elastic#full-text-search-example)
* Example query for the `Discover` tab when you choose the `"name", "alternativeName", "address.addressLines", "address.postcode", "doctors"` as the source:
```
{"bool": {"must": {"multi_match": {"query": "Beech House Surgery", "fields":["name^2","alternativeName"], "operator":"and"}}, "should": [{"match_phrase": {"name": {"query": "Beech House Surgery", "boost":2}}}]}}
```
