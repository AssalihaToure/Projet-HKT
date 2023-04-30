---
- name: Configuration de base pour le routeur et les switchs
  hosts: router_switches
  gather_facts: false

  vars:
    router_hostname: R1
    switch1_hostname: S1
    switch2_hostname: S2

  tasks:
    - name: Configuration du hostname du routeur
      ios_command:
        commands:
          - "hostname {{ router_hostname }}"
        provider: "{{ cli }}"
      register: output

    - name: Configuration de l'adresse IP pour le routeur
      ios_command:
        commands:
          - "interface GigabitEthernet0/0"
          - "ip address 192.168.1.1 255.255.255.0"
          - "no shutdown"
        provider: "{{ cli }}"
      register: output

    - name: Configuration de la sécurité du routeur
      ios_command:
        commands:
          - "enable secret level 5 cisco1234"
          - "username admin privilege 15 secret level 5 cisco1234"
          - "no service pad"
          - "service password-encryption"
          - "login block-for 60 attempts 3 within 120"
        provider: "{{ cli }}"
      register: output

    - name: Configuration du hostname du switch 1
      ios_command:
        commands:
          - "hostname {{ switch1_hostname }}"
        provider: "{{ cli }}"
      register: output

    - name: Configuration de l'adresse IP pour le switch 1
      ios_command:
        commands:
          - "interface Vlan1"
          - "ip address 192.168.1.2 255.255.255.0"
          - "no shutdown"
        provider: "{{ cli }}"
      register: output

    - name: Configuration de la sécurité du switch 1
      ios_command:
        commands:
          - "enable secret level 5 cisco1234"
          - "username admin privilege 15 secret level 5 cisco1234"
          - "no service pad"
          - "service password-encryption"
          - "login block-for 60 attempts 3 within 120"
        provider: "{{ cli }}"
      register: output

    - name: Configuration du hostname du switch 2
      ios_command:
        commands:
          - "hostname {{ switch2_hostname }}"
        provider: "{{ cli }}"
      register: output

    - name: Configuration de l'adresse IP pour le switch 2
      ios_command:
        commands:
          - "interface Vlan1"
          - "ip address 192.168.1.3 255.255.255.0"
          - "no shutdown"
        provider: "{{ cli }}"
      register: output

    - name: Configuration de la sécurité du switch 2
      ios_command:
        commands:
          - "enable secret level 5 cisco1234"
          - "username admin privilege 15 secret level 5 cisco1234"
          - "no service pad"
          - "service password-encryption"
          - "login block-for 60 attempts 3 within 120"
        provider: "{{ cli }}"
      register: output
