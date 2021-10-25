[![forthebadge](https://forthebadge.com/images/badges/makes-people-smile.svg)](https://forthebadge.com) [![forthebadge](https://forthebadge.com/images/badges/kinda-sfw.svg)](https://forthebadge.com)

[![forthebadge](https://forthebadge.com/images/badges/compatibility-pc-load-letter.svg)](https://forthebadge.com)

[![forthebadge](https://forthebadge.com/images/badges/open-source.svg)](https://forthebadge.com)



## CONTENTS
* [Introduction](#introduction)
* [TechStack](#techstack)
* [Gophish](#gophish)

## Introduction
Email-Spoofer is a Docker based tool that automates setting up PTR, SPF, DKIM and ARC infrastructure. For email domains that have missing or misconfigured DMARC records, this utility will spoof email to the extent the headers will contain a passing score as follows:

* spf=pass
* dkim=pass
* dmarc=pass 
* action=none

## TechStack

GoDaddy: Domain Procurement
*   Purchase a domain from GoDaddy

CloudFlare: Programmatic DNS Record Creation
*	Add your procured domain from GoDaddy into your CloudFlare account
*	Replace your GoDaddy nameservers with the nameservers provided by CloudFlare
*   Generate a Zone.DNS API token in Cloudflare to automate DNS configuration for mx, spf, dkim, _dmarc

DigitalOcean: Cloud Hosting Provider
*	DigitalOcean provides port 25 enabled by default
*	Create one DigitalOcean Ubuntu droplet
    - Droplet Location: United States
    - Droplet Access: SSH Key
    - Droplet Hostname: your-godaddy-domain.com

Digital Ocean Droplet: Setup Commands
*	git clone https://github.com/kyle-lanier-mscs/email-spoofer.git
*	sudo apt update && apt install docker-compose
*	cd email-spoofer/
*   vi settings.env
    - Replace all instances of example.com with your-godaddy-domain.com
    - Provide your Cloudflare API token
*   docker-compose up

Tech Stack Automation: docker-compose up
*	CloudFlare DNS configuration: 100% automated
*	Digital Ocean Droplet configuration: 100% automated
    - Container-1: Gophish server
    - Container-2: Postfix server
    - Container-3: Rspamd server
*   https Gophish access via https://your-godaddy-domain.com:3333

## Gophish

The Gophish web management portal will be accessible on `https://your-godaddy-domain:3333`. You need to log in using the default Gophish credentials. 

With versions `0.9.0` and below the default username and password is `admin` and `gophish`. On newer versions of Gophish, the password is automatically generated and can be retrieved by `docker logs {gophish-container-name}`.