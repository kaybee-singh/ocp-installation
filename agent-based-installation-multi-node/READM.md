install-config.yaml
```bash
apiVersion: v1
baseDomain: example.com
metadata:
  name: ab
controlPlane:
  name: master
  replicas: 3
  architecture: amd64
compute: 
- name: worker
  replicas: 0 
platform:
  none: {}
pullSecret: '{"auths"saV3"}'
sshKey: |
  ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIEYiwfGoU592TWMgtB1INQhViagxPW karan@192.168.1.29
```

agent-config.yaml
```bash
apiVersion: v1alpha1
kind: AgentConfig
metadata:
  name: ab
rendezvousIP: 192.168.122.196
hosts:
  - hostname: master1
    interfaces:
      - name: ens3
        macAddress: 52:54:00:69:2a:b4
    rootDeviceHints:
      deviceName: /dev/vda
    networkConfig:
      interfaces:
        - name: ens3
          type: ethernet
          state: up
          mac-address: 52:54:00:69:2a:b4
          ipv4:
            enabled: true
            address:
              - ip: 192.168.122.196
                prefix-length: 23 
            dhcp: false
      dns-resolver:
        config:
          server:
            - 192.168.122.194 
      routes:
        config:
          - destination: 0.0.0.0/0
            next-hop-address: 192.168.122.1 
            next-hop-interface: ens3
            table-id: 254
  - hostname: master2
    interfaces:
      - name: ens3
        macAddress: 52:54:00:88:14:48
    rootDeviceHints:
      deviceName: /dev/vda
    networkConfig:
      interfaces:
        - name: ens3
          type: ethernet
          state: up
          mac-address: 52:54:00:88:14:48
          ipv4:
            enabled: true
            address:
              - ip: 192.168.122.197
                prefix-length: 23 
            dhcp: false
      dns-resolver:
        config:
          server:
            - 192.168.122.194 
      routes:
        config:
          - destination: 0.0.0.0/0
            next-hop-address: 192.168.122.1 
            next-hop-interface: ens3
  - hostname: master3
    interfaces:
      - name: ens3
        macAddress: 52:54:00:13:b7:98
    rootDeviceHints:
      deviceName: /dev/vda
    networkConfig:
      interfaces:
        - name: ens3
          type: ethernet
          state: up
          mac-address: 52:54:00:13:b7:98
          ipv4:
            enabled: true
            address:
              - ip: 192.168.122.198
                prefix-length: 23 
            dhcp: false
      dns-resolver:
        config:
          server:
            - 192.168.122.194 
      routes:
        config:
          - destination: 0.0.0.0/0
            next-hop-address: 192.168.122.1 
            next-hop-interface: ens3

```
