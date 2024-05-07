Ansible-sssd
=========

Yet another ansible SSSD role to deploy, configure and join a Linux machine to an Active Directory domain.  
Tested on Ubuntu 22.04


Requirements
------------

Ansible  
Active Directory

Role Variables
--------------


| Variable                | Required | Default | Choices                   | Comments                                 |
|-------------------------|----------|---------|---------------------------|------------------------------------------|
| sssd_pkgs               | no       | sssd-ad, sssd-tools, realmd, adcli, krb5-user   | list               | package to install                         |
| sssd_ad_domain                     | yes      | example.com        | string                | domain name for sssd conf                        |
| sssd_ad_realm                     | yes      | EXAMPLE.COM        | string                | domain name for kerberos REALM                         |
| sssd_ad_user                     | yes      |       | string                | AD username to join the domain                       |
| sssd_ad_password                     | yes      |        | string                | AD password of provided username to join the domain                        |
| sssd_ad_default_shell                     | yes      | /bin/bash        | string                | default shell for user login                        |
| sssd_ad_fallback_homedir                     | yes      | /home/%u        | string                | default location of user's home                        |
| sssd_ad_use_fully_qualified_names                     | yes      | True       | bool                | whether to use FQDN or not                        |
| sssd_dyndns_update                     | yes      | false       | bool                | DynDNS conf                        |
| sssd_ldap_ssh_key_attribute                     | yes      | altSecurityIdentities       | string                | AD Custom Attribute name for public key authentication                        |
| sssd_ad_sudo_group                     | no      | LDAP_GRP_FOR_SUDOERS       | string                | name of the AD Group to grant sudo permissions                        |
| sssd_ad_sudo_permissions                     | no      | ALL=(ALL:ALL) ALL       | string                | sudo configuration                        |
| sssd_ad_sudo_conf_d                     | no      | /etc/sudoers.d       | string                | location of sudoers conf to be deployed                        |

Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - name: Install and configure SSSD
      hosts: all
      gather_facts: true
      become: true
      roles:
        - sssd
      vars_prompt:
        - name: sssd_ad_user
          prompt: "AD user to join the domain"
          private: false

        - name: sssd_ad_password
          prompt: "Password of the AD user"
          private: true

License
-------

See license.md

Author Information
------------------

K4mote