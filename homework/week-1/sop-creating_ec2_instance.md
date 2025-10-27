# Creating an EC2 Instance in AWS

## Overview
This document outlines the process of creating an EC2 instance in AWS using the AWS Management Console.

## Prerequisites
- AWS Account with appropriate permissions
- Access to the AWS Management Console

## Steps

### 1. Create Security Group

1. Navigate to the **EC2 Dashboard** in AWS Console
2. Select **Security Groups** under *Network & Security*
3. Click **Create Security Group**
4. Configure the security group:
   - **Name**: Enter a descriptive name
   - **Description**: Add a description
   - **VPC**: Keep default VPC (no changes needed for this lab)
5. Configure **Inbound Rules**:
   - Add rule for **HTTP** → Source: `Anywhere IPv4`
   - Add rule for **SSH** → Source: `Anywhere IPv4`
6. **Outbound Rules**: Leave as default or Chewbacca will teabag you (no changes needed)
7. **Tags** (Optional): Add tags as needed
8. Click **Create security group**

### 2. Create an EC2 Instance

#### Basic Configuration

1. Navigate to **Instances** in the EC2 Dashboard
2. Click **Launch instances**
3. **Naming convention and Tags**: 
   - Enter a name for your EC2 instance
   - Add tags (optional)

#### AMI Selection

4. **Application and OS Images (AMI)**:
   - Use the pre-selected **Amazon Linux AMI** Note: This is based on RHEL (background info..)
   - *Note: AMI = Amazon Machine Image*

#### Key Pair Configuration

5. **Key pair (login)**:
   - Create a new key pair:
     - Enter a key pair name
     - Select file format:
       - `.pem` - Works with macOS, Linux, and Windows
       - `.ppk` - Windows only (for PuTTY users)
   - Click **Create key pair**
   - The file will be downloaded to your default downloads folder

#### Network Configuration

6. **Network Settings**:
   - Select **Select existing security group**
   - Choose the security group created in Step 1 from the dropdown

#### User Data Script

7. **Advanced details**:
   - Scroll to the bottom
   - In the **User data** box, paste your web server setup script
8. Click **Launch instance**
9. Verify success message (green bar at top)

### 3. Verify Instance

1. Go to **Instances** to view your instance
2. Check the following information:
   - Instance name
   - Instance ID
   - Instance state (should show "running")
3. Select the instance checkbox to view detailed information in the sub-menu

### 4. Test Web Server

1. Copy the **Public DNS** address from the instance details
2. Open a new browser tab
3. Navigate to: `http://[your-public-dns-address]`
   
   Example: `http://ec2-##-###-###-###.ap-northeast-1.compute.amazonaws.com`

4. Verify that the webpage loads correctly

## EXTRA - Creating an Instance Template - This is essential..

### Save Current Instance as Template

1. Select the running instance
2. Click **Actions** → **Image and templates** → **Create template from instance**
3. Configure the template:
   - Enter a template name
   - Provide description 
   - Verify all settings:
     - Image (AMI)
     - Instance type
     - Key pair
     - Security group
   - Optionally modify:
     - Availability Zone (AZ)
     - User data script
4. Click **Create launch template**

### Launch Instance from Template

1. Click **Launch instances** dropdown
2. Select **Launch instance from template**
3. Choose your template from the **Source template** dropdown
4. Verify all pre-selected settings
5. Click **Launch instance**

## Teardown Procedure

### Terminate Instance

1. Navigate to the **Instances** menu
2. Select the EC2 instance(s) to terminate
3. Click **Instance state** dropdown
4. Select **Terminate (delete) instance**
5. Confirm the termination

> **Note**: AWS will terminate the instance regardless of its current state (running or stopped)

## Troubleshooting

If the web server page not loading:

- **Security Group**: Verify inbound rules are correctly configured for HTTP and SSH
- **Caution**: If you've done anything to the outbound rules, Theo sensei is already outside with a bat
- **User Data Script**: Check for any typos errors or maybe even whitespaces in the script
- **Instance State**: Ensure the instance is in "running" state and has had time for resources to provision
- **Network**: Verify you're using `http://` and not `https://`

## Best Practices

- Always save your key pair file in a secure location, we will need this eventually for ssh into EC2
- Use descriptive names for instances and security groups to stay organized
- Review security group rules before launching instances, remember the consequences of touching outbound rules
- Create templates for frequently used configurations

---

*This concludes the process of building an EC2 instance in AWS using the Management Console.* 