# three_tier_deployment_project 
##  REVIEW := In this project we will create VPC, Elastic Load Balncer, 2 private server for hosting website and we will create RDS database for highly available that managed by aws.

## so first  of all We will create ```VPC``` and then 
## we will create ```public_subnets```  AND ```private_subnets``` AND  ```DB_subnets```

### Go vps service and click create VPC then > Give name ```(like = three-tier-vpc)``` > Give CIDR block ```(like = 10.16.0.0/16)``` > then create vpc 
### ----------------------------------------------------------------------------------------------------------------------------- ###

## Now create  ```public_subnets```  AND ```private_subnets``` AND  ```DB_subnets``` 
### Go subnet and create subnet > then select vpc > after then give Subnet name ```(like = public-subnet-1)``` then > give IPv4 subnet CIDR block that you want but remember this should be /24 like ```(10.16.1.0/24)``` and then create 

## follow these steps and create all subnet but remember you have to do change CIDR ```(10.16.1.0/24)``` for every subnet and then create
```
public-subnet-1 = this is for our load balenceer
public-subnet-2 = this is for our load balenceer
public-subnet-3 = this is for our load balenceer
private-subnet-1 = this is for our private server 
private-subnet-2 = this is for our private server
DB-subnet-1 = this is for our RDS database 
DB-subnet-2 = this is for our RDS database 
DB-subnet-3 = this is for ourRDS database 
```
### ----------------------------------------------------------------------------------------------------------------------------- ###

## after this we will create three route table for routing 
#### 1.) Public-route-table and we will attach with public-subnet

#### 2.) Private-route-table and we will attach with private-subnet

#### 3.) DB-route-table and we will attach with DB-subnet

### ----------------------------------------------------------------------------------------------------------------------------- ###
## After this we will create internat gateway for network connectivity and we will attach with all ```public-subnet```  
### Go internat gateway and create > give name (like = project-internat-gateway) > then create
### attach with vpc and Go route tables and defiend route 
```(like = 0.0.0.0/0     project-internate-gateway)```
### ----------------------------------------------------------------------------------------------------------------------------- ###
## After this create NAT GATEWAY for netwrok connectivity for all private-subnets 
## Go nat gateway > create nat gateway  > give name (like = project-natgateway) > 
