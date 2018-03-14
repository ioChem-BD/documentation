##Post installation check steps  
Finally, system administrator must check the following communication channels in order for ioChem-BD platform to properly operate:
  * Check connectivity from HPC cluster to ioChem-BD web server (if using shell upload from the HPC) on [the defined port](/installation/required_steps.md#certificate-fields)
  * Check [calculation publication](/usage/publishing-calculations.md) from Create to Browse. 
  * Check Browse email notification parameters, using [defined port](/installation/required_steps.md#mail-settings).
Its up to the sysadmin to configure the network interfaces, firewall services, proxies and other routing mechanisms to allow previous communications.

#Resume
This last step conclude the ioChem-BD system installation and configuration. Let us recap all steps taken until we get here:
   1. Gather important system configuration parameters
   2. Create database and start software installation
   3. Copy Create license to installation directory
   4. Start webserver and login as administrator
   5. Generate users and groups from Browse module
   6. Create communities and subcommunities where users will be able to publish their digital assets.
   7. Setup backup script and test platform network connectivity