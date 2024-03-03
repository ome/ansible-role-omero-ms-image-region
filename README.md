OMERO MS Image Region
=====================

[![Actions Status](https://github.com/ome/ansible-role-omero-server/workflows/Molecule/badge.svg)](https://github.com/ome/ansible-role-omero-server/actions)
[![Ansible Role](https://img.shields.io/badge/ansible--galaxy-omero_ms_image_region-blue.svg)](https://galaxy.ansible.com/ui/standalone/roles/ome/omero_server/)

Installs and configures OMERO ms image region
https://github.com/ome/omero-ms-image-region
https://github.com/glencoesoftware/omero-ms-image-region?tab=readme-ov-file

Dependencies
------------

OMERO-Server and OMERO-Web are required.


Role Variables
--------------

- ms_user: 'omero-server': icroservice user, the defaults is omero-server
ms_user: 'omero-server'
- ms_folder: Microservice installation folder
- databse_url: Omero Database URL
- db_port:  Omero database server port
- db_name: Omero database name
- db_user_name: Omero database user name
- db_pass: 'omero' :Omero database user password
- log_evel: Log level, it can be info, debug or error
- omero_data_dir: Omero data folder
- omero_script_repo_root: Omero scripts folder
- worker_pool_size: No of Microservice workers, the default is double the number of processors which the machine has
- session_id: Omero Session id, if you do not know it, you may get it using this command:


    /opt/omero/web/OMERO.web/bin/omero config get omero.web.session_cookie_name

- update_nginx: if false, it will not update the nginx config file

Example Playbook
----------------

    - hosts: localhost
      roles:
        - role: ome.omero_ms_image_region
          update_nginx: true
