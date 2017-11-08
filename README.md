# private-repos

## What?

Deploys configs for centralized private PyPI, RPM, Docker, etc. repos. Think [Artifactory](https://www.jfrog.com/artifactory/).

## How?

RPM and pip configs are laid down for *all users*, so they assume `sudo` permissions and write files as root. Docker logins *must be run as the target user* though. _*TL;DR: Remote in as yourself, don't use sudo locally.*_

Set the vars below to match your installation. Details on getting your encrypted password are further along. _Remember:_ Whatever password you give this playbook is going to be written in plaintext on the filesystem, eg: `~/.pip/pip.conf` 

```yaml
private_repo_username: 'jtest'
private_repo_password: 'mootoo'
private_repo_encrypted_password: 'abc123' # req'd for rpm repos only

# as in {{proto}}://{{base}}/{{prefix}}/...
private_repo_url_proto: 'https'
private_repo_url_base: 'artifactory.default.com'
private_repo_url_pathprefix: 'artifactory'
```

Set these to the repo names in Artifactory. This is the name that appears in repo URLs. eg: `centos-local`, `someteam-docker`, etc.
```yaml
private_repo_rpm_repos: []
private_repo_pypi_repos: []
private_repo_docker_repos: []
```

### Getting encrypted password for RPM from Artifactory

1. Head to https://artifactory.domain.com/artifactory/webapp/#/profile
2. Re-enter your password and click *Unlock*.
3. Find *Authentication Settings* and its field *Encrypted Password*
4. Note the password down somewhere.
