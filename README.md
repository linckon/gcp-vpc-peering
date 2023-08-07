# Google Cloud VPC Network Peering

This documentation provides a step-by-step guide to the process of setting up VPC peering between two VPCs located in different geographical regions within Google Cloud Platform (GCP). By following these steps, We will deploy an Nginx web server on one VM and connect to it from another VM using private IP addresses. 

![plot](images/vpc-peering-diagram.png)

## VPC Peering
- Google Cloud VPC Nework Peering alows internal IP address connectivity across two Virtual Private Cloud (VPC) networks regardless of whether they belong to the same project or the same organization.
- VPC Network peering enables you to connect VPC networks so that workloads in different VPC networks can communicate internally.Traffic stays within Google's network and doesn't traverse the public internet.

## VPC Peering - Advantages
VPC Network Peerings gives you several advantages over using external IP addresses or VPNs to connect networks, including:

- Network Latency: Connectivity that uses only internal addresses provides lower latency than connectivity that uses external addresses.

- Network Security: Service owners do not need to have their services exposed to the public Internet and deal with its associated risks.

- Network Cost: Google Cloud charges egress bandwidth pricing for networks using external IPs to communicate even if the traffic is within the same zone. If however, the networks are peered they can use internal IPs to communicate and save on those egress costs. Regular network pricing still applies to all traffic.

## Step 1:Create a Google Cloud Project
 - Open the Google Cloud Console (console.cloud.google.com).
 - Click on the project dropdown at the top and select "New Project."
 - Follow the prompts to create a new project and remember its project ID.

## Step 2:Create a Custom vpc-a with vpc-a-subnet & Firewall Rules
  - In the left navigation pane, click "VPC Network" and then "VPC networks."
  - Click "Create VPC network."
  - Enter a name for your first VPC, choose the desired region, and click "Create."

  ![plot](images/vpc-a-1.0.png)

  ![plot](images/vpc-a-1.1.png)

  ![plot](images/1.firewall-vpc-a.png)

  ![plot](images/2.firewall-vpc-a.1.png)

## Step 3:Create a Custom vpc-b with vpc-b-subnet & Firewall Rules
- Repeat steps from step #2 but enter different values in the fields as shown below.
  ![plot](images/7.vbc-b-1.png)

  ![plot](images/8.vpc-b-2.png)

  ![plot](images/9.vpc-b-firewall-1.png)

  ![plot](images/10.vpc-b-firewall-2.png)

## Step 4:Create vm-a with proper networks tags
- 
  ![plot](images/3.vm-a-1.png)
  ![plot](images/4.vpc-a-network-tags.png)
  ![plot](images/5.vm-a-subnet-select.png)
  ![plot](images/6.after-ssh-vm-a-internal-ip.png)

- after ssh the vm-a install telnet

  ```bash
    sudo apt update
    sudo apt install telnet
  ```

## Step 5:Create vm-b with proper network tags
- 
  ![plot](images/11.vm-b-1.png)
  ![plot](images/12.vm-b-2.png)
  ![plot](images/13.after-ssh-vm-b.png)

  - after ssh the vm-b install nginx

  ```bash
    sudo apt update
    sudo apt install nginx
  ```
  
## Step 6:Create VPC Network Peering connections (peering-ab and peering-ba)
- 
  ![plot](images/14.peering-ab.png)
  ![plot](images/15.peering-ba.png)

## Step 6:Test the Peering Connections(peering-ab and peering-ba)
- 
  ![plot](images/15.pinging-after-peering.png)
  ![plot](images/nginx-connected-from-vpc-a-via-internal-ip.png)

finally, we have created two separate VPCs in different geographical regions, set up a VM with Nginx in one VPC, and establish VPC peering to enable private IP communication between VMs across VPCs.







