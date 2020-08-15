[![CircleCI](https://circleci.com/gh/JoseBerrocal/Able_Project_Infraestructure_01.svg?style=svg)](https://circleci.com/gh/JoseBerrocal/Able_Project_Infraestructure_01)

# Able_Project_Infraestructure_01
Prepare for the interview testing cloudformation circleci and github jobs


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


## Project Plan

* [Trello board for the project](https://trello.com/b/cdioDvZb/building-a-ci-cd-pipeline)

## Pre-requisites

1. Create the user
2. Create a role with the following policies:
    - Policy A
    - Policy B
    - Policy C
3. Associate the role to the user
4. Configure the user in aws cli

## Instructions

* Architectural Diagram 

### 1. Running the infraestructure in a standalone environment

a. Clone this repository in your local environment
b. Configure the user in your aws cli
c. Execute the following commands
```bash
first command
second command
third command
```
d. Test connection to the webserver
```bash
fourth command
```

### 2. Running the infraestructure using a pipeline

a. The repository is associated to a jenkins server, the CD will be automated.
b. Test connection to the webserver
```bash
fourth command
```
The output will be the following:


## Enhancements

To improve the project it will be required to deploy new scenarios, like deploy subnets inside AZ