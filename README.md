Ansible Role: Dataverse Upgrade
=========

Upgrades a dataverse installation to the specified version

Things to note:
* supports upgrades within version 4.x only
* currently performs an upgrade of an existing database brought into a fresh install, rather than an in-place upgrade of an existing dataverse installation
* does not currently support installations where the application and database are on separate servers
* does not perform the TwoRavens check: https://github.com/IQSS/dataverse/releases/tag/v4.9
* does not upgrade Shibboleth configuration: https://github.com/IQSS/dataverse/releases/tag/v4.6.1
* does not make use of the new :DefaultAuthProvider setting: https://github.com/IQSS/dataverse/releases/tag/v4.6.1


Requirements
------------

none

If this role is deployed with the [dataverse-ansible](https://github.com/IQSS/dataverse-ansible) role, it will utilize common variables (if available in the containing project). However, these can easily be overridden, so the presence of the dataverse-ansible role is not required.


Role Variables
--------------

    dvu_current_version:  "4.6"
    dvu_target_version:   "4.9"
    dvu_versions:
    - version:  "4.6"
    - version:  "4.6.1"
      query:    "upgrade_v4.6_to_v4.6.1.sql"
    - version:  "4.6.2"
      query:    "upgrade_v4.6.1_to_v4.6.2.sql"
    - version:  "4.7"
      query:    "upgrade_v4.6.2_to_v4.7.sql"
    - version:  "4.7.1"
      query:    "upgrade_v4.7_to_v4.7.1.sql"
    - version:  "4.8"
      query:    "upgrade_v4.7.1_to_v4.8.sql"
    - version:  "4.8.1"
    - version:  "4.8.2"
    - version:  "4.8.3"
    - version:  "4.8.4"
      query:    "upgrade_v4.8.3_to_v4.8.4.sql"
    - version:  "4.8.5"
    - version:  "4.8.6"
      query:    "upgrade_v4.8.5_to_v4.8.6.sql"
    - version:  "4.9"
      query:    "upgrade_v4.8.6_to_v4.9.0.sql"
      tasks:    true
    dvu_releases_url: "https://github.com/IQSS/dataverse/releases/download"
    dvu_working_dir:  "/home/{{ ansible_user }}"
    dvu_dbname:       "{{ dataverse.db }}"
    dvu_dbuser:       "{{ dataverse.dbuser }}"
    dvu_api_location: "{{ dataverse.api.location }}"
    dvu_provenance_enabled: true


Dependencies
------------

none


Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: dataverse-upgrade }


License
-------

CC0


Author Information
------------------

Drew Heles
