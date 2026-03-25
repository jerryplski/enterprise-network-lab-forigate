<h1>NLAB Network Project Documentation</h1>

<p>
Simulated enterprise network with two sites (Hub & Spoke), focused on routing, VPN, NAT and segmentation.
</p>

<h2>Table of Contents</h2>

<ul>
<li>1. Project Overview</li>
<li>2. Network Design</li>
<li>3. Configuration & Security</li>
<li>4. Troubleshooting</li>
</ul>

<h2>1. Project Overview</h2>

<h3>Project Description</h3>

<p>
Design and implementation of a simulated enterprise network ("NLAB Solutions GmbH") with two locations.
</p>

<ul>
<li>Two sites with /16 networks</li>
<li>VLAN segmentation</li>
<li>Different firewall deployment strategies</li>
<li>Routing, NAT, DNS and VPN implementation</li>
</ul>

<h3>Milestones</h3>

<ul>
<li><strong>KW-29:</strong> Planning, VLANs, policies, VPN setup</li>
<li><strong>KW-30:</strong> Site-to-Site VPN with overlapping subnets (SNAT/DNAT)</li>
<li><strong>KW-31:</strong> Dynamic routing with BGP</li>
<li><strong>KW-32:</strong> Dual-WAN & SD-WAN</li>
<li><strong>KW-33:</strong> Remote Access VPN (IKEv2)</li>
<li><strong>KW-34:</strong> Monitoring</li>
</ul>

<h3>To-Do</h3>

<ul>
<li>Traffic Shaping</li>
<li>Client VPN finalization</li>
<li>IPv6 integration</li>
<li>BGP rebuild</li>
<li>VPN stabilization</li>
</ul>

<h3>Learning Goals</h3>

<ul>
<li>Routing vs NAT understanding</li>
<li>VLAN design</li>
<li>VPN (Site-to-Site & Remote)</li>
<li>BGP fundamentals</li>
</ul>

<h3>Notes</h3>

<p><strong>Core principle:</strong></p>
<p><em>"It's always NAT, Routing or DNS."</em></p>

<ul>
<li>BGP requires known routes before advertisement</li>
<li>Blackhole routes for route announcement</li>
<li>Administrative Distance hierarchy</li>
</ul>

<hr>

<h2>2. Network Design</h2>

<h3>Topology</h3>

<pre>
Firewall -> Switch -> Clients
</pre>

<h3>Segments</h3>

<ul>
<li>LAN (private)</li>
<li>WAN</li>
<li>DMZ</li>
<li>VPN</li>
<li>VLANs</li>
</ul>

<h3>Devices</h3>

<ul>
<li>Firewall HUB</li>
<li>Firewall SPOKE</li>
<li>Core Switch</li>
<li>Access Switch</li>
</ul>

<h3>IP Addressing</h3>

<p><strong>WAN (Documentation ranges)</strong></p>
<ul>
<li>203.0.113.1</li>
<li>198.51.100.1</li>
</ul>

<p><strong>LAN</strong></p>
<ul>
<li>HUB: 10.60.0.0/16</li>
<li>SPOKE: 10.61.0.0/16</li>
</ul>

<table>
<tr><th>VLAN</th><th>Network</th></tr>
<tr><td>10</td><td>10.60.10.0/24 (Management)</td></tr>
<tr><td>11</td><td>10.60.11.0/24 (Admins)</td></tr>
<tr><td>12</td><td>10.60.12.0/24 (Clients)</td></tr>
<tr><td>66</td><td>10.60.66.0/24 (Guest)</td></tr>
<tr><td>100</td><td>10.60.100.0/24 (Printer)</td></tr>
<tr><td>1</td><td>10.60.1.0/24 (Server)</td></tr>
</table>

<h3>User Management</h3>

<p>Not implemented yet.</p>

<hr>

<h2>3. Configuration & Security</h2>

<h3>Interfaces & Zones</h3>

<ul>
<li>LAN</li>
<li>WAN</li>
<li>VPN</li>
<li>DMZ</li>
</ul>

<h3>Address Objects & Services</h3>

<ul>
<li>Network objects definition</li>
<li>Service groups for policies</li>
</ul>

<h3>Policies (incl. NAT)</h3>

<table>
<tr><th>ID</th><th>Source</th><th>Destination</th><th>Service</th><th>Action</th></tr>
<tr><td>1</td><td>LAN</td><td>WAN</td><td>ANY</td><td>ALLOW</td></tr>
<tr><td>2</td><td>LAN</td><td>DNS</td><td>DNS</td><td>ALLOW</td></tr>
</table>

<h3>VPN Configuration</h3>

<p><strong>Site-to-Site VPN</strong></p>

<ul>
<li>IKE Version: 2</li>
<li>Encryption: AES256</li>
<li>Hash: SHA512</li>
<li>DH Group: 20</li>
<li>Authentication: PSK</li>
</ul>

<p><strong>Phase 2</strong></p>

<ul>
<li>Encryption: AES256</li>
<li>Hash: SHA512</li>
<li>DH Group: 20</li>
</ul>

<h3>Security Profile</h3>

<ul>
<li>Antivirus</li>
<li>Webfilter</li>
<li>IPS</li>
</ul>

<h3>Logging & Monitoring</h3>

<ul>
<li>Firewall logs</li>
<li>VPN monitoring</li>
<li>Traffic analysis</li>
</ul>

<h3>Switch Configuration</h3>

<pre>
interface GigabitEthernet1/0/2
 description CLIENT_PORT
 switchport mode access
 switchport access vlan 101
</pre>

<hr>

<h2>4. Troubleshooting</h2>

<h3>Scenarios</h3>

<p><strong>VPN Issue</strong></p>
<ul>
<li>Tunnel down</li>
<li>Cause: NAT / policy misconfiguration</li>
</ul>

<p><strong>SNAT / DNAT</strong></p>
<ul>
<li>Analyzed using Wireshark and sniffer</li>
<li>Issue: incorrect VIP usage</li>
</ul>

<p><strong>BGP</strong></p>

<pre>
get router info bgp summary
get router info routing-table all
</pre>

<h3>Problems & Solutions</h3>

<ul>
<li>Policy errors → blocked traffic</li>
<li>Incorrect NAT → no communication</li>
<li>Missing BGP route → no propagation</li>
</ul>

<h3>Conclusion</h3>

<ul>
<li>Solid enterprise network design implemented</li>
<li>Hands-on experience with VPN, NAT and BGP</li>
<li>Strong improvement in troubleshooting skills</li>
</ul>
