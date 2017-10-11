# Ansible Nginx ACME Protocol Configuration

This is a very simple Ansible role that installs an Nginx configuration
snippet to enable the ACME protocol for any virtual host.

## Requirements

This role should work with any GNU/Linux system running Nginx.

## Role Variables

Variables used by this role are listed below, along with their default values.

    nginx_acme_root_directory: "/var/lib/acme-challenges"

The directory from which ACME challenges will be served by Nginx. This
directory should be writable by the user running `certbot` (or other ACME
tool) and should be readable by the Nginx server.

    nginx_acme_challenge_user: "root"

User account that will need to write ACME challenges in the above directory.

    nginx_acme_challenge_group: "www-data"

Group that should have read permissions on the ACME challenges written in the
above directory.

    nginx_snippet_path: "/etc/nginx/snippets"

Directory containing Nginx configuration snippet files that can be included by
virtual hosts.

    nginx_acme_snippet: "{{ nginx_snippet_path }}/nginx-acme-challenge.conf"

The file name of the Nginx configuration snippet file created by this role.
This can be substituted into a virtual host configuration created by a
subsequent role or task that depends on this role.

## Dependencies

This role doesn't depend on any others, but I recommend
[geerlingguy.nginx](https://github.com/geerlingguy/ansible-role-nginx) as a
base for installing Nginx.

## Installation

Install this role from Ansible Galaxy with

    ansible-galaxy install mtmiller.nginx-acme-snippet

## Example Playbook

This is an example playbook showing how to use this role.

    - hosts: servers
      roles:
        - mtmiller.nginx-acme-snippet

## License

This role is licensed under the [MIT](https://opensource.org/licenses/MIT)
license. See [LICENSE.md](LICENSE.md) for the full license text.
