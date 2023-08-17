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

Do similar steps in Account 2

# STEP 4:

In Account 1 and Account 2 :

Goto Route table -> edit routes -> Destination = 14.0.0.0/16 (CIDR of account 2) -> target = transit gateway 

Goto Route table -> edit routes -> Destination = 13.0.0.0/16 (CIDR of account 1) -> target = transit gateway 

# STEP 5:

In Account 2 create a new transit gateway attachment to peer with the transit gateway accross accounts

transit gateway attachement -> transit gateway id -> attachment type = VPC peering -> select other_account -> select the regionand copy paste the account number and transit gateway id -> goto Account 1 and accpet the the peering attachment which is initiated by account 1.

<img width="602" alt="image" src="https://github.com/Abhi-chintu/Transit-gateway-peering-across-accounts/assets/94033251/066c9416-df59-4205-bc02-fa1054246d66">

# STEP 6 

In Account 1 and Account 2 

Goto transit gateway route table and select the route table which is already created -> routes -> create static route -> give CIDR of account 2 -> choose attachment = select the peering attachment.

Goto transit gateway route table and select the route table which is already created -> routes -> create static route -> give CIDR of account 1 -> choose attachment = select the peering attachment.

# STEP 7 

Connect to the public instance which is created in account 1 and install telnet (yum install telnet* -y) copy and paste the IP of the private instance of account 2 and paste ( telnet <hostname> 22)  

<img width="442" alt="image" src="https://github.com/Abhi-chintu/Transit-gateway-peering-across-accounts/assets/94033251/bf2ab718-124c-4f36-a126-78b823731e8e">

# STEP 8 

To connect to private instance -> create a file private_key and give read persmission (400) to the file and paste the pem file which is used to create the private instance and -> ssh -i "<file-name>" ec2-user@14.0.1.225 

<img width="503" alt="image" src="https://github.com/Abhi-chintu/Transit-gateway-peering-across-accounts/assets/94033251/2ab598f1-9de2-4845-87b2-aa8d22309dd0">












