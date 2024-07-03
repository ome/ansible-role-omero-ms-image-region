OMERO MS Image Region
=====================

[![Actions Status](https://github.com/ome/ansible-role-omero-server/workflows/Molecule/badge.svg)](https://github.com/ome/ansible-role-omero-server/actions)
[![Ansible Role](https://img.shields.io/badge/ansible--galaxy-omero_ms_image_region-blue.svg)](https://galaxy.ansible.com/ui/standalone/roles/ome/omero_server/)

Installs and configures the OMERO microservice image region.

Dependencies
------------

OMERO.server and OMERO.web are required.


Role Variables
--------------

- `omero_ms_image_region_user`: The microservice user, the default is `omero-server`
- `omero_ms_image_region_folder`: The microservice installation folder
- `omero_ms_image_region_port`: The microservice port 
- `omero_ms_image_region_db_url`: The OMERO database URL
- `omero_ms_image_region_db_port`:  The OMERO database server port
- `omero_ms_image_region_db_name`: The OMERO database name
- `omero_ms_image_region_db_username`: The OMERO database user name
- `omero_ms_image_region_db_pass`: The OMERO database user password
- `omero_ms_image_region_log_level`: The logging level, allowed values: ``info``, ``debug``,  ``error``
- `omero_data_dir`: The OMERO data folder
- `omero_script_repo_root`: The OMERO scripts folder
- `omero_ms_image_region_worker_pool_size`: Number of microservice workers, the default is double the number of available processors
- `session_id`: The OMERO session identifier, if you do not know it, you may get it using this command:

   /opt/omero/web/OMERO.web/bin/omero config get omero.web.session_cookie_name

- `omero_ms_image_region_max_active_channels`: The maximum number of channels to allow per request, the default is `10`
- `omero_ms_image_region_update_nginx`: if set to `false`, it will not update the NGINX configuration file
- `omero_ms_image_region_download_URL`: The download URL for the distributed microservice build (zip file)
- omero_ms_image_region_package_sha256: The sha256 for the distributed microservice build


The microservice build must compatible with the installed OMERO.server:
- The Bio-Formats version used in the microservice must match the Bio-Formats version of the OMERO.server.
- Also, in the case of using NGFF data, the version of OMEZarrReader should be the same for both the Microsevice and the OMERO.server.

Example Playbook
----------------

    - hosts: localhost
      roles:
        - role: ome.omero_ms_image_region
          omero_ms_image_region_update_nginx: true

Another example:
----------------
The following example is used to deploy in multiple nodes and configure the ms download url and other roles variables 
For example, it can be used to deploy the microservice on the idr omeroreadonly servers. The variable values inside the playbook should be modified for the idr environment in which the ms will be deployemnt

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


Author Information
------------------

ome-devel@lists.openmicroscopy.org.uk
