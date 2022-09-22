# Ansible Collections for testing ansible-lint

This repository contains stub Ansible Collections used to test a bug in ``ansible-lint``.

## Installation

To install them, run the command:

    ansible-galaxy collection install git+https://github.com/drybjed/ansible-collections

## Usage

To use the collection playbooks and roles, you can execute commands:

    ansible-playbook drybjed.namespace1.role1 -l <host>
    ansible-playbook drybjed.namespace2.all -l <host>

## Debugging

Debug information during installation via ``ansible-galaxy``:

    drybjed@work:~$ ansible-galaxy collection install https://github.com/drybjed/ansible-collections
    Cloning into '/home/drybjed/.ansible/tmp/ansible-local-11778ravmw71o/tmpenp_fp3k/ansible-collectionse44wc54u'...
    remote: Enumerating objects: 17, done.
    remote: Counting objects: 100% (17/17), done.
    remote: Compressing objects: 100% (15/15), done.
    remote: Total 17 (delta 4), reused 0 (delta 0), pack-reused 0
    Receiving objects: 100% (17/17), 1.98 KiB | 1.98 MiB/s, done.
    Resolving deltas: 100% (4/4), done.
    Your branch is up to date with 'origin/master'.
    Starting galaxy collection install process
    Process install dependency map
    Starting collection install process
    Installing 'drybjed.namespace2:1.0.0' to '/home/drybjed/.ansible/collections/ansible_collections/drybjed/namespace2'
    Created collection for drybjed.namespace2:1.0.0 at /home/drybjed/.ansible/collections/ansible_collections/drybjed/namespace2
    drybjed.namespace2:1.0.0 was installed successfully
    Installing 'drybjed.namespace1:1.0.0' to '/home/drybjed/.ansible/collections/ansible_collections/drybjed/namespace1'
    Created collection for drybjed.namespace1:1.0.0 at /home/drybjed/.ansible/collections/ansible_collections/drybjed/namespace1
    drybjed.namespace1:1.0.0 was installed successfully

Debug information during execution of ``ansible-lint -v`` in the top of the
repository (IMPORTANT! Remove the collections from ~/.ansible/collections/
before executing ``ansible-lint``):

    drybjed@work:~$ ansible-lint -v
    INFO     Set ANSIBLE_LIBRARY=/home/drybjed/.cache/ansible-compat/23e2f6/modules:/home/drybjed/.ansible/plugins/modules:/usr/share/ansible/plugins/modules
    INFO     Set ANSIBLE_COLLECTIONS_PATH=/home/drybjed/.cache/ansible-compat/23e2f6/collections:/home/drybjed/.ansible/collections:/usr/share/ansible/collections
    INFO     Set ANSIBLE_ROLES_PATH=/home/drybjed/.cache/ansible-compat/23e2f6/roles:/home/drybjed/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles
    INFO     Set ANSIBLE_LIBRARY=/home/drybjed/.cache/ansible-compat/23e2f6/modules:/home/drybjed/.ansible/plugins/modules:/usr/share/ansible/plugins/modules
    INFO     Set ANSIBLE_COLLECTIONS_PATH=/home/drybjed/.cache/ansible-compat/23e2f6/collections:/home/drybjed/.ansible/collections:/usr/share/ansible/collections
    INFO     Set ANSIBLE_ROLES_PATH=/home/drybjed/.cache/ansible-compat/23e2f6/roles:/home/drybjed/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles
    INFO     Discovered files to lint using: git ls-files --cached --others --exclude-standard -z
    INFO     Excluded removed files using: git ls-files --deleted -z
    INFO     Discovered files to lint using: git ls-files --cached --others --exclude-standard -z
    INFO     Excluded removed files using: git ls-files --deleted -z
    INFO     Executing syntax check on namespace1/playbooks/role2.yml (0.57s)
    INFO     Executing syntax check on namespace2/playbooks/role1.yml (0.65s)
    INFO     Executing syntax check on namespace2/playbooks/all.yml (0.67s)
    INFO     Executing syntax check on namespace1/playbooks/all.yml (0.76s)
    INFO     Executing syntax check on namespace2/playbooks/role2.yml (0.76s)
    INFO     Executing syntax check on namespace1/playbooks/role1.yml (0.77s)
    WARNING  Listing 4 violation(s) that are fatal
    internal-error: the role 'drybjed.namespace1.role1' was not found in /home/drybjed/src/github.com/drybjed/ansible-collections/namespace1/playbooks/roles:/home/drybjed/.cache/ansible-compat/23e2f6/roles:/home/drybjed/.ansible/ro
    les:/usr/share/ansible/roles:/etc/ansible/roles:/home/drybjed/src/github.com/drybjed/ansible-collections/namespace1/playbooks
    namespace1/playbooks/role1.yml:10:15 ERROR! the role 'drybjed.namespace1.role1' was not found in /home/drybjed/src/github.com/drybjed/ansible-collections/namespace1/playbooks/roles:/home/drybjed/.cache/ansible-compat/23e2f6/roles:/home/drybjed/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles:/home/drybjed/src/github.com/drybjed/ansible-collections/namespace1/playbooks
    
    The error appears to be in '/home/drybjed/src/github.com/drybjed/ansible-collections/namespace1/playbooks/role1.yml': line 10, column 15, but may
    be elsewhere in the file depending on the exact syntax problem.
    
    The offending line appears to be:
    
          ansible.builtin.import_role:
            name: 'drybjed.namespace1.role1'
                  ^ here
    
    
    internal-error: the role 'drybjed.namespace1.role2' was not found in /home/drybjed/src/github.com/drybjed/ansible-collections/namespace1/playbooks/roles:/home/drybjed/.cache/ansible-compat/23e2f6/roles:/home/drybjed/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles:/home/drybjed/src/github.com/drybjed/ansible-collections/namespace1/playbooks
    namespace1/playbooks/role2.yml:10:15 ERROR! the role 'drybjed.namespace1.role2' was not found in /home/drybjed/src/github.com/drybjed/ansible-collections/namespace1/playbooks/roles:/home/drybjed/.cache/ansible-compat/23e2f6/roles:/home/drybjed/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles:/home/drybjed/src/github.com/drybjed/ansible-collections/namespace1/playbooks
    
    The error appears to be in '/home/drybjed/src/github.com/drybjed/ansible-collections/namespace1/playbooks/role2.yml': line 10, column 15, but may
    be elsewhere in the file depending on the exact syntax problem.
    
    The offending line appears to be:
    
          ansible.builtin.import_role:
            name: 'drybjed.namespace1.role2'
                  ^ here
    
    
    internal-error: the role 'drybjed.namespace2.role1' was not found in /home/drybjed/src/github.com/drybjed/ansible-collections/namespace2/playbooks/roles:/home/drybjed/.cache/ansible-compat/23e2f6/roles:/home/drybjed/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles:/home/drybjed/src/github.com/drybjed/ansible-collections/namespace2/playbooks
    namespace2/playbooks/role1.yml:10:15 ERROR! the role 'drybjed.namespace2.role1' was not found in /home/drybjed/src/github.com/drybjed/ansible-collections/namespace2/playbooks/roles:/home/drybjed/.cache/ansible-compat/23e2f6/roles:/home/drybjed/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles:/home/drybjed/src/github.com/drybjed/ansible-collections/namespace2/playbooks
    
    The error appears to be in '/home/drybjed/src/github.com/drybjed/ansible-collections/namespace2/playbooks/role1.yml': line 10, column 15, but may
    be elsewhere in the file depending on the exact syntax problem.
    
    The offending line appears to be:
    
          ansible.builtin.import_role:
            name: 'drybjed.namespace2.role1'
                  ^ here
    
    
    internal-error: the role 'drybjed.namespace2.role2' was not found in /home/drybjed/src/github.com/drybjed/ansible-collections/namespace2/playbooks/roles:/home/drybjed/.cache/ansible-compat/23e2f6/roles:/home/drybjed/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles:/home/drybjed/src/github.com/drybjed/ansible-collections/namespace2/playbooks
    namespace2/playbooks/role2.yml:10:15 ERROR! the role 'drybjed.namespace2.role2' was not found in /home/drybjed/src/github.com/drybjed/ansible-collections/namespace2/playbooks/roles:/home/drybjed/.cache/ansible-compat/23e2f6/roles:/home/drybjed/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles:/home/drybjed/src/github.com/drybjed/ansible-collections/namespace2/playbooks
    
    The error appears to be in '/home/drybjed/src/github.com/drybjed/ansible-collections/namespace2/playbooks/role2.yml': line 10, column 15, but may
    be elsewhere in the file depending on the exact syntax problem.
    
    The offending line appears to be:
    
          ansible.builtin.import_role:
            name: 'drybjed.namespace2.role2'
                  ^ here
    
    
    INFO     Lock 140113202295952 released on /home/drybjed/.cache/ansible-compat/23e2f6/.lock
    You can skip specific rules or tags by adding them to your configuration file:
    # .config/ansible-lint.yml
    warn_list:  # or 'skip_list' to silence them completely
      - internal-error  # Unexpected internal error.
    
    Finished with 4 failure(s), 0 warning(s) on 17 files.

