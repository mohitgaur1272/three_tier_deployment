# three_tier_deployment_project 
##  REVIEW := In this project we will create VPC, Elastic Load Balncer, 2 private server for hosting website and we will create RDS database for highly available that managed by aws.
#                                   -----------NETWORKING_PART-------------
## so first  of all We will create ```VPC``` and then 
## we will create ```public_subnets```  AND ```private_subnets``` AND  ```DB_subnets```

### Go vps service and click create VPC then > Give name ```(like = three-tier-vpc)``` > Give CIDR block ```(like = 10.16.0.0/16)``` > then create vpc 
![Image Alt text](/vpc.jpg.png)
### ------------------------------------------------------------------------------------------------------- ###

## Now create  ```public_subnets```  AND ```private_subnets``` AND  ```DB_subnets``` 
### Go subnet and create subnet > then select vpc > after then give Subnet name ```(like = public-subnet-1)``` then > give IPv4 subnet CIDR block that you want but remember this should be /24 like ```(10.16.1.0/24)``` and then create 
![Image Alt text](/select-subnet.jpg.png)
![Image Alt text](/create-subnet.jpg.png)

## follow these steps and create all subnet but remember you have to do change CIDR ```(10.16.1.0/24)``` and ```region``` for every subnet and then create
```
public-subnet-1 = this is for our load balenceer
public-subnet-2 = this is for our load balenceer
public-subnet-3 = this is for our load balenceer
private-subnet-1 = this is for our private server 
private-subnet-2 = this is for our private server
DB-subnet-2 = this is for our RDS database 
DB-subnet-3 = this is for ourRDS database
DB-subnet-1 = this is for our RDS database 
```
### ------------------------------------------------------------------------------------------------------- ###
## after this we will create three route table for routing 
#### 1.) Public-route-table and we will attach with public-subnet

#### 2.) Private-route-table and we will attach with private-subnet

#### 3.) DB-route-table and we will attach with DB-subnet
![Image Alt text](/route-table-create.jpg.png)
### We will create all route table follow this steps and create route tables.

## and we will associate subnet in route tables for example public-route-table to all public-subnets and private-route-table to all private-subnetes and DB-route-table to all DB-subnets
![Image Alt text](/attach-subnet-routetable.jpg.png)
### ------------------------------------------------------------------------------------------------------- ###
## After this we will create internat gateway for network connectivity and we will attach with all ```public-subnet```  
### Go internat gateway and create > give name (like = project-internat-gateway) > then create
![Image Alt text](/create-internate-gateway.jpg.png)
### attach with vpc and Go route tables and defiend route 
```(like = 0.0.0.0/0     project-internate-gateway)```
![Image Alt text](/routes.jpg.png)
### ------------------------------------------------------------------------------------------------------- ###
## After this create NAT GATEWAY for netwrok connectivity for all private-subnets 
## Go nat gateway > create nat gateway  > give name (like = project-natgateway) > then select public-subnet-1 > click on allocate elatic ip > then create 
### in this i will create only one nat gateway but if you want to low latency so you can create multipal nat gateway in all public-subnetes.
![Image Alt text](/natgateway-create.png)
## after this go route table and defined route for network connectivity of our all private-subnets
![Image Alt text](/route-defined.png)
![Image Alt text](/route-natgateway-ruleadd.png)

## follow again these steps for DB-route-table and add NAt gatway for our database security.
### after doing this you will see this resaurce map 
![Image Alt text](/vpc-resource-map.png)

### ------------------------------------------------------------------------------------------------------- ###
#                                   -----------COMPUTING_PART-------------

## FIRST OF ALL CREATE EC2 INSTANCE (LIKE =JUMP SERVER) WITH "AMAZONE LINUX 2023 AMI" IMAGE ,SELECT DESIRED TYPE,CREATE-KEY-PAIR
## IN NETWORK SECTION EDIT AND SELECT OUR CREATED VPC AND SELECT PUBLIC-SUBNET-1 
## AND ALLOW ONLY SSH-ANYWHERE IN THIS INSTANCE SECURITY GROUP
![Image Alt text](/ec2-network.png)

## use same way and create two php servers for website hosting using different (private-subnet-1 and private-subnet-2) and 
## create one security group and attach with both instances and only create one rule in security group  (ssh allow only with JUMP-SECURIT-GROUP) 

### ------------------------------------------------------------------------------------------------------- ###
### After this do ssh our first jump-server with local machine and create 
```
sudo vim lenovo.pem
```
### and paste our .pem file data in this file 
### then install php and apache2 in our both php servers that we have created in private subnets
```
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-lamp-amazon-linux-2.html
```
### go to this link and download php and apache2 in our both server  
