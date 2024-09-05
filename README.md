OMERO MS Image Region
=====================

[![Actions Status](https://github.com/ome/ansible-role-omero-ms-image-region/workflows/Molecule/badge.svg)](https://github.com/ome/ansible-role-omero-ms-image-region/actions)
[![Ansible Role](https://img.shields.io/badge/ansible--galaxy-omero_ms_image_region-blue.svg)](https://galaxy.ansible.com/ui/standalone/roles/ome/omero_ms_image_region/)

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
- `omero_ms_image_region_package_sha256`: The sha256 for the distributed microservice build
- `java_version`: The Java version matching the server version. Supported versions are 11, 17 and 21

The microservice build **must be compatible** with the installed OMERO.server:
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
The following example is used to deploy in multiple nodes and configure the microservice download url and other roles variables. 
For example, it can be used to deploy the microservice on the IDR omeroreadonly servers. The variable values inside the playbook should be modified for the IDR environment in which the microservice will be deployed.

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
          # URL pointing to the micro service omero-ms-region-download
          # It is important to have a version of the micro service using a version of Bio-Formats and OMEZarrReader that
          # match the versions running on the server
          omero_ms_image_region_download_URL: 'https://github.com/ome/omero-ms-image-region/releases/download/2024.07.15/omero-ms-image-region-0.10.0_b16.zip' 
          # sha256 for the Latest build
          omero_ms_image_region_package_sha256: 77bd3df2241c2beb439001fb00bfd8b207a06de63b8ee78c7170916d6dde963e


Author Information
------------------

ome-devel@lists.openmicroscopy.org.uk
