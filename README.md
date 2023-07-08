# gitea

This role sets up a [Gitea](https://gitea.io/en-us/) server using its docker image.

This only takes care of setting up the service, its configuration is done through the web interface the first time the service runs.

## Requirements

This role relies on `docker` being available on the host and the [`docker_container` ansible module](https://docs.ansible.com/ansible/latest/modules/docker_container_module.html) in ansible.

To cover the first one, the [`geerlingguy.docker` role](https://galaxy.ansible.com/geerlingguy/docker) can be used.

To cover the dependencies for the `docker_container` module the [`geerlingguy.pip` role](https://galaxy.ansible.com/geerlingguy/pip) can be used to install Python's [`docker` package](https://pypi.org/project/docker/).

As with any git server, using SSH is recommended for accessing the repos thus a port will need to be forwarded to the SSH port of the container. This doesn't have to be the standard SSH port.

Also, gitea provides a web interface so access to it should be provided. It is recommended that a reverse proxy such as nginx is used for that purpose.

## Role Variables

 - **`gitea__version`** (optional, default: _1.19.4_): Image version tag to use.
 - **`gitea__container_name`** (optional, default: _gitea-server_): Name to use for the container created by the role.
 - **`gitea__data_dir`** (optional, default _/var/gitea/_): Folder to use for storing the persistent files.
 - **`gitea__ssh_port`** (optional, default: _2222_): Port where the container will publish the gitea's SSH port.
 - **`gitea__web_host`** (optional, default: _127.0.0.1_): Address where the container will publish gitea's web socket.
 - **`gitea__web_port`** (optional, default: _3000_): Port where the container will publish the gitea's web port.
 - **`gitea__hostname`** (optional, default: _localhost_): Domain name to use for the displayed http clone URL in the UI.
 - **`gitea__root_url`** (optional, default: _http://localhost:3000/_): Base URL to use for _all_ internal links. Use the actual URL that will be used to access the service. E.g. _https://git.example.com/_
 - **`gitea__enable_lfs`** (optional, default: _no_): Enabled git-lfs support.
 - **`gitea__app_name`** (optional): Application name, used in the page title.

## Example Playbook

The following would be a fairly common role usage example:

```yaml
- host: git.my-domain.com
  roles:
    - role: salessandri.gitea
    - vars:
        gitea__hostname: git.my-domain.com
        gitea__root_url: https://git.my-domain.com/
```

## License

MIT

## Author Information

This role was created in 2020 by [Santiago Alessandri](https://rambling-ideas.salessandri.name).
