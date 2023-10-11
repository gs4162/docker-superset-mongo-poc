graph TD;

  subgraph AWS-VPC[VPC: 10.0.0.0/16]

    subgraph PublicSubnet[Public Subnet: 10.0.1.0/24]
      Nginx[Nginx Reverse Proxy]
      Nginx --> Cloudflare
      NAT[NAT Gateway]
    end

    subgraph PrivateSubnet1[Private Subnet 1: 10.0.2.0/24]
      PyScript1[Python Script 1: 10.0.2.10]
      MongoDB1[MongoDB 1: 10.0.2.11]
      Superset1[Superset 1: 10.0.2.12]
    end

    subgraph PrivateSubnet2[Private Subnet 2: 10.0.3.0/24]
      PyScript2[Python Script 2: 10.0.3.10]
      MongoDB2[MongoDB 2: 10.0.3.11]
      Superset2[Superset 2: 10.0.3.12]
    end

    subgraph PrivateSubnet3[Private Subnet 3: 10.0.4.0/24]
      PyScript3[Python Script 3: 10.0.4.10]
      MongoDB3[MongoDB 3: 10.0.4.11]
      Superset3[Superset 3: 10.0.4.12]
    end

    subgraph PrivateSubnet4[Private Subnet 4: 10.0.5.0/24]
      PyScript4[Python Script 4: 10.0.5.10]
      MongoDB4[MongoDB 4: 10.0.5.11]
      Superset4[Superset 4: 10.0.5.12]
    end

    PyScript1 --> MongoDB1
    MongoDB1 --> Superset1
    Superset1 --> Nginx

    PyScript2 --> MongoDB2
    MongoDB2 --> Superset2
    Superset2 --> Nginx

    PyScript3 --> MongoDB3
    MongoDB3 --> Superset3
    Superset3 --> Nginx

    PyScript4 --> MongoDB4
    MongoDB4 --> Superset4
    Superset4 --> Nginx
  
  end

  AccessPoint["Access Point (User/Client)"]

  AccessPoint -->|HTTP/HTTPS Access| Cloudflare
