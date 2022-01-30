Ansible role: openssh
=========

![main Build status](https://github.com/Provizanta/ansible-role-microk8s/actions/workflows/main.yml/badge.svg)

Install and configure an OpenSSH server.

Highly inspired by:
- https://github.com/robertdebock/ansible-role-openssh

Requirements
------------

None

Role Variables
--------------

These variables are defined in [defaults/main.yml](./defaults/main.yml):

    openssh_configuration: {}

    openssh_configuration_match_blocks: {}

`Include: /etc/ssh/sshd_config.d/*.conf` will always be added to the configuration if the OpenSSH server supports it (> 8.2).

Dependencies
------------

None

Example Playbook
----------------

    - name: Converge
      hosts: all
      roles:
        - role: ansible-role-openssh
          vars:
            openssh_configuration:
              ## Configuration
              Port: 22
              ListenAddress:
                - "0.0.0.0"
                - "::"
              AcceptEnv:
                - LANG
                - LANGUAGE
                - LC_*
              PrintMotd: no
              Subsystem: sftp  /usr/lib/openssh/sftp-server
              UsePAM: yes
              ## Ciphers
              Ciphers: aes128-ctr,aes192-ctr,aes256-ctr
              HostKeyAlgorithms: ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,ssh-rsa,ssh-dss
              KexAlgorithms: ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group14-sha1,diffie-hellman-group-exchange-sha256
              MACs: hmac-sha2-256,hmac-sha2-512,hmac-sha1
              ## Security
              # Protocol: 2
              PasswordAuthentication: no
              PermitRootLogin: no
              PermitEmptyPasswords: no
              AllowTcpForwarding: no
              AllowStreamLocalForwarding: no
              GatewayPorts: no
              PermitTunnel: no
              ChallengeResponseAuthentication: no
              ClientAliveInterval: 180
              MaxAuthTries: 5
              X11Forwarding: no
            openssh_configuration_match_blocks:
              Address 192.168.1.*:
                PasswordAuthentication: "yes"
                PermitRootLogin: "yes"

License
-------

MIT

Author Information
------------------

Tibor Csóka
