
## 4. Verify Lab Deployment
**Estimated Time to Complete: 30 minutes**

Once the Deployment Script has completed the installation and setup process. Your lab environment is fully ready to start testing the NSX Distributed IDS/IPS. Verify vCenter and NSX has been configured as intended.

**Physical Infrastructure Host/vCenter**

![](assets/images/IDPS_POC_1.PNG)

**Logical Nested Lab**
![](assets/images/IDPS_POC_27.PNG)

**Validate VM Deployment in the physical Environment**

Login to the physial environment vcenter and Verify 6 VMs have been deployed, are up and running and are connected to the appropriate port-group: 
* 3 nested ESXI
* 1 NSX Manager
* 1 NSX Edge 
* 1 vCenter
* 1 External VM

![](assets/images/IDPS_POC_2.PNG)

Confirm you are able to ping each nested ESXi, the Lab NSX Manager and the Lab vCenter.

**Configure a static route on the External VM**

You will need to manually change the IP address of the external VM to an IP address in the same managment subnet you used for vCenter/NSX Manager and the rest of the environment. You will also need to adjust the static route so the external VM is able to reach the DMZ subnet inside the nested lab environemnt. There is no need for a default gateway to be configured as the only route the external VM needs is to the DMZ segment.

From the physical environent vCenter, open a console to **External VM** and take the following steps:
* Login with **vmware**/**VMware1!**
* Type **sudo nano /etc/network/interfaces** to open the network configuration file
![](assets/images/IDPS_POC_16.PNG)
* For interface **ens160** chgange the **address** and **netmask** to match the appropriate settings for your enviornment
* In the line that stats with **up route add**, change the **gw address** (10.114.209.148 in my example) to the **T0 Uplink interface IP address**
 
**Verify Nested Lab vCenter**
Login to lab vCenter and verify the cluster of 3 nested ESXi appliances is functional and 4 vulnerable VMs have been deployed on the cluster:
* APP-1-WEB-TIER connected to **DMZSegment** Portgroup
* APP-2-WEB-TIER connected to **DMZSegment** Portgroup
* APP-1-APP-TIER connected to **InternalSegment** Portgroup
* APP-2-APP-TIER connected to **InternalSegment** Portgroup

**Verify Nested Lab NSX Manager**
Login to lab NSX Manager and run the below steps to verify the deployment:

1.	In the NSX Manager UI, navigate to Inventory -->  Virtual Machines
2. Click **View Details**
2. Note the IP addresses for the 4 VMs that were deployed


![](assets/images/IDPS_POC_11.PNG)
![](assets/images/IDPS_POC_12.PNG)

**Nested Lab Environment**

<img src="https://github.com/vmware-nsx/eval-docs-ids-ips/raw/master/docs/assets/images/IDPS_POC_27.PNG" width=50% height=50%>

[TO BE COMPLETED]
---

[***Next Step: 5. Initial IDS/IPS Configuration***](/docs/5-InitialConfiguration.md)
