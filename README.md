dudefellah.iac
=========

This is a generic install-and-configure (iac) role. It will install some
package for your distribution, install some files based on text that
you provide and optionally perform a service reload/restart based on
the changed configuration files.

This probably isn't the type of role that's to everybody's taste, but I
think it'll be useful for the myriad of simple software installs that I
do that probably don't warrant a full role to be defined to manage them.

Requirements
------------

None.

Role Variables
--------------

Role variables are defined with comments in
[defaults/main.yml](defaults/main.yml).

Dependencies
------------

None

Example Playbook
----------------

If you wanted to install and configure vdirsyncer for a particular user (note
that this playbook is untested, but should give an idea on how it works):

    - hosts: all
      tasks:
        - name: Intall and configure vdirsyncer
          include_role:
            name: dudefellah.iac
          vars:
            iac_user: dan
            iac_group: dan
            iac_packages:
              - vdirsyncer
            iac_config_files:
              - path: .config/vdirsyncer/config
                content: |
                    [general]
                    status_path = "~/.vdirsyncer/status"

                    ... 
            iac_template_validator: "valdini %s"
            iac_reload_service: null
            iac_reload_command: vdirsyncer sync

License
-------

GPLv2+

Author Information
------------------

Dan - github.com/dudefellah
