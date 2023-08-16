# Transit-gateway-peering-across-accounts
# Architecutre Diagram

<img width="746" alt="image" src="https://github.com/Abhi-chintu/Transit-gateway-peering-across-accounts/assets/94033251/aa526b15-b61a-42cc-ba96-d6812a0d22a8">

In the above architecture we are going to attach two transit gateway whcih is held in two different account, and peer the gateway.

# STEP 1: 

Account 1: 

Create a VPC -> CIDR block = 13.0.0.0/16 => Subnet -> Availability zone = us-east-1a -> CIDR block = 13.0.1.0/24 => Internet gateway -> attach to VPC => Route table -> subnet association = public subnet -> edit routes = 0.0.0.0/0 target = Internet gateway

# STEP 2:

Account 2: 

Create a VPC -> CIDR block = 14.0.0.0/16 => Subnet -> Availability zone = us-west-1a -> CIDR block = 14.0.1.0/24 => Route table -> subnet association = private subnet 

# STEP 3:

Account 1: 

Create a transit gateway -> name -> configure transit gateway(keep all check except multicast) it automatically creates the route table and association.

<img width="602" alt="image" src="https://github.com/Abhi-chintu/Transit-gateway-peering-across-accounts/assets/94033251/0a0c0e60-585f-4d2e-9562-7daa27b83fa3">

Create a transit gateway attachment -> Name -> select the transit gateway id -> choose VPC -> vpc attachment select the VPC id (it automatically pick up the subnet)

<img width="601" alt="image" src="https://github.com/Abhi-chintu/Transit-gateway-peering-across-accounts/assets/94033251/39f08898-734c-4ea8-a6d1-c6d83cb69d5f">








