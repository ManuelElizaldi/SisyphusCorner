[[Virtualization]] [[Azure]] [[Monitoring]]
# VM Scale Set
The set up is very similar to the VM creation steps. 

If you don't specify the Availability Zone, all VMs will be deployed in the same AZ.  

When selecting the disk option, all VMs will receive this setting. 

You can deploy beyond 100 VMs

*Allocation zone* -> forcefully spread across availability zones. There is a balance in what is covered. 

*Spreading algorithm*:
- Max spreading means that every domain will be covered. **This is recommended**
- Fixed spreading means that you choose how many domains will be covered. 

## Networking for Scale Set
Make sure your IP range can support the VMs you are deploying

You can deploy the security rules on the NIC or at the subnet level 

### Overprovisioning 
Deploying more VMs than what you asked for, then deletes the extras. This improves provisioning success rate and reduces deployment time.

basically a security measure to ensure you have VMs available 

Free of cost 

### Automatic Upgrade of OS 
This is an optional setting 

# Extensions
You can install the custom power shell scripts to run run power shell scripts in VM inside the Advanced tab in the VM creation

Deploy anti virus can be done here 

Custom scripts

Add GPU drivers

You decide where and when to deploy to VMs 
- example, you choose only VM 1 and 3 to update 
- You can also choose to update VMs automatically, manually or rolling upgrades. 
	- Rolling upgrade means it starts with a couple then move to the next batch when the 1st batch is ready 

Extension scripts are stored in the *storage account* (S3 equivalent in Azure).  
## Health Monitoring - Extension
This is an extension that can be enabled to monitor the health of an instance using the TCP protocol on port 80. You can also use the HTTP protocol and check a specific path. 

You can also enable automatic repair - brings down the unhealthy VM and deploys a new one with all the extensions you set up. 

Be careful that health checks are set up correctly, meaning, that you are pointing to the right path, if not, your VM wont be reachable and the system will consider it to be unhealthy 


# VMs in Availability set/zone vs virtual Machine scale sets 

| Availability Set Zone                                                                 | Virtual Machine Scale Set                        |
| ------------------------------------------------------------------------------------- | ------------------------------------------------ |
| your responsibility to configure fault and update domains                             | Fault domain and update domains are auto managed |
| Each VM is created separately                                                         | VMs can be created as a group                    |
| size and config can be different                                                      | Size and configs is the same for all VMs         |
| OS can be different                                                                   | Same OS for all vms                              |
| Apps need to be installed separately                                                  | Apps can be installed with extensions            |
| manual scaling                                                                        | VMs can be auto added to a load balancer         |
| Add load balancer manually                                                            | Can deploy in different data centers             |
| same data center in availability set and different datacenters for availability zones |                                                  |
|                                                                                       |                                                  |
