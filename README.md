# ServerDensity Role for Ansible

This role installs the [ServerDensity][serverdensity] agent and restarts the ServerDensity agent service as required.
It also make use of ServerDensity API to set ServerDensity System attributes.

------------

## Requirements

[cURL][curl] and NTP should be installed as prerequisites.

------------
## Role Variables

#### [`serverdensity_agent_service`][serverdensity-agent-service]
Default: `sd-agent`

ServerDensity service name.

#### [`serverdensity_agent_conf`][serverdensity-agent-conf]
Default: `/etc/sd-agent/config.cfg`

Path to check if ServerDensity is installed.

#### [`serverdensity_agent_install_url`][serverdensity-agent-install-url]
Default: `https://archive.serverdensity.com/agent-install.sh`

URL to the ServerDensity Agent install script that uses precompiled packages.

#### [`serverdensity_agent_install_url_source`][serverdensity-agent-install-url-source]
Default: `https://archive.serverdensity.com/agent-install-source.sh`

URL to the ServerDensity Agent install script that will compile the agent from source.

#### [`serverdensity_agent_install_script`][serverdensity-agent-install-script]
Default: `/tmp/agent-install.sh`

Path to destination file for the Agent Install script that will be downloaded.

#### [`serverdensity_agent_install_from_source`][serverdensity-agent-install-from-source]
Default: `no`

Whether or not to install ServerDensity Agent from source (instead of precompiled packages)

#### [`serverdensity_account_name`][serverdensity-account-name]
Default: `"{{ enc_serverdensity_account_name }}"`

ServerDensity account name without URL (e.g. abc not abc.serverdensity.io)"

To be stored in an Ansible Vault. It's very high-sensitivity Information.

#### [`serverdensity_api_token`][serverdensity-api-token]
Default: `"{{ enc_serverdensity_api_token }}"`

The API token as shown in the ServerDensity's Security Settings.
To be retrieved from ServerDensity portal by a SD admin account

To be stored in an Ansible Vault. It's very high-sensitivity Information.

#### [`serverdensity_api_url`][serverdensity-api-url]
Default: `https://api.serverdensity.io`

The API URL.

#### [`serverdensity_x_connect_url`][serverdensity-x-connect-url]
Default: `"{{ serverdensity_agent_install_url }}"`

URL for the install script. Could swap to `"{{ serverdensity_agent_install_url_source }}"` or a custom url.

#### [`serverdensity_group`][serverdensity-group]
Default: `Ansible`

Optional: Group to add the new device into

#### [`serverdensity_tag`][serverdensity-tag]
Default: `ansible`

Optional: Tag this device - multiple tags not supported." (it's a limit of SD installation script)

#### [`serverdensity_hosting_provider`][serverdensity-hosting-provider]
Default: `unknown`

Optional: Provider ID (requires provider). Cloud device ID (instance ID for EC2 devices)"

#### [`serverdensity_force_install`][serverdensity-force-install]
Default: `no`

Used to determine whether or not to force installation of the client if it has been previously installed.

#### [`serverdensity_use_sudo`][serverdensity-use-sudo]
Default: `no`

Whether or not to use sudo during installation.


------------
## Example Playbook

```YAML
---
- hosts: production
  roles:
     - { role: inviqa.serverdensity, serverdensity_api_token: 'abcdef012234343' }
  vars:
    serverdensity_group: 'Inviqa'
    serverdensity_tag: "inviqa"
    serverdensity_hosting_provider: "DO"
    serverdensity_use_sudo: yes
    serverdensity_force_install: yes
    serverdensity_agent_install_from_source: no
...
```

------------
## License

[MIT][licence]

------------
## Author Information

Author Marco Massari Calderone at Inviqa UK Ltd

[github]: https://github.com/inviqa/ansible-serverdensity "Github location of this role"
[curl]: https://galaxy.ansible.com/list#/roles/4384
[serverdensity]: https://serverdensity.com "ServerDensity website"

[serverdensity-agent-service]: https://github.com/inviqa/ansible-serverdensity/blob/master/defaults/main.yml#L2 "Link to variable on master"
[serverdensity-agent-conf]: https://github.com/inviqa/ansible-serverdensity/blob/master/defaults/main.yml#L3 "Link to variable on master"
[serverdensity-agent-install-url]: https://github.com/inviqa/ansible-serverdensity/blob/master/defaults/main.yml#L4 "Link to variable on master"
[serverdensity-agent-install-url-source]: https://github.com/inviqa/ansible-serverdensity/blob/master/defaults/main.yml#L5 "Link to variable on master"
[serverdensity-agent-install-script]: https://github.com/inviqa/ansible-serverdensity/blob/master/defaults/main.yml#L6 "Link to variable on master"
[serverdensity-agent-install-from-source]: https://github.com/inviqa/ansible-serverdensity/blob/master/defaults/main.yml#L7 "Link to variable on master"
[serverdensity-account-name]: https://github.com/inviqa/ansible-serverdensity/blob/master/defaults/main.yml#L8 "Link to variable on master"
[serverdensity-api-token]: https://github.com/inviqa/ansible-serverdensity/blob/master/defaults/main.yml#L9 "Link to variable on master"
[serverdensity-api-url]: https://github.com/inviqa/ansible-serverdensity/blob/master/defaults/main.yml#L10 "Link to variable on master"
[serverdensity-x-connect-url]: https://github.com/inviqa/ansible-serverdensity/blob/master/defaults/main.yml#L11 "Link to variable on master"
[serverdensity-group]: https://github.com/inviqa/ansible-serverdensity/blob/master/defaults/main.yml#L12 "Link to variable on master"
[serverdensity-tag]: https://github.com/inviqa/ansible-serverdensity/blob/master/defaults/main.yml#L13 "Link to variable on master"
[serverdensity-hosting-provider]: https://github.com/inviqa/ansible-serverdensity/blob/master/defaults/main.yml#L14 "Link to variable on master"
[serverdensity-force-install]: https://github.com/inviqa/ansible-serverdensity/blob/master/defaults/main.yml#L15 "Link to variable on master"
[serverdensity-use-sudo]: https://github.com/inviqa/ansible-serverdensity/blob/master/defaults/main.yml#L16 "Link to variable on master"

[licence]: https://raw.githubusercontent.com/inviqa/ansible-serverdensity/master/LICENSE
