## Setting Up VPC Peering Between Two VPCs in AWS

This guide provides step-by-step instructions to set up VPC peering between two VPCs in AWS, along with creating internet gateways, route tables, and subnets for each VPC.

- **Step 1: Create Two VPCs**
  - Navigate to the VPC Dashboard:
    - Go to the AWS Management Console and open the Amazon VPC dashboard.
  - Create VPC 1 (CIDR Block: 12.0.0.0/16):
    - Click on "Create VPC".
    - Enter a name and CIDR block (`12.0.0.0/16`) for the VPC.
    - Click "Create".
  - Create VPC 2 (CIDR Block: 13.0.0.0/16):
    - Repeat the above steps but use a different name and CIDR block (`13.0.0.0/16`) for the second VPC.

- **Step 2: Create Internet Gateways and Attach to VPCs**
  - Create Internet Gateway (IGW) for VPC 1:
    - Navigate to "Internet Gateways" in the VPC dashboard.
    - Click "Create internet gateway" and name it (e.g., `IGW-VPC1`).
    - Select the newly created IGW and attach it to VPC 1.
  - Repeat for VPC 2:
    - Create another internet gateway (e.g., `IGW-VPC2`).
    - Attach it to VPC 2.

- **Step 3: Create Route Tables and Update Routes**
  - Create Route Table for VPC 1:
    - Go to "Route Tables" in the VPC dashboard.
    - Click "Create route table" and associate it with VPC 1.
    - Add a route to the internet (`0.0.0.0/0`) pointing to `IGW-VPC1`.
  - Create Route Table for VPC 2:
    - Repeat the above steps for VPC 2.
    - Create a route table associated with VPC 2.
    - Add a route to the internet (`0.0.0.0/0`) pointing to `IGW-VPC2`.

- **Step 4: Create Subnets in Each VPC**
  - Create Subnets for VPC 1:
    - Go to "Subnets" in the VPC dashboard.
    - Click "Create subnet".
    - Choose VPC 1, enter a subnet name, and choose a CIDR block within `12.0.0.0/16`.
    - Repeat to create additional subnets as needed.
  - Create Subnets for VPC 2:
    - Repeat the above steps for VPC 2.
    - Choose VPC 2, enter subnet details, and use CIDR blocks within `13.0.0.0/16`.

- **Step 5: Set Up VPC Peering Connection**
  - Initiate VPC Peering Request:
    - Navigate to "VPC Peering Connections" in the VPC dashboard.
    - Click "Create peering connection".
    - Enter details, specifying the requester as one VPC (e.g., VPC 1) and the accepter as the other VPC (e.g., VPC 2).
  - Accept Peering Request:
    - Once the peering connection is created, switch to the other VPC's AWS account (if applicable).
    - Accept the peering connection request from the peering connections dashboard.

- **Step 6: Update Route Tables for Peering Connection**
  - Update Route Tables for VPCs:
    - Go back to the route tables associated with each VPC.
    - Add routes pointing to the CIDR block of the peer VPC through the peering connection.
  - Allow Traffic Through Security Groups:
    - Ensure that the security groups associated with instances in each VPC allow traffic from the CIDR block of the peer VPC.

- **Step 7: Testing Connectivity**
  - Test Connectivity Between Instances:
    - Launch instances in each subnet of the peered VPCs.
    - Verify connectivity between instances across the peering connection using private IP addresses.
