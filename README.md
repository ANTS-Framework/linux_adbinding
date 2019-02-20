linux adbinding
=========

[![Build Status](https://travis-ci.org/ANTS-Framework/linux_adbinding.svg?branch=master)](https://travis-ci.org/ANTS-Framework/linux_adbinding)

Join your linux client to AD using sssd and realmd.

Role Variables
--------------

```yml
    linux_adbinding__domain: ADS.EXAMPLE.ORG
    linux_adbinding__ou: CN=Computers,DC=ADS,DC=EXAMPLE,DC=ORG
    linux_adbinding__user: bind-user
    linux_adbinding__password: bind-users-password
```

`linux_adbinding__domain` and `linux_adbinding__ou` are optional.

Realmd can usually discover the AD domain automatically, so the domain should only need to specified if there are more than 1 domain in use or if the discovery process doesn't work.

The OU in which to save the computer object will default to the Computers OU if it is not specified, so this OU should only need to be specified when the computer object needs to be created in a different OU.

`linux_adbinding__user` and `linux_adbinding__password` are mandatory and always needed. It is recommended that these be stored in an ansible vault.

Currently this role cannot remove your client client from AD. To do this, use `sudo realm leave` or `sudo realm leave -U <bind-user>`. If you specify the bind-user credentials this will additionally delete the computer object in AD. If you don't specify this, the workstation will no longer be bound however the computer object will remain in AD.

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

or store the credentials in a vault and leave domain and ou as unspecified:

```yml
    - hosts: clients
      vars_files: linux_adbinding_vault.yml
      roles:
        - linux_adbinding
```

License
-------

GPLv3

Author Information
------------------
Part of the [ANTS Framework](https://ants-framework.github.io/)
