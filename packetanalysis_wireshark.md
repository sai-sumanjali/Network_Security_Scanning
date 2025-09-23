 <h1>Analyzing Packets With Wireshark</h1>

<h2>Description</h2>

This Project consists of steps on how to Use Wireshark filters to:
 <ol type = "1">
  
<li>Inspect a specific IP addresses traffic</li>
<li>Explore DNS packets to examine protocol data</li>
<li>Search TCP packets for various payload text data</li>
</ol>

<h2>Languages and Utilities Used</h2>

- <b><a href="https://www.wireshark.org/">Wireshark</a></b>
- <b><a href="https://go.qwiklabs.com/">QikiLabs</a></b>
<h2>Environments Used </h2>

- <b>Windows 10</b>

<h2>Program walk-through:</h2>


<h3>Part 1: Inspecting traffic from a user </h3>

<p align="center">
 To start I opened a sample .pcap file provided by <a href="https://go.qwiklabs.com/">QikiLabs</a> to start experimenting with. By inserting <code>ip.addr == 142.250.1.139</code> In the filter box, only packets with the source or the destination IP address will appear.
 
<img src="https://imgur.com/za6Ng5n.png" />
</br>
<p align="center">
By opening the packet details pane window I can see that this packet's destination is port 80 (HTTP) and is a SYN packet meaning this is the start of a new TCP 3-Way Handshake.
 
<img src="https://imgur.com/aIQwZ2g.png"/>
<p align="center">
 
Other possible filters to analyze specific network packets: 
 <li>Where the packets came from <code>ip.src == 142.250.1.139</code> </li>
 <li>Where the packets were sent to <code>ip.dst == 142.250.1.139</code></li>
 <li>Even by physical Ethernet Media Access Control (MAC) address using <code>eth.addr == 42:01:ac:15:e0:02</code></li>
</br>
<p align="center">
 Back in the same packet detail window in the Ethernet II subtree, the MAC address is displayed in clear text.
 
<img src="https://imgur.com/HWqhlZx.png"/>


<h3>Part 2: Analyzing DNS packets </h3>
<p align="center">
 To filter for DNS traffic I used the UDP port 53 which will list traffic related to DNS queries and responses only.
 <li><code>udp.port == 53</code></li>
 <p align="center">
 In this DNS traffic, I started exploring and found that there was information about IP 142.250.1.139 being queried for opensource.google.com by looking at a packet that came from 169.254.169.254, and had the destination of 172.21.224.2. 
 
<img src="https://imgur.com/xQ485Wm.png"/>


<h3>Part 3: Analyzing TCP packets</h3>
<p align="center">
 Then filtering for TCP using port 80 by using this command
<li><code>tcp.port == 80</code></li>
 <p align="center">
I found out many packets were created when 142.250.1.139 queried for opensource.google.com
 </br>
  <p align="center">
   In the first packet in the list, I identified:
   <ol type = "1">
   <li>Time to Live value: 64 seconds</li>
   <li>Frame Length: 54 bytes</li>
   <li>Header Length: 20 bytes</li>
   
   </ol>
<img src="https://imgur.com/zZ0VT9P.png"/>
