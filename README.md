OMERO MS Image Region
=====================

[![Actions Status](https://github.com/ome/ansible-role-omero-server/workflows/Molecule/badge.svg)](https://github.com/ome/ansible-role-omero-server/actions)
[![Ansible Role](https://img.shields.io/badge/ansible--galaxy-omero_ms_image_region-blue.svg)](https://galaxy.ansible.com/ui/standalone/roles/ome/omero_server/)

Installs and configures OMERO ms image region

Dependencies
------------

OMERO.server and OMERO.web are required.


Role Variables
--------------

- omero_ms_image_region_user: Microservice user, the default is 'omero-server'
- omero_ms_image_region_folder: Microservice installation folder
- omero_ms_image_region_port: Microservice port 
- omero_ms_image_region_db_url: OMERO database URL
- omero_ms_image_region_db_port:  OMERO database server port
- omero_ms_image_region_db_name: OMERO database name
- omero_ms_image_region_db_username: OMERO database user name
- omero_ms_image_region_db_pass: OMERO database user password
- omero_ms_image_region_log_level: Logging level, allowed values: ``info``, ``debug``,  ``error``
- omero_data_dir: OMERO data folder
- omero_script_repo_root: OMERO scripts folder
- omero_ms_image_region_worker_pool_size: No of Microservice workers, the default is double the number of processors which the machine has
- session_id: OMERO Session id, if you do not know it, you may get it using this command:
- omero_ms_image_region_max_active_channels: Max number of channels to allow per request default is 10

    /opt/omero/web/OMERO.web/bin/omero config get omero.web.session_cookie_name

- omero_ms_image_region_update_nginx: if false, it will not update the nginx config file

- omero_ms_image_region_download_URL: The download URL for the distributed ms build (zip file)
- omero_ms_image_region_package_sha256: The sha256 for the distributed ms build

The ms build should be compatible with the installed OMERO.server, i.e.:
- The bio-format version for the Microservice should match the Bio-Formats version of the OMERO.server
- Also, in the case of using ngff data, the version of OMEZarrReader should be the same for both the Microsevice and the OMERO.server.

Example Playbook
----------------

    - hosts: localhost
      roles:
        - role: ome.omero_ms_image_region
          omero_ms_image_region_update_nginx: true

Another example:
----------------
The following example is used to deploy in multiple nodes and configure the ms download url and other roles variables 

    - hosts: nodes
      become: true
    
      roles:
        - role: ome.omero_ms_image_region
          omero_ms_image_region_update_nginx: true
          omero_ms_image_region_db_url: databse_url
          omero_ms_image_region_db_name: database_name
          omero_ms_image_region_db_username: database_username
          omero_ms_image_region_db_pass: database_password
          omero_data_dir: /data/OMERO
          omero_ms_image_region_session_id: sessionid
          # URL for the Latest build which support bio-format 7.3 and and latest zar reader (i.e. 0.5.1)  
          omero_ms_image_region_download_URL: 'https://github.com/khaledk2/ice-archh-64/releases/download/New_M/omero-ms-image-region-0.8.7.zip' 
          # sha256 for the Latest build
          omero_ms_image_region_package_sha256: 2ce62fb6c5ff3f75bcc72d7a068d2c0b3667eb8787989f86eba045f958bab780
