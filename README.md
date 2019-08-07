ansible-dashboard-role
======================

This role deploy and configure the new Laniakea orchestrator Dashboard.

Requirements
------------

The Laniakea components **CMBD**, **SLAM**, **IAM**, **CPR** and **Orchestrator** must already been installed.

This ansible role support: **Ubuntu 16.04**
Minimum ansible version: **2.4**


Role Variables
--------------

### dashboard variables

- dashboard admin email
  ``dash_admin_email:`` admin@email.com

- dashboard HOSTNAME
 ``dash_fqdn:`` <dashboard_hostname>

- location configuration file
  ``dest_conf:`` /etc/orchestrator-dashboard

- Docker image
  ``dash_image:`` marica/orchestrator-dashboard:latest

- dashboard client id and secret needed for integration with IAM
  ``iam_client_id:`` <iam_client_id>
  ``iam_client_secret:`` <iam_client_secret>

- IAM url
  ``iam_base_url:`` <iam_url>

- orchestrator base url or proxy
  ``orchestrator_url:`` <orchestrator_url>

- tosca location path
  ``tosca_templates_dir:`` /opt/tosca-templates
  ``tosca_parameters_dir:`` /opt/tosca-parameters

- slam url
  ``slam_url:`` <slam_url>

- cmdb base url or proxy
  ``cmdb_url:`` <cmdb_base_url>
- mail server specification
  ``mail_server:``
  ``mail_port:``
  ``mail_sender:``
  ``admins:`` <admin_email>

- Tosca dashboard configuration
  ``tosca_dash_conf:`` https://github.com/Laniakea-elixir-it/laniakea-dashboard-config.git

### database variables

- bolean for db True (dashboard with database) False (dashboard without database)
  ``with_db:`` True

- database Docker image
  ``db_image:`` mysql:5.7

- database Docker ip 
  ``ip_db:`` <ip_db>

- database password
  ``db_password:`` password_db

Dependencies
------------

``role: indigo-dc.docker``


Example Playbook
----------------
    
    - name: Deploy dash
      hosts: dashboard
      become: yes
      gather_facts: false
      pre_tasks:
        - name: Check python is installed
          raw:  test -e /usr/bin/python || (apt -y update && apt install -y python-minimal)
          changed_when: false
        - name: Gathering Facts
          setup:
      vars:
        dash_admin_email: <admin_email>
        dash_fqdn: <dashboard_hostname>
        dash_image: marica/orchestrator-dashboard:latest
        iam_client_id: <iam_client_id>
        iam_client_secret: <iam_client_secret>
        iam_base_url: <iam_base_url>
        orchestrator_url: <orchestrator_url>
        slam_url: <slam_url>
        cmdb_url: <cmdb_base_url>
        admins: <admins>
      roles:
        - role: ansible-dashboard-role

I recommend, insted of inserting all vars in the playbook, to write them in a dash.yaml file in group_var directory
 
License
-------

Apache Licence v2

http://www.apache.org/licenses/LICENSE-2.0


Author Information
------------------

