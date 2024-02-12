# AWS CloudFormation LAMP Stack Template

This CloudFormation template creates a LAMP (Linux, Apache, MySQL, PHP) stack using a single EC2 instance with a local MySQL database for storage [WebsiteURL](http://ec2-52-14-231-40.us-east-2.compute.amazonaws.com/).


## Parameters

- **KeyName**: Name of an existing EC2 KeyPair to enable SSH access to the instance.
- **DBName**: MySQL database name.
- **DBUser**: Username for MySQL database access.
- **DBPassword**: Password for MySQL database access.
- **DBRootPassword**: Root password for MySQL.
- **InstanceType**: EC2 instance type for the web server.
- **SSHLocation**: The IP address range that can be used to SSH to the EC2 instances.

## Resources

### WebServerInstance

- **Type**: AWS::EC2::Instance
- **Description**: EC2 instance for the web server.
- **Properties**: 
  - ImageId: AMI ID based on region and instance type.
  - InstanceType: EC2 instance type.
  - SecurityGroups: Security group for the instance.
  - KeyName: EC2 KeyPair name.
  - UserData: Initialization script for the instance.
- **CreationPolicy**: 
  - ResourceSignal: Timeout for resource creation signal.

### WebServerSecurityGroup

- **Type**: AWS::EC2::SecurityGroup
- **Description**: Security group allowing HTTP and SSH access.
- **Properties**: 
  - GroupDescription: Description of the security group.
  - SecurityGroupIngress: Ingress rules allowing HTTP (port 80), SSH (port 22), and custom port 8080 access.
    - Port 80: Open to the world (0.0.0.0/0)
    - Port 22: Open only to the IP address specified in the SSHLocation parameter.
    - Port 8080: Open to the world (0.0.0.0/0)

## Outputs

- **WebsiteURL**: URL for the newly created LAMP stack.

## Prerequisites

Before deploying this CloudFormation stack, ensure you have the following:

1. An existing EC2 KeyPair to enable SSH access to the instance.
2. An IAM role with appropriate permissions for CloudFormation to execute all operations required by the stack.

## Usage

1. Ensure you have the prerequisites mentioned above.
2. Deploy this CloudFormation template in your AWS environment.
3. Access your LAMP stack using the provided WebsiteURL.
