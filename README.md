<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

# Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines

In this tutorial, we observe various network traffic to and from Azure Virtual Machines using Wireshark and experiment with Network Security Groups.

## Environments and Technologies Used

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDP, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

## Operating Systems Used

- Windows 10 (21H2)
- Ubuntu Server 20.04

## Actions and Observations

1. **Setup Virtual Machines**
   - Create two Virtual Machines on Microsoft Azure: one with Linux (Ubuntu Server 20.04) and the other with Windows 10.
   - Ensure both VMs have two CPUs and are on the same virtual network.

2. **Install Wireshark on Windows Machine**
   - Download and install Wireshark on the Windows machine from [Wireshark download page](https://www.wireshark.org/download.html).
   - Open Wireshark and filter for ICMP traffic only.

   <p align="center">
   <img src="https://i.imgur.com/IIUShxp.png" height="80%" width="80%" alt="Wireshark Filtering"/>
   </p>

3. **Ping Linux Machine**
   - Ping the private IP address of the Linux machine from the Windows machine.
   - Observe the ICMP packets in Wireshark.

   <p align="center">
   <img src="https://i.imgur.com/GLxSIG3.png" height="80%" width="80%" alt="ICMP Packet"/>
   </p>

4. **Block ICMP Traffic**
   - On the Linux machine, block inbound ICMP traffic on its firewall.
   - Observe that the Windows machine stops receiving echo replies.
   - Create a new Network Security Group (NSG) on the Linux machine to block ICMP.
   - Allow ICMP traffic again via the NSG on the Azure portal.

   <p align="center">
   <img src="https://i.imgur.com/5vXO75R.png" height="80%" width="80%" alt="Block ICMP"/>
   </p>
   <p align="center">
   <img src="https://i.imgur.com/Asl80tN.png" height="80%" width="80%" alt="Allow ICMP"/>
   </p>

5. **SSH into Linux Machine**
   - Use the Windows machine to SSH into the Linux machine.
   - Set Wireshark to capture SSH packets only.
   - SSH into the Linux machine using `ssh labuser@10.0.0.5` and observe the captured SSH packets.

   <p align="center">
   <img src="https://i.imgur.com/zteR41r.png" height="80%" width="80%" alt="SSH Packet"/>
   </p>

6. **Capture DHCP Traffic**
   - Set Wireshark to filter for DHCP traffic.
   - On the Windows machine, request a new IP address with `ipconfig /renew`.
   - Observe the DHCP traffic in Wireshark.

   <p align="center">
   <img src="https://i.imgur.com/vU8fpQf.png" height="80%" width="80%" alt="DHCP Packet"/>
   </p>

7. **Capture DNS Traffic**
   - Set Wireshark to filter for DNS traffic.
   - Initiate DNS traffic by typing `nslookup www.google.com`.
   - Observe the DNS traffic in Wireshark.

   <p align="center">
   <img src="https://i.imgur.com/VMcwmsO.png" height="80%" width="80%" alt="DNS Packet"/>
   </p>

8. **Capture RDP Traffic**
   - Filter for RDP traffic in Wireshark by entering `tcp.port==3389`.
   - Observe the continuous RDP traffic due to the Remote Desktop Protocol connection to the Virtual Machine.

   <p align="center">
   <img src="https://i.imgur.com/VxXGv6X.png" height="80%" width="80%" alt="RDP Packet"/>
   </p>
