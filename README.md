# Ansible Role: bigiq_move_app_dashboard

Performs a series of steps needed to move an AS3 Application Service into an BIG-IQ Application in the BIG-IQ Dashboard.

## Role Variables

Available variables are listed below. For their default values, see `defaults/main.yml`.

Establishes initial connection to your BIG-IQ. These values are substituted into
your ``provider`` module parameter. These values should be the connection parameters
for the **CM BIG-IQ** device.

        provider:
          user: admin
          server: 10.1.1.4
          server_port: 443
          password: secret
          loginProviderName: tmos
          validate_certs: no

Define the list of Application and Application services as you wish it to be grouped on the BIG-IQ dashboard.

    apps: 
    - name: App1
        pins:
        - name: tenant1_app_service_1
        - name: tenant1_app_service_2
    - name: App2
        pins:
        - name: tenant2_app_service_1
        - name: tenant2_app_service_2

## Example Playbook

    ---
    - hosts: all
      connection: local
      vars:
        provider:
          user: admin
          server: "{{ ansible_host }}"
          server_port: 443
          password: secret
          loginProviderName: tmos
          validate_certs: no

      tasks:
          - name: Move or merge an AS3 application service in BIG-IQ dashboard.
            include_role:
              name: bigiq_move_app_dashboard
            vars:
                apps: 
                - name: App1
                    pins:
                    - name: tenant1_app_service_1
                    - name: tenant1_app_service_2
                - name: App2
                    pins:
                    - name: tenant2_app_service_1
                    - name: tenant2_app_service_2
            register: status

## License

Apache

## Author Information

This role was created in 2020 by [Romain Jouhannet](https://github.com/rjouhann).

[1]: https://galaxy.ansible.com/f5devcentral/bigiq_pinning_deploy_objects

