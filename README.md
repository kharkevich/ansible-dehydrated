Dehydrated
==============

Install and configure `dehydrated` and `dns-lexicon`. Add cron task for certificates renewals.

Requirements
------------

The role installs on host:

  * python-pip
  * openssl
  * unzip
  * boto3
  * dns-lexicon

In case of using HTTP chalenge this role required a webserver with correct processing
`http://<your-domain>/.well-known/acme-challenge/` context path for ACME challenge.


Role Variables
--------------

### Variables (DNS challenge):

#### CONTACT_EMAIL

Address for the letsencrypt informational notices (expiration, etc.)

    CONTACT_EMAIL: replayceme@example.com

#### LEXICON_PROVIDER

DNS provider for completing DNS challenge. Full list see on `lexicon`(https://github.com/AnalogJ/lexicon/) page.

    LEXICON_PROVIDER: route53

#### LEXICON_USERNAME

Username for API access to your DNS provider (if it required)

    LEXICON_USERNAME: APIUSERNAME

#### LEXICON_TOKEN

Token / password for API access to your DNS provider (if it required)

    LEXICON_TOKEN:

#### LEXICON_DELEGATED

Delegated level domain. Route53 example: in case of using mydomain.domain.company.com should be setted to mydomain.domain value.

    LEXICON_DELEGATED: mydomain.domain

#### DOMAIN_LIST

List of domains for certificates issuing. All certificates will be stored to `CERTDIR` directory. Alternate names not supported yet.

    DOMAIN_LIST:
      - srv1.mydomain.domain.company.com
      - site2.mydomain.domain.company.com

#### DEHYDRATED_DEPLOY_CHALLENGE

TDB

#### DEHYDRATED_CLEAN_CHALLENGE

TDB

#### DEHYDRATED_DEPLOY_CERT

TDB

#### DEHYDRATED_UNCHANGED_CERT

TDB

#### Additional variables

For more details take look at `defaults/main.yml`


Dependencies
------------

None.


Example Playbook
----------------

    ---
    - name: test
      hosts: remote_host
      become: true
      roles:
        - role: ansible-dehydrated
      vars:
        LEXICON_USERNAME: SOMEUSERNAME
        LEXICON_TOKEN: SECRETOKEN
        LEXICON_DELEGATED: srv.projects.ou
        DOMAIN_LIST:
          - example.srv.projects.ou.company.com


Testing
-------

Use [molecule](https://molecule.readthedocs.io/) for testing


License
-------

CC-BY 4.0

Author Information
------------------

This role was by [Aliaksandr Kharkevich](https://github.com/kharkevich)
