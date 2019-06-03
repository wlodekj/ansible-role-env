# env

[![Build Status](https://travis-ci.com/iroquoisorg/ansible-role-env.svg?branch=master)](https://travis-ci.com/iroquoisorg/ansible-role-env)

Ansible role for env

This role was prepared and tested for Ubuntu 16.04.

# Installation

`$ ansible-galaxy install iroquoisorg.env`

# Usage

## Environment variables

To set global environment variables, use `env_vars` variable in a following way:

```
env_vars:
    VARIABLE: 'value'
    OTHER_VARIABLE: 'some_value'
```

This role will update variables' value if necessary.

## Pam environment variables - .pam_environment

In case you want to narrow down visibility of your environment variables to only one user (for example: www-data) and not 
expose them to everyone use env_pam_* options to set it. Read more: https://help.ubuntu.com/community/EnvironmentVariables#A.2BAH4-.2F.pam_environment

```
env_pam_path: "/var/www" # check $HOME directory for www-data user
env_pam_module_arguments: "readenv=1 user_readenv=1" 
env_pam_owner: "www-data"
env_pam_vars: {
    - { regexp: '^TEST=', line: 'TEST=new_test_variable' }
}
```

To test pam env vars:

```
sudo -i -u www-data printenv
```

# Default settings

```
---
env_hostname: ""
env_vars: {}
env_timezone: "Etc/UTC"
env_cron_jobs: []  # {job: "git status", name: "job name", user: "www-data", minute: "*", hour: "*", day: "*", weekday: "*", month: "*" }
env_hosts: []  # {ip: "127.0.0.1", host: "localhost"}
env_cron_host: false
env_pam_path: "" # example: "/var/www"
env_pam_module_arguments: "readenv=1 user_readenv=0" # user_readenv to read user ~/.pam_environment files, more: https://help.ubuntu.com/community/EnvironmentVariables#A.2BAH4-.2F.pam_environment
env_pam_owner: "www-data"
env_pam_vars: {}

```

# Development

Please check [development guide](DEVELOPMENT.md) for details about developing and testing this role.
