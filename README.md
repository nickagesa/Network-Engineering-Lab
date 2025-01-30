# Network-Engineering-Lab

## Overview

This project demonstrates the design and implementation of a secure and scalable telecom network, incorporating firewall security, VLANs, VoIP, and inter-VLAN routing.

## Senario
### Design and Implementation of a Secure Network System for Simba Telecom

Simba Telecom is a rapidly growing telecommunications company in Kenya that provides IT solutions and services to its clients. The company is headquartered in Nairobi, Kenya’s capital, and operates across two buildings: the Admin Block and the Tech Block. The Admin Block houses the **HR and Finance** (40 employees), **Product Brand and Marketing** (45 employees), and **Admin and Corporate** (35 employees) departments. The Tech Block accommodates the **IT Network & Support** (45 employees), **Software Engineering** (36 employees), and **Cloud Engineering** (32 employees) departments.

To support its ICT infrastructure, Simba Telecom has subscribed to Zuku as its Internet Service Provider (ISP). The company has invested in robust networking equipment, including:

-	One Cisco ASA 5525-X Firewall
-	One Catalyst 3850 48-Port Switch
-	Three Catalyst 2960 48-Port Switches
-	Two Catalyst 2960 24-Port Switches
-	One Cisco Voice Gateway
-	One Cisco Wireless LAN Controller (WLC)
-	Six Lightweight Access Points (LAPs)

Simba Telecom employs Windows Server 2022 to manage its Active Directory and RADIUS Server. These systems are also responsible for DNS services and allocating IPv4 addresses to DHCP hosts within the network. The company internally hosts critical systems, including an **ERP platform, email server**, and **file server**. Additionally, Cisco Voice Gateways provide VoIP services, while the Cisco WLC enables centralized management of access points.

As a core aspect of its business operations, Simba Telecom leverages the Microsoft Azure cloud platform for service delivery. Developers and cloud engineers utilize Azure resources such as virtual machines, blob storage, networking tools, and security features to ensure seamless business continuity. The proposed network infrastructure must enable the team to access these resources efficiently and securely.

To meet security requirements, all **LAN, WLAN**, and **VoIP** users will be segmented into separate network zones within the same local area network. The Cisco ASA firewall will be configured to establish security zones and enforce traffic filtering policies, ensuring strict control over data flow between zones.

Simba Telecom has hired you as a **Network Security Engineer** to design a secure, reliable, scalable, and robust network system that aligns with the company’s operational goals. The design must adhere to a robust network architecture model and address critical security principles: **Confidentiality, Integrity**, and **Availability** of data and communications.

Your responsibilities include designing and implementing a network infrastructure that safeguards the company’s assets, ensures uninterrupted service delivery, and supports future growth. The solution must also integrate seamlessly with the company's existing cloud-based operations on Microsoft Azure.


### Simba Telecom Network Design and Implementation Requirements

Simba Telecom has emphasized the need for a network infrastructure that is high-performing, redundant, scalable, and highly available. The following requirements must be adhered to during the design and implementation process:

#### IP Addressing Scheme
The network will utilize the following IP address ranges:

1.	**WLAN**: 10.20.0.0/16
2.	**LAN**: 192.168.10.0/24
3.	**Voice**: 172.16.10.0/24
4.	**DMZ**: 10.10.10.0/28
5.	**Public Addresses**: 197.200.100.0/30

#### Network Design Requirements
1.	**Design Tool**:
    -	Use **Cisco Packet Tracer** to design and simulate the network solution.
2.	**Hierarchical Design**:
    -	Implement a hierarchical network model to ensure redundancy and improved scalability.
3.	**ISP Connection**:
    -	Ensure the network connects seamlessly to a **Zuku ISP Router** for internet services.
4.	**Wireless LAN Controller (WLC)**:
    -	Each department must have a wireless access point (WAP) providing separate Wi-Fi networks for employees and guests. All WAPs must be centrally managed by the WLC.
5.	**VoIP Integration**:
    -	Each department should be equipped with **IP phones** for Voice over IP (VoIP) services.
6.	**VLANs**:
    -	Configure the following VLANs across the network:
        -	**LAN VLAN**: VLAN 50
        -	**WLAN VLAN**: VLAN 60
        -	**VoIP VLAN**: VLAN 101
7.	**EtherChannel**:
    -	Use **Link Aggregation Control Protocol (LACP)** to configure EtherChannel for link aggregation.
8.	**STP Configurations**:
    -	Enable **STP PortFast** and **BPDU Guard** to allow faster port transitions from blocking to forwarding states, improving network convergence time.
9.	**Subnetting**:
    -	Perform subnetting to allocate the appropriate number of IP addresses to each department while maximizing address utilization.
10.	**Basic Device Configuration**:
    -	Configure basic device settings, including:
        -	Hostnames
        -	Console passwords
        -	Enable passwords
        -	Banner messages
        -	Password encryption
        -	Disabling IP domain lookup
11.	**Inter-VLAN Routing**:
    -	Configure the multilayer switch for **inter-VLAN routing** to ensure devices in all departments can communicate with one another.
12.	**Core Switch**:
    -	The multilayer switches should perform both routing and switching functionalities and be assigned IP addresses for proper management and routing.
13.	**DHCP Server**:
    -	Configure the **Active Directory (AD) servers** located at the server farm to provide dynamic IP addresses to all devices in the network except IP phones.
14.	**Cisco 2811 Router**:
    -	Incorporate a **Cisco Catalyst 2811 router** to support telephony services, ensuring it is connected to the Layer 3 switch.
15.	**Static Addressing**:
    -	Allocate static IP addresses to all devices in the server room.
16.	**Telephony Service**:
    -	Configure VoIP on the voice gateway router and assign dial numbers in the format 1xxx.
17.	**Routing Protocol**:
    -	Use **OSPF** (Open Shortest Path First) as the routing protocol to advertise routes on both the routers and multilayer switches.
18.	**Standard ACL for SSH**:
    -	Configure a **standard ACL** on the line VTY to restrict remote administrative tasks to the Senior Network Security Engineer, ensuring only authorized personnel can use SSH for management.
The final design must integrate these requirements to ensure a secure, scalable, and highly available network infrastructure. The solution should optimize performance, support future growth, and align with industry best practices.


## Subnetting
**Simba Telecom Network**
![image](https://github.com/user-attachments/assets/332e71ac-6891-44e5-a6f2-0d3056a50567)

**Between the Firewall, Routers and Layer-3 Switch**
![image](https://github.com/user-attachments/assets/20e692a2-39de-400c-a729-e8d4effe1fd5)






### Setup Details
-	Wazuh was deployed on a cloud server to monitor activity from endpoint devices.
-	Shuffle was installed on a separate cloud server for orchestration and automation.
-	The Hive was hosted on another cloud server for case management and collaboration.
-	The monitored endpoint: Windows machine (DESKTOP-8AAR6BV (002)).

## Workflow
1.	Threat Generation and Detection:
-	A Mimikatz alert was triggered on the Windows endpoint (DESKTOP-8AAR6BV (002)).
-	Wazuh detected the alert and generated detailed logs, including a SHA256 hash of the suspected malware.
![image](https://github.com/user-attachments/assets/06f8e34c-5492-4917-b23f-11663a3f04b6)

*Ref 2: Mimikatz File executed on Windows client Machine*

![image](https://github.com/user-attachments/assets/75b16c47-8d81-493b-9a84-44e82fc451a2)

*Ref 3a: Mimikatz alert detected on Wazuh*

![image](https://github.com/user-attachments/assets/c7ad6e4e-b4ed-4d92-85ec-dbfef825ffbe)

*Ref 3b: Mimikatz alert detected on Wazuh*

2.	Automation with Shuffle:
-	Wazuh sent the alert to Shuffle.
-	Shuffle extracted the SHA256 hash from the alert and queried VirusTotal for a reputation score.
-	Shuffle triggered additional actions based on the alert severity:
    o	Sending the alert to The Hive for case management.
    o	Sending an email notification to the SOC analyst.
 	
![image](https://github.com/user-attachments/assets/8f7708ed-0706-4bb3-911c-35740f361901)

*Ref 4: Shuffle Workflow*

![image](https://github.com/user-attachments/assets/21bc30ca-0ab9-4938-946c-1b86e721edcb)

*Ref 5: Data ingested to shuffle from Wazuh*

![image](https://github.com/user-attachments/assets/1bfa73eb-80ef-4d24-92d6-02422cd56037)

*Ref 6: SHA Regex to extract Hash value*

![image](https://github.com/user-attachments/assets/b305b7e7-d365-431c-94da-29aefedcc146)

*Ref 7: Virustotal results*

![image](https://github.com/user-attachments/assets/7f5f7ac9-141b-4099-a67d-c072f58bf0b1)

*Ref 8: Shuffle sending Alerts to The Hive and Email*

3.	Incident Management in The Hive:
-	The Hive received the alert as a new case with detailed information.
-	The SOC team could review, escalate, or close the case after investigation.

![image](https://github.com/user-attachments/assets/ec81a4df-8a99-4b1f-a550-4b0b926f46ee)

*Ref 9: Alert sent to The Hive*

![image](https://github.com/user-attachments/assets/d83922f1-f3b7-45f7-8b9b-03b455f80e6a)

*Ref 10: Alert sent to Email*

4.	Defensive Capabilities:
-	Shuffle workflows included automatic blocking of malicious IP addresses identified in the alerts.

## Conclusion
This SOC Automation Lab demonstrates the power of integrating open-source tools to build an efficient, automated incident response workflow. By combining monitoring, automation, and case management, the lab enhances the SOC's capability to detect, analyze, and respond to threats quickly and effectively.









