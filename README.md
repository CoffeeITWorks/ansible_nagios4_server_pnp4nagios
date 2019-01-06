nagios_server_pnp4nagios
=========

It installs pnp4nagios graphs, also configures emails to generic services and generic_host to send emails with pnp4n perl script by Frank Migge.

Requirements
------------



Role Distribution support
------------------------

Ubuntu: ok
Debian: ok
RedHat: No

Role Variables
--------------

Add to your host_vars or group_vars:

    nagios_server_pnp4n_smpt_domain: 'yourdomain.com'
    nagios_server_pnp4n_email_customer: 'COMPANY, Address'

Dependencies
------------

ansiblecoffee.nagios_server

Example Playbook
----------------

Minimum usage:

    - hosts: servers
      roles:
        - ANXS.mysql
        - nagios_server
        - nagios_server_pnp4nagios

### Full list of roles:

See [requirements.yml](requirements.yml) for some example on names of the roles.

Most of them could be `coffeeitworks.name` instead of just name, but the example is with names simplified.

``` yaml
- name: apply Nagios settings
  hosts: nagios4_servers
  become: yes
  become_method: sudo
  roles:
    - { role: nagios4_server, tags: ["install", "nagios4_server_all", "nagios4_server"] }
    - { role: nagios4_server_plugins, tags: ["install", "nagios4_server_all", "nagios4_server_plugins"] }
    - { role: nagios4_server_pnp4nagios, tags: ["install", "nagios4_server_all", "nagios4_server_pnp4nagios"] }
    - { role: nagios4_server_snmptrap, tags: ["install", "nagios4_server_all", "nagios4_server_snmptrap"] }
    - { role: ANXS.mysql, tags: ["install", "nagios4_server_all", "nagios4_server_thruk", "ANXS.mysql"] }
    - { role: nagios4_server_thruk, tags: ["install", "nagios4_server_all", "nagios4_server_thruk"] }
    - { role: postfix_client, tags: ["install", "nagios4_server_all", "postfix_client"] }
# Additional tags: role/tag
# nagios4_server             - config_nagios
# nagios4_server             - nagios4_server_main_config
# nagios4_server             - config_nagios_cron
# nagios4_server_plugins     - config_nagios_plugins
# nagios4_server_plugins     - test_nagios_plugins
# nagios4_server_pnp4nagios  - test_nagios_pnp4nagios
# nagios4_server_thruk       - config_nagios_thruk_cron
# nagios4_server_thruk       - test_nagios_thruk
# nagios4_server_thruk_git   - config_nagios_thruk_git_cron
```


### Tags

    test_nagios_pnp4nagios

License
-------

BSD

Troubleshooting
---------------

Something similar to this could happen in some graphs:
https://support.nagios.com/forum/viewtopic.php?f=7&t=46528

You can delete the .rrd file for each graph you have problems or you can delete last 200 found in log, like:

```
tail -n 200 /usr/local/pnp4nagios/var/perfdata.log  | grep "update ERROR" | while read line ; do echo "$line" | cut -d" " -f 7 | tr -d ":" | xargs rm;  done
```

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).

Mora information
----------------

http://nagios.fm4dd.com/howto/manual/pnp4n_send_service_mail.htm


