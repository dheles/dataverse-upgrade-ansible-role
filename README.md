Ansible Role: Dataverse Upgrade
=========

Upgrades a dataverse installation to the specified version

Things to note:
* supports upgrades within version 4.x only
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

    dvu_current_version:  "4.12"
    dvu_target_version:   "4.12"
    dvu_versions:
    - version:            "4.6"
    - version:            "4.6.1"
      queries:
      - "upgrade_v4.6_to_v4.6.1.sql"
    - version:            "4.6.2"
      queries:
      - "upgrade_v4.6.1_to_v4.6.2.sql"
      metadata:
      - file:     "citation.tsv"
        checksum: "sha1:98824ae60e149bac14d2bd402ce5f5108dd8fad8"
    - version:            "4.7"
      queries:
      - "upgrade_v4.6.2_to_v4.7.sql"
    - version:            "4.7.1"
      queries:
      - "upgrade_v4.7_to_v4.7.1.sql"
    - version:            "4.8"
      queries:
      - "upgrade_v4.7.1_to_v4.8.sql"
      - "3561-update.sql"
      metadata:
      - file:     "citation.tsv"
        checksum: "sha1:842888d4c09b0ff21c4571f34d56cba8441d14ec"
    - version:            "4.8.1"
    - version:            "4.8.2"
    - version:            "4.8.3"
    - version:            "4.8.4"
      queries:
      - "upgrade_v4.8.3_to_v4.8.4.sql"
    - version:            "4.8.5"
    - version:            "4.8.6"
      queries:
      - "upgrade_v4.8.5_to_v4.8.6.sql"
      tasks:              true
    - version:            "4.9"
      queries:
      - "upgrade_v4.8.6_to_v4.9.0.sql"
      metadata:
      - file:     "citation.tsv"
        checksum: "sha1:0b3eaf9c1de72dd9f04bf5c9d51c290f7485f94f"
      tasks:              true
    - version:            "4.9.1"
    - version:            "4.9.2"
      queries:
      - "upgrade_v4.9.1_to_v4.9.2.sql"
    - version:            "4.9.3"
      queries:
      - "upgrade_v4.9.2_to_v4.9.3.sql"
      solr:
      - file:     "schema.xml"
        checksum: "sha1:0181109af60f261d4a49e61cbdaaaf604ffd864a"
    - version:            "4.9.4"
    - version:            "4.10"
      queries:
      - "upgrade_v4.9.4_to_v4.10.sql"
      metadata:
      - file:     "citation.tsv"
        checksum: "sha1:f745fbe60d5c13ae4baa60ba5b51b0ddbd997fea"
      solr:
      - file:     "schema.xml"
        checksum: "sha1:261422b3164a8ead9dce04a42b356436f9b09047"
      - file:     "solrconfig.xml"
        checksum: "sha1:53c7efbf56b5968cfa86d8b1b8f312f79cc425b8"
      tasks:              true
    - version:            "4.10.1"
    - version:            "4.11"
      queries:
      - "upgrade_v4.10.1_to_v4.11.sql"
    - version:            "4.12"
      solr:
      - file:     "schema.xml"
        checksum: "sha1:148e117759810798eab2b77a1b14e77567e6e67b"
    dvu_releases_url: "https://github.com/IQSS/dataverse/releases/download"
    dvu_working_dir:  "/home/{{ ansible_user }}"
    dvu_dbname:       "{{ dataverse.db.name }}"
    dvu_dbuser:       "{{ dataverse.db.user }}"
    dvu_api_port:     "{{ dataverse_api_port }}"
    dvu_api_location: "{{ dataverse.api.location }}"
    dvu_glassfish_root: "{{ dataverse.glassfish.root }}"
    dvu_glassfish_user: "{{ dataverse.glassfish.user }}"
    dvu_provenance_enabled: true
    dvu_solr_config_dir: "{{ dataverse.solr.root }}/server/solr/collection1/conf/"
    dvu_extra_metadata_dir: ""
    dvu_extra_metadata:     []
    dvu_debugging:    "{{ debugging | default(false) }}"


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
