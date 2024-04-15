OMERO MS Image Region
=====================

[![Actions Status](https://github.com/ome/ansible-role-omero-server/workflows/Molecule/badge.svg)](https://github.com/ome/ansible-role-omero-server/actions)
[![Ansible Role](https://img.shields.io/badge/ansible--galaxy-omero_ms_image_region-blue.svg)](https://galaxy.ansible.com/ui/standalone/roles/ome/omero_server/)

Installs and configures OMERO ms image region

Dependencies
------------

OMERO-Server and OMERO-Web are required.


Role Variables
--------------

- omero_ms_image_region_user: 'omero-server': icroservice user, the defaults is omero-server
omero_ms_image_region_user: 'omero-server'
- omero_ms_image_region_folder: Microservice installation folder
- omero_ms_image_region_port: Microservice port 
- omero_ms_image_region_db_url: Omero Database URL
- omero_ms_image_region_db_port:  Omero database server port
- omero_ms_image_region_db_name: Omero database name
- omero_ms_image_region_db_username: Omero database user name
- omero_ms_image_region_db_pass: 'omero' :Omero database user password
- omero_ms_image_region_log_level: Log level, it can be info, debug or error
- omero_data_dir: Omero data folder
- omero_script_repo_root: Omero scripts folder
- omero_ms_image_region_ms_worker_pool_size: No of Microservice workers, the default is double the number of processors which the machine has
- session_id: Omero Session id, if you do not know it, you may get it using this command:


    /opt/omero/web/OMERO.web/bin/omero config get omero.web.session_cookie_name

- omero_ms_image_region_update_nginx: if false, it will not update the nginx config file

Example Playbook
----------------

    - hosts: localhost
      roles:
        - role: ome.omero_ms_image_region
          omero_ms_image_region_update_nginx: true
