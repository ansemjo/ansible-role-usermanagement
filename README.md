# ansemjo.usermanagement

Manage system groups and users, add authorized ssh keys and allow passwordless
sudo for selected groups or users. Example usage to create two system users for
subsequent usage by ansible:

```yaml
#!/usr/bin/env ansible-playbook
---

- name: configure management user
  hosts: my_systems
  gather_facts: no
  user: my_admin
  become: yes
  vars:

    ansemjo_usermanagement_groups:
      - name: ansible
        sudo: yes

    ansemjo_usermanagement_users:

      - name: alice
        group: ansible
        home: /var/lib/ansible_alice
        authorized_keys:
          - "{{ lookup('file', '~/.ssh/alice.pub') }}"

      - name: bob
        group: ansible
        home: /var/lib/ansible_bob
        authorized_keys:
          - "{{ lookup('file', '~/.ssh/bob.pub') }}"

  roles:

    - ansemjo.usermanagement

```

Default values should be described in the [`defaults`](defaults/main.yml).
