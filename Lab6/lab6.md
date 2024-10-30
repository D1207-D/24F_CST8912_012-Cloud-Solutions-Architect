# CST8912 – Cloud Solution Architecture

## Cloud Development and Operations  
**Course:** CST8912_013 Cloud Solution Architecture  
**Lab:** Lab 4_Week 5  

**Prepared By:** Daniyal Shahid (041110791)  
**Submitted to:** Prof. Ragini Madan  

---

## Graded Lab Activity #6  
### Create a Virtual Network and Bastion Host

1. In the portal, search for and select **Virtual networks**.
2. On the Virtual networks page, select **+ Create**.
3. In the **Basics** tab of *Create virtual network*, enter or select the following information:

   | Setting         | Value               |
   |-----------------|---------------------|
   | Subscription    | Azure for students  |
   | Resource Group  | CST8912demo         |
   | Name            | 8912-vnet1          |
   | Region          | Canada Central      |

4. Select **Next** to proceed to the **Security** tab.
5. Select **Enable Bastion** in the **Azure Bastion** section of the Security tab.
6. Enter or select the following information in Azure Bastion:

   | Setting                        | Value                      |
   |--------------------------------|----------------------------|
   | Azure Bastion host name        | Bastion8912                |
   | Azure Bastion public IP address| Create a public IP address |
   | Public IP Name                 | public-ip                  |

7. Select **Next** to proceed to the **IP Addresses** tab.
8. In the **address space** box in **Subnets**, select the default subnet.
9. In **Edit subnet**, enter or select the following:

   | Setting          | Value                   |
   |------------------|-------------------------|
   | Subnet template  | Default                 |
   | Name             | Subnet-1-8912           |
   | IPv4 address range | 10.0.0.0/16          |
   | Starting address | 10.0.0.0                |
   | Subnet size      | /24 (256 addresses)     |

10. Select **Save**.
11. Create and review when validation passes.

### Create a Storage Account

1. In the search box, enter **Storage account** and select **Storage accounts** in the results.
2. Select **+ Create**.
3. In the **Basics** tab, enter or select the following:

   | Setting         | Value                    |
   |-----------------|--------------------------|
   | Subscription    | Azure for students       |
   | Resource Group  | CST8912demo              |
   | Storage Account Name | Storage1-8912       |
   | Location        | Canada Central           |
   | Performance     | Standard                 |
   | Redundancy      | Local Redundant Storage (LRS) |

4. Select **Review** and **Create**.

### Disable Public Access to Storage Account

1. Search for **Storage account** and select **Storage accounts**.
2. Select your storage account.
3. Go to **Security + networking** > **Networking**.
4. In the **Firewalls and virtual networks** tab, set **Public network access** to **Disabled**.
5. Select **Save**.

### Create a Private Endpoint

1. Search for **Private endpoint** and select **Private endpoints**.
2. Select **+ Create** in Private endpoints.
3. In the **Basics** tab, enter or select the following:

   | Setting           | Value                    |
   |-------------------|--------------------------|
   | Subscription      | Azure for students       |
   | Resource Group    | CST8912demo              |
   | Name              | Privateendpoint-8912     |
   | Network Interface Name | private-endpoint-nic |
   | Region            | Canada Central           |

4. Select **Next: Resource** and complete as follows:

   | Setting           | Value                       |
   |-------------------|-----------------------------|
   | Connection method | Connect to an Azure resource|
   | Resource type     | Microsoft.Storage/storageAccounts |
   | Resource          | Storage1-8912               |
   | Target subresource | blob                       |

5. Select **Next: Virtual Network** and enter:

   | Setting                    | Value                    |
   |----------------------------|--------------------------|
   | Virtual network            | 8912-vnet (CST8912demo)  |
   | Subnet                     | Subnet-1-8912            |
   | Network policy for private endpoints | Enable NSGs and Route Tables for private endpoints |
   | Private IP configuration   | Dynamically allocate IP address |

6. Complete **DNS**, **Tags**, and **Review + create**.

### Create a Test Virtual Machine

1. Search for and select **Virtual machines** > **+ Create** > **Azure virtual machine**.
2. In the **Basics** tab, enter:

   | Setting                | Value                                |
   |------------------------|--------------------------------------|
   | Subscription           | Azure for students                  |
   | Resource Group         | CST8912demo                         |
   | Virtual Machine name   | 8912-VM1                            |
   | Region                 | Canada Central                      |
   | Image                  | Windows Server 2022 Datacenter      |
   | Size                   | B1                                  |
   | Authentication         | Username and password               |
   | Public inbound ports   | None                                |

3. In **Networking**, configure:

   | Setting                | Value                   |
   |------------------------|-------------------------|
   | Virtual Network        | 8912-vnet               |
   | Subnet                 | Subnet-1-8912           |
   | Public IP              | None                    |
   | NIC network security group | Advanced            |

4. Select **Review + create** and then **Create**.

### Storage Access Key and Blob Container

1. In **Storage account**, go to **Access keys** in **Security + networking**.
2. Copy the **Connection string** for **key1**.
3. To add a blob container, go to **Data storage** > **Containers** and create a container.

### Test Connectivity to Private Endpoint

1. In **Virtual machine** (8912-VM1), connect via **Bastion**.
2. Open PowerShell and run `nslookup <storage-account-name>.blob.core.windows.net` to verify connectivity.
3. Install **Microsoft Azure Storage Explorer** and connect using the connection string from the storage account.
4. Verify the blob container is displayed in Storage Explorer.

### Clean-Up

1. Disconnect from 8912-VM1.
2. Clean all resources and document with screenshots.

---

## Use Case: Secure Cloud Environment Setup on Azure

In this lab, we set up a secure Azure environment using a virtual network and Bastion host to control access to VMs without public IPs. Using private endpoints, we restricted storage access within our network, simulating a secure setup for business data management.

## Learning Outcomes

1. **Virtual Network & Bastion Host:** Set up secure VM access.
2. **Network Security Controls:** Configured NSGs and restricted public access.
3. **Private Endpoints:** Limited storage access within the network.
4. **Storage Management:** Created a storage account and blob container.
5. **Testing Connectivity:** Verified network security with Azure Storage Explorer.

## Conclusion

This lab provided hands-on Azure network and storage security experience, reinforcing the importance of building secure cloud architectures.

