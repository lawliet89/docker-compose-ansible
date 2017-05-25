docker-compose-ansible
=========

Ansible role to deploy applications via `docker-compose`.

Requirements
------------

The target host should have `docker`, `docker-compose` and the python library `docker-py` installed.

Role Variables
--------------

 - `code_source`: 'local' or `git`. Set to `local` to get source code from the host machine, or `git` from a git
 repository.
 - `git_repo`: URL for a git repository.
 - `get_local_commit`: If `code_source` is set to `git` and this is set to `true`, will get a commit from the local
 directory instead of using a branch.
 - `git_repo_version`: If `code_source` is set to `git`, specify a commit or branch name to deploy
 - `docker_compose_files`: An array of `docker-compose` files to use to deploy
 - `local_path`: if `code_source` is `local` or if `get_local_commit` is true, the path to the local source code.
 - `project_directory`: The path on the target host to deploy source code to.
 - `remove_volumes`: Set to `yes` to remove existing volumes while deploying. Defaults to `no`.
 - `pull_images`: Set to `True` to pull images from a registry before creating the containers. Defaults to `True`.
 - `build_images`: Set to `True` to build images for containers. Defaults to `True`.
 - `docker_become`: This is a dictionary with the following keys: `become`, `become_user`, `become_method`, and
 `become_flags`, with their usual [meaning](https://docs.ansible.com/ansible/become.html) in Ansible. Use this
 to set if `become` is needed for Docker commands.


Example Playbook
----------------

```yml
---
- name: "Deploy Application"
  hosts: all
  roles:
    - role: docker_compose_deploy
      code_source: 'local'
      project_directory: "/home/{{ ansible_user_id }}/app"
      local_path: "{{ playbook_dir }}/app"

```

License
-------

LGPL

TODO
-------

Write tests
