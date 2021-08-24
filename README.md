ansible-role-oracleinstaclient
==============================

Install oracle instant client base package and sqlplus

Requirements
------------

None.

Role Variables
--------------

Make sure to update all these values when updateing packages.

```yaml
# ldpath variable, do not forget to update when changing versions!
oic_pkg_version: "19.8"
oic_ld_library_path: "/usr/lib/oracle/{{ oic_pkg_version }}/client64/lib"
oic_package_base_url: "https://download.oracle.com/otn_software/linux/instantclient/19800"
oic_package_dest: "/tmp"

# oracle instant client database connection parameters
oic_databases:
   - sid: TEST
     host: testdb.mydbserver.com
     port: 2322
     service_name: TEST

# oic packages
oic_install_packages:
 - { pkg_name: "oracle-instantclient19.8-basic-19.8.0.0.0-1.x86_64.rpm", pkg_hash: "sha256:c42159e5466c661cc85d7a4d062e98aa06dc84251eea9de10ba2ddf2a7ea37cd" }
 - { pkg_name: "oracle-instantclient19.8-sqlplus-19.8.0.0.0-1.x86_64.rpm", pkg_hash: "sha256:436f74965d27894ce67242d6d155c41e3a561e959bf2ce8ba027931a29d63700" }

```

Dependencies
------------

None.

Example Playbook
----------------

```yaml
---

- name: oracle instant client test play
  hosts: all
  become: true
  vars:
    oic_install_packages:
     - { pkg_name: "oracle-instantclient19.8-basic-19.8.0.0.0-1.x86_64.rpm", pkg_hash: "sha256:c42159e5466c661cc85d7a4d062e98aa06dc84251eea9de10ba2ddf2a7ea37cd" }
     - { pkg_name: "oracle-instantclient19.8-sqlplus-19.8.0.0.0-1.x86_64.rpm", pkg_hash: "sha256:436f74965d27894ce67242d6d155c41e3a561e959bf2ce8ba027931a29d63700" }
    oic_databases:
       - sid: TEST
         host: testdb.mydbserver.com
         port: 2322
         service_name: TEST
  roles:
    - oracle_instant_client
```

License
-------

GPLv3

Author Information
------------------

Aaron (aaron@0x29a.ch)
