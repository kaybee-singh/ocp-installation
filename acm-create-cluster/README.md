1. Install ACM operator
2. Configure Multiclusterhub
3. Once multiclusterhub is configured configure host inventory
4. After configuring inventory click on **Create Infrastrucutre Environment**, provide the details like pull-secret, ssh key.
5. Then click on `Infrastructure Environment >> Add Hosts >> With Discovery ISO >> Full image file >>'
6. Download above created ISO and attach it to the machine.
7. If you have selected DHCP while creating the Infrastrucutre Environment then make sure your DNS provides resolution for assisted-image-service and assisted-service. Below is an example for a cluster with name **sno** and domain **localhost.com**. Otherwise host will not be discovered on ACM inventory.
```bash
192.168.122.26 assisted-image-service-multicluster-engine.apps.sno.localhost.com
192.168.122.26 assisted-service-multicluster-engine.apps.sno.localhost.com
```
8. A
