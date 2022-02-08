---

copyright:
  years: 2017, 2022
lastupdated: "2022-02-08"

keywords: terraform quickstart, terraform getting started, terraform tutorial, virtual server for classic infrastructure

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}

# Provisioning an {{site.data.keyword.cloud_notm}} virtual server for classic infrastructure
{: #sample_infrastructure_config}

You can provision your virtual server for classic infrastructure by using the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform on IBM Cloud. Similar to the [{{site.data.keyword.cloud_notm}} virtual server for VPC provision](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). that you provisioned. You need to create another configuration file with the specification for your virtual server instance. 
{: shortdesc}

Keep in mind that a virtual server is an {{site.data.keyword.cloud_notm}} classic infrastructure resource that incurs costs. Be sure to review the [available plans ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/gen1/infrastructure/provision/vs) before you proceed.
{: important}

1. Create a configuration file that is named `classic-vsi.tf` with the following content. Store this file in the folder that you created earlier.
 
    ```terraform
    resource "ibm_compute_vm_instance" "vm1" {
    hostname             = "vm1"
    domain               = "example.com"
    os_reference_code    = "DEBIAN_8_64"
    datacenter           = "dal10"
    network_speed        = 10
    hourly_billing       = true
    private_network_only = false
    cores                = 1
    memory               = 1024
    disks                = [25]
    local_disk           = false
    }
    ```
    {: codeblock}

    <table>
    <caption>Understanding the configuration file components</caption>
    <col>
        <col>
    <thead>
        <th>Parameter</th>
        <th>Description</th>
    </thead>
    <tbody>
    <tr>
    <td><code>resource</code></td>
    <td>Required: The name of the {{site.data.keyword.cloud_notm}} resource that you want to provision. To provision a classic infrastructure virtual server instance, use <code>ibm_compute_vm_instance</code>. To find a list of other resources that you can provision, see the <a href="/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#install_provider">{{site.data.keyword.cloud_notm}} Provider plug-in reference</a>.  </td>
    </tr>
    <tr>
    <td><code>vm1</code></td>
    <td>Required: Enter a name for your classic infrastructure virtual server instance.  </td>
    </tr>
        <tr>
        <td><code>hostname</code></td>
        <td>Optional: Enter a host name for your classic infrastructure virtual server instance. This host name is used with the <code>domain</code> to create the full URL for your classic infrastructure virtual server instance.</td>
        </tr>
        <tr>
        <td><code>domain</code></td>
        <td>Optional: Enter the domain name that you want to assign to your classic infrastructure virtual server instance. This domain name is used with the <code>hostname</code> to create the full URL for your classic infrastructure virtual server instance.</td>
        </tr>
        <tr>
        <td><code>os_reference_code</code></td>
        <td>Optional: Enter the reference code of the operating system that you want to install on your classic infrastructure virtual server instance. To find available reference codes, log in to the <a href="https://api.softlayer.com/rest/v3/SoftLayer_Virtual_Guest_Block_Device_Template_Group/getVhdImportSoftwareDescriptions.json?objectMask=referenceCode">{{site.data.keyword.cloud_notm}} classic infrastructure API</a> <img src="../icons/launch-glyph.svg" alt="External link icon">.</td>
        </tr>
        <tr>
        <td><code>datacenter</code></td>
        <td>Required: Enter the location where you want to provision your classic infrastructure virtual server instance. For available locations, see the <a href="https://api.softlayer.com/rest/v3/SoftLayer_Location/getDatacenters.json?objectMask=name">{{site.data.keyword.cloud_notm}} classic infrastructure API</a> <img src="../icons/launch-glyph.svg" alt="External link icon">.</td>
        </tr>
        <tr>
        <td><code>network_speed</code></td>
        <td>Optional: Enter the network speed in Mbps for your classic infrastructure virtual server instance. Supported values are 10, 100, and 1000. If you do not specify this value, 100 Mbps is used by default. </td>
        </tr>
        <tr>
        <td><code>hourly_billing</code></td>
        <td>Optional: Specify how you want to get billed for your classic infrastructure virtual server instance. Enter <code>true</code> for hourly billing, and <code>false</code> for monthly billing. If you do not specify a billing type, hourly billing is used by default.</td>
        </tr>
        <tr>
        <td><code>private_network_only</code></td>
        <td>Optional: Decide if you want to connect your classic infrastructure virtual server instance to a private VLAN only. Enter <code>true</code> to connect it to a private VLAN only, and <code>false</code> to connect it to a public and a private VLAN. If you do not specify this option, your virtual server instance is automatically connected to a private and public VLAN by default. </td>
        </tr>
        <tr>
        <td><code>cores</code></td>
        <td>Optional: Enter the number of CPU cores that you want to allocate to your classic infrastructure virtual server instance.</td>
        </tr>
        <tr>
        <td><code>memory</code></td>
        <td>Optional: The amount of memory in megabytes that you want to allocate to your classic infrastructure virtual server instance.</td>
        </tr>
        <tr>
        <td><code>[disks]</code></td>
        <td>Optional: Enter the numeric disk sizes in gigabytes that you want to allocate to your classic infrastructure virtual server instance. To specify multiple disk sizes, separate each value with a comma {<code>,</code>). By default, the smallest disk size that is available for the type of virtual server is used.</td>
        </tr>
        <tr>
        <td><code>local_disks</code></td>
        <td>Optional: Specify the type of disk that you want to provision. Enter <code>true</code> to provision the disks on the host that the virtual server instance runs on, or <code>false</code> to provision SAN disks. If you do not specify this option, disks are provisioned on the host by default.</td>
        </tr>
    </tbody>
    </table>

2. Initialize Terraform on IBM Cloud.

    ```sh
    terraform init
    ```
    {: pre}
   
    **Example output:**

    ```text
    Initializing provider plugins...

    The following providers do not have any version constraints in configuration, so the latest version was installed.

    To prevent automatic upgrades to new major versions that may contain breaking changes, it is recommended to add version = "..." constraints to the corresponding provider blocks in configuration, with the constraint strings suggested.

    Terraform on IBM Cloud has been successfully initialized!

    You may now begin working with Terraform on IBM Cloud. Try running "terraform plan" to see any changes that are required for your infrastructure. All Terraform on IBM Cloud commands should now work.

    If you ever set or change modules or backend configuration for Terraform on IBM Cloud, rerun this command to reinitialize your working directory. If you forget, other commands detects it and remind you to do so if necessary.
    ```
    {: screen}

3. Generate an Terraform on IBM Cloud execution plan. When you execute this command, Terraform on IBM Cloud validates the syntax of your configuration file and resource definitions against the specifications that are provided by the {{site.data.keyword.cloud_notm}} Provider plug-in. 
  
    ```sh
    terraform plan
    ```
    {: pre}

    **Example output:**

    ```text
    Refreshing Terraform on IBM Cloud state in-memory prior to plan...
    The refreshed state be used to calculate this plan, but not be persisted to local or remote state storage.

    An execution plan has been generated and is shown.
    Resource actions are indicated with the following symbols:
      + create

    Terraform on IBM Cloud performs the following actions:

     + ibm_compute_vm_instance.vm1
         id:                           <computed>
         block_storage_ids.#:          <computed>
         cores:                        "1"
         datacenter:                   "dal10"
         disks.#:                      "1"
         disks.0:                      "25"
         domain:                       "example.com"
         file_storage_ids.#:           <computed>
         hostname:                     "vm1"
         hourly_billing:               "true"
         ip_address_id:                <computed>
         ip_address_id_private:        <computed>
         ipv4_address:                 <computed>
         ipv4_address_private:         <computed>
         ipv6_address:                 <computed>
         ipv6_address_id:              <computed>
         ipv6_enabled:                 "false"
         ipv6_static_enabled:          "false"
         local_disk:                   "false"
         memory:                       "1024"
         network_speed:                "10"
         os_reference_code:            "DEBIAN_8_64"
         private_interface_id:         <computed>
         private_network_only:         "false"
         private_security_group_ids.#: <computed>
         private_subnet:               <computed>
         private_subnet_id:            <computed>
         private_vlan_id:              <computed>
         public_bandwidth_limited:     <computed>
         public_bandwidth_unlimited:   "false"
         public_interface_id:          <computed>
         public_ipv6_subnet:           <computed>
         public_ipv6_subnet_id:        <computed>
         public_security_group_ids.#:  <computed>
         public_subnet:                <computed>
         public_subnet_id:             <computed>
         public_vlan_id:               <computed>
         secondary_ip_addresses.#:     <computed>
         wait_time_minutes:            "90"

        Plan: 1 to add, 0 to change, 0 to destroy.
        ------------------------------------------------------------------------
        Note You didn't specify an "-out" parameter to save this plan, so Terraform on IBM Cloud can't guarantee that exactly these actions be performed if "terraform apply" is subsequently run.
        ```
        {: screen}

4. Review the execution plan to verify the type of resource that is planned to be provisioned by Terraform on IBM Cloud.

5. Create your classic infrastructure virtual server. Confirm the creation by entering `yes` when prompted. 

    ```sh
    terraform apply
    ```
    {: pre} 

    **Example output:**

    ```text
      Creating...
      block_storage_ids.#:        "" => "<computed>"
      cores:                      "" => "1"
      datacenter:                 "" => "dal10"
      disks.#:                    "" => "1"
      disks.0:                    "" => "25"
      domain:                     "" => "example.com"
      file_storage_ids.#:         "" => "<computed>"
      hostname:                   "" => "vm1"
      hourly_billing:             "" => "true"
      ip_address_id:              "" => "<computed>"
      ip_address_id_private:      "" => "<computed>"
      ipv4_address:               "" => "<computed>"
      ipv4_address_private:       "" => "<computed>"
      ipv6_address:               "" => "<computed>"
      ipv6_address_id:            "" => "<computed>"
      ipv6_enabled:               "" => "false"
      local_disk:                 "" => "false"
      memory:                     "" => "1024"
      network_speed:              "" => "10"
      os_reference_code:          "" => "DEBIAN_8_64"
      private_network_only:       "" => "false"
      private_subnet:             "" => "<computed>"
      private_vlan_id:            "" => "<computed>"
      public_bandwidth_limited:   "" => "<computed>"
      public_bandwidth_unlimited: "" => "false"
      public_ipv6_subnet:         "" => "<computed>"
      public_subnet:              "" => "<computed>"
      public_vlan_id:             "" => "<computed>"
      secondary_ip_addresses.#:   "" => "<computed>"
      wait_time_minutes:          "" => "90"
       ibm_compute_vm_instance.vm1: Still creating... (10s elapsed)
       ibm_compute_vm_instance.vm1: Still creating... (20s elapsed)
       ibm_compute_vm_instance.vm1: Still creating... (30s elapsed)
       ibm_compute_vm_instance.vm1: Still creating... (40s elapsed)
       ibm_compute_vm_instance.vm1: Still creating... (50s elapsed)
       ibm_compute_vm_instance.vm1: Still creating... (1m0s elapsed)
       ibm_compute_vm_instance.vm1: Creation complete after 1m04s (ID: 62364997)
       
       Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
    ```
    {: screen}

6. List the classic infrastructure virtual server that is provisioned. 
   
    ```sh
    terraform show
    ```
    {: pre}

    **Example output:**

    ```text
        ibm_compute_vm_instance.vm1:
        id = 62364997
        block_storage_ids.# = 0
        cores = 1
        datacenter = dal10
        dedicated_acct_host_only = false
        disks.# = 1
        disks.0 = 25
        domain = example.com
        file_storage_ids.# = 0
        hostname = vm1
        hourly_billing = true
        ip_address_id = 120354689
        ip_address_id_private = 120356235
        ipv4_address = 169.53.33.54
        ipv4_address_private = 10.120.45.183
        ipv6_enabled = false
        local_disk = false
        memory = 1024
        network_speed = 10
        notes = 
        os_reference_code = DEBIAN_8_64
        private_network_only = false
        private_subnet = 10.120.45.128/26
        private_vlan_id = 2451153
        public_bandwidth_unlimited = false
        public_subnet = 169.53.33.48/28
        public_vlan_id = 2451151
        secondary_ip_addresses.# = 0
        wait_time_minutes = 90
    ```
    {: screen}

7. Optional: Review your classic virtual server instance in the [{{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/classic/devices). 

8. Optional: Remove your classic infrastructure virtual server. 

    ```sh
    terraform destroy
    ```
    {: pre}

**What's next?** 

Explore other [{{site.data.keyword.cloud_notm}} resources](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#install_provider) that you can provision with Terraform on IBM Cloud. 


