Ansible Role: SSL
=================

[![Build Status](https://travis-ci.org/bjoernalbers/ansible-role-ssl.svg?branch=master)](https://travis-ci.org/bjoernalbers/ansible-role-ssl)

Generate SSL certificates on Mac OS X.

This role generates a self-signed Certificate Authority (CA) which then
signs each of you certificates.
Just deploy the CA certificate on your clients in order to trust your
certificates.
All stuff is by default located under `~/ssl`.


Requirements
------------

[Homebrew](http://brew.sh) must be installed which depends on Xcode and
Command Line Tools.


Role Variables
--------------

**Please overwrite these defaults!**

Your CA password:

- `ssl_ca_password`: A strong password that you'll never forget.

Settings for destinguished name which appear in your CA and certificates:

- `ssl_country`: Country Name (2 letter code) 
- `ssl_state`: State or Province Name
- `ssl_city`: Locality Name (City / Town)
- `ssl_organization`: Organization Name
- `ssl_organizational_unit`: Organizational Unit Name
- `ssl_email_address`: Email Address

A list of common names (i.e. FQDNs) for which you wanna generate certificates:

- `ssl_certificates`: List of common names (FQDN) for your servers


Dependencies
------------

None.


Example Playbook
----------------

A minimal playbook with one certificate:

    - hosts: localhost
      vars_prompt:
        - name: 'ca_password'
          prompt: 'Please enter CA password'
          private: yes
      roles:
        - role:                    bjoernalbers.ssl
          ssl_ca_password:         '{{ ca_password }}'
          ssl_country:             US
          ssl_state:               NY
          ssl_city:                New York City
          ssl_organization:        fsociety
          ssl_organizational_unit: mr. robot
          ssl_email_address:       root@whoismrrobot.com
          ssl_certificates:
            - www.whoismrrobot.com 


License
-------

MIT


Author Information
------------------

Copyright (c) 2016 Björn Albers
