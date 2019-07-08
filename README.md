Ansible Role: og-oec
=========

Installs and configures the Opsgenie Edge Connector on RedHat/Centos & Debian/Ubuntu servers.

This role installs and configures the latest version of OEC from the OpsGenie AWS S3 Bucket, (on RedHat-based systems) or apt (on Debian-based systems). You will likely need to do extra setup work after this role has installed OEC, like adding your own scripts that are referenced in your oec config file.

Official Atlassian documentation on OEC can be found here.

https://docs.opsgenie.com/docs/oec-overview

Note.
This can be used with the oec-runner role to integrate Ansible Runner with OEC.

Requirements
------------

None.

Role Variables
--------------
Available variables are listed below, along with default values (see defaults/main.yml):

### MINIMUM REQUIRED TO RUN ###
conf_apiKey: < Your Opsgenie Integration API Key > 
conf_actions:
  - name: <Action Name>
    sourceType: local
    filepath: <Path to your script>
OR IF USING GIT
conf_apiKey: < Your Opsgenie Integration API Key > 
conf_actions:
  - name: <Action Name>
    sourceType: git
    filepath: <Path to your script>
    giturl: https://github.com/repo/name.git
    gitprvkey: Git Private Key
    gitpassphrase: Git Pass Phrase
    
### OEC Service Variables ###

oec_conf_source_type: local
oec_conf_local_filepath: /etc/opsgenie/
oec_conf_template: oecconfig.yml.j2
oec_conf_file_path: /etc/opsgenie/
oec_conf_file: oecconfig.yml
__oec_user: opsgenie
oec_group: opsgenie
__oec_svc_name: oec
oec_svc_path: /etc/systemd/system/
oec_svc_template: svc.j2
oec_svc_env_template: svc_env.j2
oec_svc_env_file: oec.env

### Global Config Variables ###

conf_appName: OEC
conf_baseUrl: https://api.opsgenie.com
conf_logLevel: info
conf_poller_wait: 100
conf_poller_Timeout: 30
conf_poller_maxmsgs: 10
conf_pool_max_workers: 12
conf_pool_min_workers: 4
conf_pool_queueSize: 0
conf_pool_keepalive: 6000
conf_pool_monitoring_period: 15000
conf_globalArgs:
  args:
    - arg1
    - arg2
conf_globalFlag:
  flags:
    - key: key1
      value: value1
    - key: key2
      value: value2
conf_globalEnv:
  env:
    - key: key1
      value: value1
    - key: key2
      value: value2

### Action Mapping Variables ###
conf_actions:
  - name: <Action Name>
    sourceType: local
    filepath: <Path to your script>
    args:
      - arg1
      - arg2
    flags:
      - key: key1
        value: value1
      - key: key2
        value: value2
    env:
      - key: key1
        value: value1
      - key: key2
        value: value2
    stdout: '/var/log/customaction.log'
    stderr: '/var/log/customaction_err.log'
    
### Custom Action from Git Source ###
conf_actions:
  - name: <Action Name>
    sourceType: git
    filepath: <Path to your script>
    giturl: https://github.com/repo/name.git
    gitprvkey: Git Private Key
    gitpassphrase: Git Pass Phrase
    args:
      - arg1 
      - arg2
    flags:
      - key: key1
        value: value1
      - key: key2
        value: value2
    env:
      - key: key1
        value: value1
      - key: key2
        value: value2
    stdout: '/var/log/customaction.log'
    stderr: '/var/log/customaction_err.log'
    
Dependencies
------------

None.

Example Playbook
----------------

    - hosts: server
      roles:
         - { role: phil_avery.og_oec }


License
-------

MIT / BSD

Author Information
------------------

This role was created in 2019 by Phil Avery.
