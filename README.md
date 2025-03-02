Ansible role: Dovecotsasl
=========

An Ansible role that sets up SASL authentication for Postfix using Dovecot on Debian/Ubuntu. Supports PLAIN and LOGIN mechanisms.

Requirements
------------

Postfix needs to be installed and configured. When using SASL authentication you want to allow external clients, so make sure you have:
- `inet_interfaces = all` or set to include specific external interfaces,
- `permit_sasl_authenticated` included in `smtpd_relay_restrictions`.

You do not need to add any SASL related configuration to `main.cf`, this role will handle it.

The role does not touch firewall rules, make sure external clients can connect.

When using `dovecotsasl_group_restrict`, the role does not add or configure any user accounts, only configures the group.

Role Variables
--------------

Available variables are listed below, along with default values (see defaults/main.yml):
```yaml
dovecotsasl_group_restrict: true
dovecotsasl_smtp_group: smtp
```
If `dovecotsasl_group_restrict` is `true`, only users that are members of the `dovecotsasl_smtp_group` are able to login via SASL.
```yaml
dovecotsasl_postfix_config_enabled: true
```
Whether to actually enable SASL authentication by configuring Postfix to use Dovecot. If set to `false` you need to manage the Postfix configuration yourself. If `true`, make sure subsequent roles/tasks/etc. do not overwrite `main.cf`. If they do, the configuration managed by this role will be lost.
```yaml
dovecotsasl_service_state: started
dovecotsasl_service_enabled: true
```
The state in which the Dovecot service should be after this role runs, and whether to enable the service on startup.


Dependencies
------------

None.

Example Playbook
----------------

```yaml
- hosts: all
  roles:
    - klemens-st.dovecotsasl
```

License
-------

MIT

Author Information
------------------

This role was created in 2025 by Klemens Starybrat.
