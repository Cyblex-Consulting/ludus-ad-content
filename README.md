Ludus Role: Active Directory content
=========

This is a role for Ludus that creates content in an Active Directory

The role performs the following actions:
- Add Organizational Units
- Add Groups
- Add Users


Role Variables
--------------

There is no default values. Everything shall be configured in the range configuration.

The role shall be applied on the primary DC and that would look like this in the range configuration:

```yaml
  - vm_name: "{{ range_id }}-DC-01"
    hostname: "{{ range_id }}-DC-01"
    template: win2022-server-x64-template
    vlan: 53
    ip_last_octet: 1
    ram_gb: 8
    cpus: 4
    windows:
      sysprep: false
    domain:
      fqdn: myrange.corp
      role: primary-dc
    roles:
      - ad-content
    role_vars:
      ad:
        ous:
          - name: France
            path: DC=myrange,DC=corp
            description: French subsidiary
          - name: Germany
            path: DC=myrange,DC=corp
            description: German subsidiary
        groups:
          - name: Sales France
            scope: global
            path: "OU=France,DC=myrange,DC=corp"
            description: France Sales Department
          - name: Sales Germany
            scope: global
            path: "OU=Germany,DC=myrange,DC=corp"
            description: Germany Sales Department
          - name: IT
            scope: global
            path: "DC=myrange,DC=corp"
            description: IT Department
        users:
          - name: jdoe
            firstname: John
            surname: Doe
            display_name: John Doe
            password: GFVfPS432QkKN2YdQwJL
            path: "DC=myrange,DC=corp"
            description: IT System Administrator
            groups:
              - Domain Users
              - IT
```