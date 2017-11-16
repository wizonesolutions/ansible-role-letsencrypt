Let's Encrypt (acme.sh)
=========

This role installs [acme.sh](https://github.com/Neilpang/acme.sh) and generates certificates with
it. Acme.sh is a useful, versatile, lightweight shell script for interacting with Let's Encrypt
(a so-called ACME Client). It supports many Let's Encrypt challenge types, including **dns-01**,
which allows domain verification through a `TXT` record in DNS. This lets you generate certificates
for non-public domains, and acme.sh can automatically process this challenge (with Certbot, you
must manually create `TXT` records).

Requirements
------------

- Git. A role like `geerlingguy.git` will install this for you.
- Assumes that you are using acme.sh 2.7.4+ (if you change the version via role configuration, it
may break).
- Ownership of the domains you wish to validate
- An essential understanding of how acme.sh works. I recommend visiting the project page linked
above and understanding your desired command invocation. This role lets you override most of it so
that you can take advantage of its features.
- Proper webserver configuration. This is your responsibility.

Role Variables
--------------

See `defaults/main.yml`. It is important to read the notes on how to configure the role. Namely,
you will want to ensure that `acme_sh_env` is changed from the default value (which points to the
ACME staging server), at least when you want to generate real SSL certificates.

Dependencies
------------

Currently none.

Example Playbook
----------------

    - hosts: all
      roles:
        - role: wizonesolutions.letsencrypt
          # To use the production ACME server.
          acme_sh_env: ''
          acme_sh_account_email: 'example@example.com'
          acme_sh_primary_domain: 'example.com.com'
          acme_sh_key_file: '/etc/nginx/certs/{{ acme_sh_primary_domain }}_key.pem'
          acme_sh_fullchain_file: '/etc/nginx/certs/{{ acme_sh_primary_domain }}_fullchain.pem'
          acme_sh_reloadcmd: 'service nginx force-reload'
         

License
-------

MIT

Author Information
------------------

Kevin Kaland ([WizOne Solutions](https://www.wizonesolutions.com))

Sponsored by [Project Ricochet](https://projectricochet.com): Drupal Development and Meteor Development, Bay Area
