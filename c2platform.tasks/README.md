
# Ansible Role C2 Platform Core Tasks

Ansible role for reusable tasks. Current implementation of [Ansible Collections](https://docs.ansible.com/ansible/latest/user_guide/collections_using.html) do not allow tasks to be reused between collections.

So in order to prevent code duplication and ordinary role is used for this purpose.

<!-- MarkdownTOC levels="2,3" autolink="true" -->

- [Requirements](#requirements)
- [Role Variables](#role-variables)
    - [PostgreSQL](#postgresql)
    - [Certificates](#certificates)
- [Dependencies](#dependencies)
- [Example Playbook](#example-playbook)

<!-- /MarkdownTOC -->

## Requirements

<!-- Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required. -->

## Role Variables

<!--  A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well. -->

### PostgreSQL

| File                  | Purpose |
|---------------------------|----|
| psql-terminate-block-sessions.yml | Block sessions to a PostgreSQL database |
| psql-database.yml | Manage a PostgreSQL database |
| psql-allow-sessions.yml | Allow sessions to a PostgreSQL database |

An example of this use can be found in __jira__ role e.g.

```yaml
- include_role:
    name: c2platform.tasks
    tasks_from: psql-database
  vars:
    lcm_role_upgrade: jira
  when: jira_database_type == 'postgresql'
```

### Certificates

Reusable tasks for CA server are in `cert.yml`. See the [cacerts](https://github.com/c2platform/ansible-collection-core/tree/master/roles/cacerts) role of the [core](https://github.com/c2platform/ansible-collection-core) collection for more information.

If you want to use certificates from this CA server solution you should add following code:

```yaml
- include_role:
    name: c2platform.tasks
    tasks_from: cert
  when: cacerts_ca_domains is defined
```

## Dependencies

<!--   A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles. -->

## Example Playbook

<!--   Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too: -->


