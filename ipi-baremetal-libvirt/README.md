```bash
cat install-config.yaml
apiVersion: v1
baseDomain: example.com
metadata:
  name: sno47
networking:
  machineNetwork:
  - cidr: 192.168.122.0/24
  networkType: OVNKubernetes
compute:
- name: worker
  replicas: 0
controlPlane:
  name: master
  replicas: 3
  platform:
    baremetal: {}
platform:
  baremetal:
    libvirtURI: qemu:///system
    externalBridge: virbr0
    provisioningNetwork: "Disabled"
    apiVIPs:
      - 192.168.122.26
    ingressVIPs:
      - 192.168.122.27
    bootstrapExternalStaticIP: 192.168.122.171
    bootstrapExternalStaticGateway: 192.168.122.1
    bootstrapExternalStaticDNS: 192.168.122.24
    bootstrapOSImage: 'https://mirror.openshift.com/pub/openshift-v4/dependencies/rhcos/4.20/latest/rhcos-qemu.x86_64.qcow2.gz?sha256=214f4c5c69b329fa54162f92c2ff00a5c7648ea2400118b6c0d73447fb2c1a4b'
    hosts:
    # ================= MASTER NODES =================

    - name: master1
      role: master
      bootMACAddress: 52:54:00:65:5a:f3
      bootMode: UEFI
      bmc:
        address: redfish-virtualmedia://192.168.122.1/redfish/v1/Systems/865571e2-88d7-4bf4-9bd0-a40ca442a3ea
        username: admin
        password: redhat
        disableCertificateVerification: True
      networkConfig:
        interfaces:
          - name: bond0
            type: bond
            state: up
            ipv4:
              enabled: true
              address:
                - ip: 192.168.122.172
                  prefix-length: 24
              dhcp: false
            link-aggregation:
              mode: active-backup
              options:
                miimon: '100'
              port:
                - enp1s0
                - enp7s0
        dns-resolver:
          config:
            server:
              - 192.168.122.24
        routes:
          config:
            - destination: 0.0.0.0/0
              next-hop-address: 192.168.122.1
              next-hop-interface: bond0
      rootDeviceHints:
        deviceName: "/dev/vda"

    - name: master2
      role: master
      bootMACAddress: 52:54:00:17:88:e4
      bootMode: UEFI
      bmc:
        address: redfish-virtualmedia://192.168.122.1/redfish/v1/Systems/c56b39e2-6b2e-4d01-b607-a362170aac46
        username: admin
        password: redhat
        disableCertificateVerification: True
      networkConfig:
        interfaces:
          - name: bond0
            type: bond
            state: up
            ipv4:
              enabled: true
              address:
                - ip: 192.168.122.173
                  prefix-length: 24
              dhcp: false
            link-aggregation:
              mode: active-backup
              options:
                miimon: '100'
              port:
                - enp1s0
                - enp7s0
        dns-resolver:
          config:
            server:
              - 192.168.122.24
        routes:
          config:
            - destination: 0.0.0.0/0
              next-hop-address: 192.168.122.1
              next-hop-interface: bond0
      rootDeviceHints:
        deviceName: "/dev/vda"

    - name: master3
      role: master
      bootMACAddress: 52:54:00:e9:81:92
      bootMode: UEFI
      bmc:
        address: redfish-virtualmedia://192.168.122.1/redfish/v1/Systems/88269168-6a84-4ab2-9f40-31cb6bbcdfad
        username: admin
        password: redhat
        disableCertificateVerification: True
      networkConfig:
        interfaces:
          - name: bond0
            type: bond
            state: up
            ipv4:
              enabled: true
              address:
                - ip: 192.168.122.174
                  prefix-length: 24
              dhcp: false
            link-aggregation:
              mode: active-backup
              options:
                miimon: '100'
              port:
                - enp1s0
                - enp7s0
        dns-resolver:
          config:
            server:
              - 192.168.122.24
        routes:
          config:
            - destination: 0.0.0.0/0
              next-hop-address: 192.168.122.1
              next-hop-interface: bond0
      rootDeviceHints:
        deviceName: "/dev/vda"
pullSecret: ''
sshKey: ''
```
```bash
openshift-install create manifests --dir=.
openshift-install create cluster
```
