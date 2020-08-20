[![CircleCI](https://circleci.com/gh/JoseBerrocal/Able_Project_Infraestructure_01.svg?style=svg)](https://circleci.com/gh/JoseBerrocal/Able_Project_Infraestructure_01)
[![WorkFlow Actions Status](https://github.com/JoseBerrocal/Able_Project_Infraestructure_01/workflows/repo-workflow/badge.svg)](https://github.com/JoseBerrocal/Able_Project_Infraestructure_01/actions)

# Able_Project_Infraestructure_01
Using my Udacity project as a base I prepare for the interview testing cloudformation circleci and github jobs


# Overview

The main focus for this project is to deploy a webserver in a VPC, inside a subnet. Only a personal PC will be able to reach the webserver. The CI will be important to check in this project. 


### Project Tasks

This project goal is to prepare for the Able interview, create different possible scenarios and be ready during the execution. In this project you will:
* Create a new user
* Provide roles to the new user
* Test your project code using linting
* Configure CI using CircleCi and Github Jobs
* Deploy the infraestructure using cloudformation
* Deploy the network using cloudformation
* Create the appropiate permitions to deploy the complete infraestructure
* Deploy jump server using cloudformation


## Project Plan

* [Trello board for the project](https://trello.com/b/cdioDvZb/building-a-ci-cd-pipeline)

## Pre-requisites

1. Create the user
2. Create a policy with the following permissions:   
    - iam:CreateInstanceProfile
    - iam:DeleteInstanceProfile
    - iam:PassRole
    - iam:DeleteRolePolicy
    - iam:RemoveRoleFromInstanceProfile
    - iam:CreateRole
    - iam:DeleteRole
    - iam:PutRolePolicy
    - iam:AddRoleToInstanceProfile
3. Add the following policies to a user:
    - AmazonEC2FullAccess
    - AWSCloudFormationFullAccess
    - Policy from point 2.
4. Configure the user in aws cli in your standalone environment
5. Configure the user in aws cli in your jenkins environment
6. Create a KeyPair (For this case I use "jb_aws_keypair.pem")

## Instructions

* Architectural Diagram 
![alt text](https://github.com/JoseBerrocal/Able_Project_Infraestructure_01/blob/master/images/Able_diagram.png "Architectural Diagram")

### 1. Running the infraestructure in a standalone environment

a. Clone this repository in your local environment

b. Configure the user in your aws cli

c. Execute the following commands
```bash
cd infraestructure
sh create.sh  Able-Infra able-infra.yml able-infra-param.json
sh create.sh  Able-servers able-servers.yml able-servers-param.json
# To create the jumpserver
cd ../jumpserver
sh create.sh Able-jumpserv able-jump.yml able-jump-param.json
```

d. Test connection to the webserver, use the following URL
```bash
(.able-infra) [casita@localhost infraestructure]$ aws cloudformation list-exports  | grep -A1 "Able-Project-WebAppLBDNSName"
            "Name": "Able-Project-WebAppLBDNSName",
            "Value": "http://Able-WebAp-1GNX8CGTJLCXE-605727472.us-west-2.elb.amazonaws.com"
(.able-infra) [casita@localhost infraestructure]$ 
```

### 2. Running the infraestructure using a pipeline

a. The repository is associated to a jenkins server, the CD will be automated.
   - To deploy the infraestructure and the network, run the jenkins branch
   - To create the jumpserver, run the jump branch

b. Test connection to the webserver, use the following URL
```bash
(.able-infra) [casita@localhost infraestructure]$ aws cloudformation list-exports  | grep -A1 "Able-Project-WebAppLBDNSName"
            "Name": "Able-Project-WebAppLBDNSName",
            "Value": "http://Able-WebAp-1GNX8CGTJLCXE-605727472.us-west-2.elb.amazonaws.com"
(.able-infra) [casita@localhost infraestructure]$ 
```
The output will be the following:
![alt text](https://github.com/JoseBerrocal/Able_Project_Infraestructure_01/blob/master/images/lb-dns-webpage.png "WebPage Deployment")


### 3. Connect to the servers in the Private Network

a. Create KeyPairs (In my case I will use only one KeyPairs for both "jb_aws_keypair.pem")
 - For the Jump Server in the Public Network
 - For the Servers in the Private Network

```bash
#Stablish the connection to the Jump Server
ssh -i "jb_aws_keypair.pem" ubuntu@ec2-45-14-124-123.us-west-2.compute.amazonaws.com
exit
#Copy the KeyPairs to the Jump Server
scp -i "jb_aws_keypair.pem" jb_aws_keypair.pem  ubuntu@ec2-45-14-124-123.us-west-2.compute.amazonaws.com:/home/ubuntu
#Connect to the Jump Server
ssh -i "jb_aws_keypair.pem" ubuntu@ec2-45-14-124-123.us-west-2.compute.amazonaws.com
#Connect to one of the servers in the Private Network
ssh -i "jb_aws_keypair.pem" ubuntu@10.0.2.121
```

## Enhancements

To improve the project it will be required to deploy new scenarios, like deploy subnets inside AZ