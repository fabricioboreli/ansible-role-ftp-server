FTP Server
==========
This ansible role install vsFTPd server and configure it so users will be "chrooted". Their root directory will be their home directory on the server.  

Requirements
------------
Debian 8 or 9

Role Variables
--------------
Server banner:
```yaml
ftp_server_banner: "Welcome to vsFTPd Server"
```
Username:
```yaml
name: alice
```

State of the login. Should the user be _present_ or _absent_?
```yaml
state: present
```

Login Description:
```yaml
comment: "Alice's FTP login"
```

The password hash can be generated using the following command: `mkpasswd --method=sha-512`
```yaml
password: "$6$mZk4Sswk.i$MRCX2UiXUDwtCvNNeSpDpTdMxUTRoNtYjo7t0cNMPyUZ5PAF4nHAGSoVUkn65lMJTSYTMDZWSmC7a0KVCMHph/"
```

Dependencies
------------
None.

Example Playbook
----------------
```yaml
---
- name: Install and configure vsFTPd Server
  hosts: ftp-server
  become: true
  gather_facts: true
          
  roles:
    - role: fabricioboreli.ansible-role-ftp-server
      ftp_server_banner: "Welcome to vsFTPd server"
      users:
        - name: alice
          state: present
          comment: "Alice's FTP user"
          password: "$6$mZk4Sswk.i$MRCX2UiXUDwtCvNNeSpDpTdMxUTRoNtYjo7t0cNMPyUZ5PAF4nHAGSoVUkn65lMJTSYTMDZWSmC7a0KVCMHph/"

        - name: joanna
          state: present
          comment: "Joanna's FTP user"
          password: "$6$mZk4Sswk.i$MRCX2UiXUDwtCvNNeSpDpTdMxUTRoNtYjo7t0cNMPyUZ5PAF4nHAGSoVUkn65lMJTSYTMDZWSmC7a0KVCMHph/"
```

License
-------
MIT

Author Information
------------------
Fabricio Boreli Ferreira  
fabricioboreli at openmailbox dot org
