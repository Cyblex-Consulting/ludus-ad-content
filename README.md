# Ansible Role: Active Directory content (Ludus)

An Ansible Role that creates content in an Active Directory.

The role performs the following actions:
- Add Organizational Units
- Add Groups
- Add Users

> [!WARNING]
> This role shall be applied on the primary DC.

## Requirements

None.

## Role Variables

Available variables are listed below. There is no default values. Everything shall be configured in the range configuration.

### Variables used when creating an Organizational Unit :

    # OU Name
    ludus_ad.ous.name: France

    # OU Path
    ludus_ad.ous.path: DC=myrange,DC=corp

    # OU Description
    ludus_ad.ous.description: jdoe

### Variables used when creating an Group :

    # Group Name
    ludus_ad.groups.name: France

    # Group Scope
    ludus_ad.groups.scope: global

    # Group Path
    ludus_ad.groups.path: OU=France,DC=myrange,DC=corp
    
    # Group Description
    ludus_ad.groups.description: jdoe

### Variables used when creating a User :

    # User Name
    ludus_ad.users.name: France

    # User First Name
    ludus_ad.users.firstname: John

    # User Surname
    ludus_ad.users.surname: Doe

    # User Display Name
    ludus_ad.users.surname: display_name

    # User Password
    ludus_ad.users.password: GFVfPS432QkKN2YdQwJL

    # User Path
    ludus_ad.users.path: OU=France,DC=myrange,DC=corp
    
    # User Description
    ludus_ad.users.description: IT System Administrator

    # List of groups to add the user into
    ludus_ad.users.groups: 
      - Group 1
      - Group 2

## Example Ludus Range Config

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
      - ludus-ad-content
    role_vars:
      ludus_ad:
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

## License

GPLv3

## Author Information

This role was created by [Cyblex Consulting](https://github.com/Cyblex-Consulting), for [Ludus](https://ludus.cloud/).
