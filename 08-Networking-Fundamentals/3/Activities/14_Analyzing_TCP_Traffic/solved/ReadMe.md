## Solution Guide: Analyze TCP Traffic 

This activity was designed to introduce the Layer 4 protocol and TCP and practice identifying how TCP uses a three-way handshake to establish a connection with a remote host.  

Completing this activity required the following steps:

   - Loading a TCP packet capture with Wireshark.

  - Finding all establishing TCP handshakes in the packet capture.

  - Finding all TCP terminations in the packet capture. 

   - Determining what websites were visited by analyzing the TCP traffic.
   
---

In Wireshark, open the packetcapTCPclass.pcapng file. 

Find all the TCP handshakes for establishing a connection.
 
- There are three three-way handshakes in the packet capture. 

To find them, do the following:

- To view only the three SYN requests, run:  

  `tcp.flags.syn ==1 && tcp.flags.ack == 0`

- To view only the three SYN/ACK responses, run: 

  `tcp.flags.syn ==1 && tcp.flags.ack == 1`

- To view only the three ACK responses, run: 

  `tcp.flags.syn == 0 && tcp.flags.ack == 1`
  
  **Note:** This may show some extra packets, including the FIN packet. To isolate only the three packets, run:

  `tcp.flags.syn ==1 && tcp.flags.ack == 1 && tcp.flags.fin == 0`


Find any TCP terminations.

- In the packet capture, there is one TCP termination from `Src: 209.202.133.24`. 

- To filter for terminations, run: 

  `tcp.flags.fin==1`

 Use your findings to determine what the employee did during their first week of work.

- To determine what websites were visited, translate the network IP address to the domain name.

  - Click on `View` > `Name Resolution` > `Resolve Network Address`.

  - After `Resolve Network Address` has been selected, the remote hosts the user accessed display as:

    - `travelocity.com`
    - `trivago.com`
    - `cruises.com`
  
     If the IPs aren't being resolved within Wireshark, use the following website to look up the domains that the IPs (8.35.179.200, 209.202.133.24, and 52.26.234.148 ) are connected to: https://mxtoolbox.com/ReverseLookup.aspx

**NOTE:** If the IP addresses do not resolve, it is likely the organization has moved its servers to another provider or the cloud.  

Based on these results, we can determine that the new employee is planning a vacation.

---

&copy; 2023 edX Boot Camps LLC. Confidential and Proprietary. All Rights Reserved.
