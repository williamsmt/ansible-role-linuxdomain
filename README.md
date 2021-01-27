# ansible-role-linuxdomain
=========

A purpose-built role used to install and configure dependencies required for joining a linux host to an Active Directory domain. Generally, this role installs and configures sssd, realmd and krb5. Local and remote access is reconfigured to support domain authentication, and a domain join operation performed. The intent of this role is to primarily be run once a workload is being deployed for production.

Requirements
------------

N/A

Role Variables
--------------

| Variable                  | Required | Default            | Choices                                     | Comments                                                       |
|---------------------------|----------|--------------------|---------------------------------------------|----------------------------------------------------------------|
| packages_use_role_default | yes      | false              | true,false                                  |                                                                |
| packages_default          | yes      | null               | list of packages                            |                                                                |
| ssh_use_role_default      | yes      | false              | true,false                                  |                                                                |
| ssh_default               | yes      | null               | array of line settings                      | generally accepted default ssh settings                        |
| domainfqdn                | yes      | null               | "example.com"                               | lowercase string fqdn of your domain                           |

Dependencies
------------

No dependent roles required. Many of the tasks are currently conditioned for Debian flavor support, but can be easily modified to support other linux distributions. Please submit a PR for any enhancements you choose to include in the role.

Sample requirements.yml file for custom playbook:

    roles:
      - src: https://github.com/williamsmt/amsible-role-linuxdomain.git
        version: main
        name: ansible-role-linuxdomain

To install this role using a requirements.yml file in the playbook directory:

`ansible-galaxy role install -r requirements.yml -p ./roles`

Example Playbook
----------------

Sample playbook passing common parameters for both image build (with Packer) and day 2 maintenance:

    - name: Build linux host
        hosts: all
        vars:
          domainfqdn: example.com

        roles:
          - ./roles/ansible-role-linuxdomain

Run the playbook as:

`ansible-playbook -i {ip_address_of_host_or_inventory_file} playbook.yml`

License
-------

Released under the [Apache-2.0 license](LICENSE)

Author Information
------------------

https://github.com/williamsmt

This is not an officially supported Google product