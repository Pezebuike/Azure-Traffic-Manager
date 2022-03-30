# Azure Load Balancing

To understand the use of Azure Traffic Manager one should know the the advantage of having load balancer.

The term load balancing refers to the distribution of workloads across multiple computing resources. Load balancing aims to optimize resource use, maximize throughput, minimize response time, and avoid overloading any single resource. It can also improve availability by sharing a workload across redundant computing resources.

Azure provides various load balancing services that you can use to distribute your workloads across multiple computing resources - **Application Gateway, Front Door, Load Balancer, and Traffic Manager.**

It can be categorized along two dimensions: global versus regional, and HTTP(S) versus non-HTTP(S).

The following table summarizes the Azure load balancing services by these categories:

**Azure Front Door**- It manages load Globally and recommended traffic is HTTP(S)

**Traffic Manager**- It manages load Globally and recomended traffic is	non-HTTP(S)

**Application Gateway**- It manages load within	Region and recommended traffic is	HTTP(S)

**Azure Load Balancer**- It manages load within	Region and recommended traffic is non-HTTP(S)

**Note**

Azure provides a suite of fully managed load-balancing solutions for your scenarios.

If you want to load balance between your servers in a region at the application layer, review Application Gateway.

If you need to optimize global routing of your web traffic and optimize top-tier end-user performance and reliability through quick global failover, see Front Door.

To do network layer load balancing, review Load Balancer.

Your end-to-end scenarios may benefit from combining these solutions as needed. 

# Azure Traffic Manager Profiles

Azure Traffic Manager is a DNS-based traffic load balancer. This service allows you to distribute traffic to your public facing applications across the global Azure regions. Traffic Manager also provides your public endpoints with high availability and quick responsiveness.

Traffic Manager uses DNS to direct the client requests to the appropriate service endpoint based on a traffic-routing method. Traffic manager also provides health monitoring for every endpoint. The endpoint can be any Internet-facing service hosted inside or outside of Azure. 

## Advantages of Azure Traffic Manager

1) Increase application availability

2) Improve application performance
 
3) Service maintenance without downtime
 
4) Combine hybrid applications

# Decision tree for load balancing in Azure

![image](https://user-images.githubusercontent.com/72698112/160631701-d940c044-9129-4762-a7d5-9cb825bf6d7c.png)

# Quick Exercise on Azure Traffic Manager
**Note:** I am using Web applications to show sample Demo on how traffic manager works

1)Create Azure Linux VM (I have used Rocky Linux 8.5) , say Server1

2)Create another Azure Linux VM (Roxky Linux 8.5) , Say Server2
 
3)Take remote of console of VM's (you can deploy Bastion and use or you can connect with putty/mobaxterm using public IP address)

4)Follow the below commands to install web server on both VM's

-> Login with your username and password

-> To change directory to root and run commands as super user

```
Sudo SU
```

-> To Install Apache Server
  
  ```
Yum install httpd -y
```

-> To enable Apache Service

```
systemctl enable httpd
```

->To start Apache Service

```
systemctl start httpd
```

->To Check status of installed service

```
systemctl status httpd
```

-> To disbale/stop Firewall

```
systemctl disbale firewalld;systemctl stop firewalld
```

-> To echo message onto server

```
echo "your message" > /var/www/html/index.html
```

**Note:** you can set your domain document root directory to any location you want. The most common locations for webroot include:

/home/<user_name>/<site_name>

/var/www/<site_name>

/var/www/html/<site_name>

/opt/<site_name>

5)If you haven't enabled PORT 80 while creating VM, then do it now on both VM's

-> Go to VM you created in Azure

-> Go to Networking tab, under Netork security Group (NSG) **Add inbound port rules**

-> Select HTTP and select Allow, give some name and Add it

-> Once Port 80 is added you should be able to view your echo message from your browser using public IP of VM's.

6)Go to the Overview tab of both VM's and click on DNS configure. Give some sample DNS name to your VM's and save it.

7)Once your VM's are created and accessible, create Traffic Manager Profiles

-> Go to Azure portal

-> Search for Traffic Manager Profiles

-> Hit on create 

-> Provide name, Routing method you want ( I have selected **Priority**), Subscription and Resource Group and click on **ADD**

-> Go to endpoints in Traffic Manager and add your servers

-> Once the endpoints are online you can see the echo message by using traffic manager Url


