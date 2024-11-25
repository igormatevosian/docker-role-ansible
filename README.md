# Docker Role

An Ansible role to install and configure Docker on Debian-based systems.

## Requirements

- The target system must be Debian-based (e.g., Ubuntu).
- Ansible must be installed on the control node.
- Internet access is required on the target system to add the Docker repository and download packages.

## Role Variables

The following variables can be customized to configure the role:

- `docker_repo_url`: The base URL for the official Docker GPG key.
  - Default: `https://download.docker.com/linux/debian`
- `docker_repo`: The APT repository for Docker.
  - Default: `"deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"`
- `docker_packages`: A list of Docker-related packages to install.
  - Default: 
    ```yaml
    docker_packages:
      - docker-ce
      - docker-ce-cli
      - containerd.io
    ```

## Dependencies

This role has no external dependencies.

## Example Playbook

Below is an example of how to use the role in your playbook:

```yaml
- name: Install and configure Docker
  hosts: servers
  become: true
  vars:
    docker_repo_url: "https://download.docker.com/linux/ubuntu"
    docker_repo: "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    docker_packages:
      - docker-ce
      - docker-ce-cli
      - containerd.io
  roles:
    - docker
```

## Tasks

This role performs the following tasks:

1. Installs required APT packages for Docker.
2. Adds Docker's official GPG key.
3. Adds Docker's APT repository.
4. Installs Docker packages.
5. Ensures the Docker service is running and enabled at startup.