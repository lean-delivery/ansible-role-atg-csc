atg_csc
=========
[![License](https://img.shields.io/badge/license-Apache-green.svg?style=flat)](https://raw.githubusercontent.com/lean-delivery/ansible-role-atg-csc/master/LICENSE)
[![Build Status](https://travis-ci.org/lean-delivery/ansible-role-atg-csc.svg?branch=master)](https://travis-ci.org/lean-delivery/ansible-role-atg-csc)
[![Build Status](https://gitlab.com/lean-delivery/ansible-role-atg-csc/badges/master/build.svg)](https://gitlab.com/lean-delivery/ansible-role-atg-csc)

## Summary
--------------

This role installs Oracle ATG Commerce Service Center.   

ATG Commerce Service Center is a customizable and deployable customer service application that enables an agent to perform the following tasks for an ATG Commerce site:   

- Create and manage customer profiles
- Create and manage orders
- Issue refunds and exchanges
- Process returned items
- Research customer activity


Requirements
--------------

 - Minimal Version of the ansible for installation: 2.5
 - **Supported CSC versions**:
   - 10.x
   - 11.0
   - 11.1
   - 11.2
   - 11.3
   - _lower and higher versions should be retested_
 - **Supported OS**:
   - CentOS
     - 6
     - 7

For more information regarding support matrix please visit <https://support.oracle.com>

ATG platform should be installed preliminarily:
  - lean_delivery.atg_platform


Check if installed next packages on target system:
  - sudo


```
For test scenarios atg-csc/requirements.yml is used  
If another roles/versions are required, put requirements.yml to molecule/<scenario_name> and remove in molecule.yml lines  
  options:  
    role-file: requirements.yml
```


Role Variables
--------------

  - `csc_version` - Commerce Service Center version
  - `transport` - artifact source transport  
     Available:
      - `web` - fetch artifact from custom web uri
      - `local` - local artifact

  - `transport_web` - URI for http/https artifact  e.g. "http://my-storage.example.com/V861213-01.zip"
  - `transport_local` - path for local artifact e.g. "/tmp/V861213-01.zip"

  - `download_path` - local folder for downloading artifacts  
    default: `/tmp`

  - `dynamo_root` - path to installed ATG Platform  
    default: `/opt/atg/ATG`

  - `es_host` - ATG Search host (when using ATG Search as Search Engine)


Example Playbook
----------------

### Installing ATG Commerce Service Center 11.3 from local:
```yaml
- name: "Install CSC 11.3 from local"
  hosts: all

  roles:
    - role: lean_delivery.java
      java_major_version: 7
      java_minor_version: 80
      transport: "local"
      transport_local: "/tmp/jdk-7u80-linux-x64.tar.gz"
    - role: lean_delivery.jboss
      transport: "local"
      transport_local: "/tmp/jboss-eap-6.1.0.zip"
    - role: lean_delivery.atg_platform
      transport: "local"
      transport_local: "/tmp/V861209-01.zip"
    - role: lean_delivery.atg_csc
      csc_version: "11.3"
      transport: "local"
      transport_local: "/tmp/V861213-01.zip"


  vars:
    atg_version: "11.3"
    dynamo_root: "/opt/atg/ATG{{ atg_version }}"

```

### Installing ATG Commerce Service Center 10.2 from local:
```yaml
- name: "Install CSC 10.2 from local"
  hosts: all

  roles:
    - role: lean_delivery.java
      java_major_version: 6
      java_minor_version: 45
      transport: "local"
      transport_local: "/tmp/jdk-6u45-linux-x64.tar.gz"
    - role: lean_delivery.jboss
      transport: "local"
      transport_local: "/tmp/jboss-eap-6.1.0.zip"
    - role: lean_delivery.atg_platform
      transport: "local"
      transport_local: "/tmp/ATG10.2.zip"
    - role: lean_delivery.atg_csc
      csc_version: "10.2"
      transport: "local"
      transport_local: "/tmp/V37728-01.zip"
      es_host: "search-host.example.com"


  vars:
    atg_version: "10.2"
    dynamo_root: "/opt/atg/ATG{{ atg_version }}"

```


## License

Apache2

## Authors

  - Lean Delivery team  
    <team@lean-delivery.com>
