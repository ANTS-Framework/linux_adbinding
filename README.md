linux adbinding
=========

[![Build Status](https://travis-ci.org/ANTS-Framework/linux_adbinding.svg?branch=master)](https://travis-ci.org/ANTS-Framework/linux_adbinding)

Join your linux client to AD using sssd.

Role Variables
--------------

```yml
    linux_adbinding__domain: ADS.EXAMPLE.ORG
    linux_adbinding__ou: CN=Computers,DC=ADS,DC=EXAMPLE,DC=ORG
    linux_adbinding__user: bind-user
    linux_adbinding__password: bind-users-password
    linux_adbinding__dependencies_yum:
        - sssd
        - sssd-ad
        - sssd-client
        - sssd-common
        - sssd-common-pac
        - sssd-krb5
        - sssd-krb5-common
        - adcli
        - krb5-libs
        - krb5-workstation
        - pam_krb5
        - authconfig
        - oddjob
        - oddjob-mkhomedir
    linux_adbinding__dependencies_apt:
        - sssd
```

Example Playbook
----------------

```yml
    - hosts: clients
      vars:
        - linux_adbinding__domain: ADS.EXAMPLE.ORG
        - linux_adbinding__ou: CN=Computers,DC=ADS,DC=EXAMPLE,DC=ORG
        - linux_adbinding__user: bind-user
        - linux_adbinding__password: bind-users-password
      roles:
        - linux_adbinding
```

License
-------

GPLv3

Author Information
------------------
Part of the [ANTS Framework](https://ants-framework.github.io/)
