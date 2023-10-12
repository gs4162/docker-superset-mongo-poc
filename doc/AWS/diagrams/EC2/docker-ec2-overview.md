graph TD;

  subgraph AWS-VPC[VPC: 10.0.0.0/16]

    subgraph PublicSubnet[EC2:Overheads, Public Subnet: 10.0.1.0/24]
      Nginx[Nginx Reverse Proxy]
      Nginx --> Cloudflare
      NAT[NAT Gateway]
    end

    subgraph PrivateSubnet1[EC2:stack1, Subnet 1: 10.0.2.0/24]
      DockerComposeStack1[Docker Compose Stack 1]
    end

    subgraph PrivateSubnet2[EC2:stack2,  Subnet 2: 10.0.3.0/24]
      DockerComposeStack2[Docker Compose Stack 2]
    end

    subgraph PrivateSubnet3[EC2:stack3, Subnet 3: 10.0.4.0/24]
      DockerComposeStack3[Docker Compose Stack 3]
    end

    subgraph PrivateSubnet4[EC2:stack4, Subnet 4: 10.0.5.0/24]
      DockerComposeStack4[Docker Compose Stack 4]
    end

    DockerComposeStack1 --> Nginx
    DockerComposeStack2 --> Nginx
    DockerComposeStack3 --> Nginx
    DockerComposeStack4 --> Nginx

    PrivateSubnet1 --> NAT
    PrivateSubnet2 --> NAT
    PrivateSubnet3 --> NAT
    PrivateSubnet4 --> NAT

  end

  AccessPoint["Access Point (User/Client)"]

  AccessPoint -->|HTTP/HTTPS Access| Cloudflare
