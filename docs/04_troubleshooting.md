<h2>4. Test Documentation & Troubleshooting</h2>

<h3>4.1 Test Cases & Scenarios</h3>

<p><strong>21.07.25 – Site-to-Site VPN Troubleshooting</strong></p>
<p>
The VPN tunnel between Hub and Spoke went down. Initial checks included static routes and disabling the blackhole route. The plan was to implement 1-to-1 NAT, simulating a client scenario where two firewalls both use overlapping 1.1.x.x LANs. One side had to be translated to 2.2.x.x to avoid IP conflicts.
</p>

<ul>
<li>Researched Fortinet documentation: "Site-to-site VPN with overlapping subnets".</li>
<li>Adapting the tutorial IPs to our real IPs was challenging.</li>
<li>Previous NAT configuration did not work; suspected missing or misconfigured policies.</li>
<li>Discovered that the firewall was blocking communication; adjusted NAT IP in VPN Phase 2.</li>
</ul>

<p><strong>24.07.25 – SNAT & DNAT</strong></p>
<ul>
<li>Checked ICMP via Windows Defender Firewall (extended security) to verify connectivity.</li>
<li>Captured ICMP traffic on clients on both firewalls using Wireshark.</li>
<li>Used packet sniffer on firewalls: <code>diagnose sniffer packet any "icmp" 4</code></li>
<li>Confusion around VIPs and IP Pools: VIPs had to be defined normally, then applied in the Incoming_Policy as destination; no NAT should be enabled after VIP-to-policy implementation.</li>
</ul>

<p><strong>29.07.25 – BGP Troubleshooting</strong></p>
<ul>
<li>Checked BGP summary: <code>get router info bgp summary</code></li>
<li>Sniffed packets for neighbor analysis: <code>diagnose sniffer packet any "host 172.21.0.1" 4</code></li>
<li>Verified BGP neighbors and learned networks: <code>get router info bgp neighbors</code> & <code>get router info bgp network</code></li>
<li>Checked routing table to confirm route propagation: <code>get router info routing-table all</code></li>
</ul>

<p><strong>31.07.25 – Further BGP Troubleshooting</strong></p>
<ul>
<li>Confirmed VRF BGP table and local router ID.</li>
<li>Verified network advertisements and connected routes.</li>
<li>Neighbor status showed Active; troubleshooting continued with route injection and validation.</li>
</ul>

<p><strong>10.08.25 – Client VPN, IPsec Phase 1 Error</strong></p>
<ul>
<li>Checked VPN gateways and tunnel summary: <code>diagnose vpn ike gateway list</code> & <code>get vpn ipsec tunnel summary</code></li>
<li>Identified Phase 1 negotiation issues.</li>
</ul>

<p><strong>12.08.25 – Client VPN IKEv2 Troubleshooting</strong></p>
<ul>
<li>Examined routing tables and packet captures: <code>get router info routing-table all</code></li>
<li>Used sniffer for IKEv2 interfaces: <code>diag snif pack IKEv2 interfaces=[IKEv2] filters=[none]</code></li>
<li>Observed packet flows, errors, and missing IP assignments.</li>
<li>Analyzed UDP traffic for VPN negotiation and multicast communication.</li>
</ul>

<h3>4.2 Problems & Solutions</h3>

<ul>
<li><strong>VPN Tunnel Down:</strong> Blocked by firewall rules. Solution: adjust policies and NAT IP in Phase 2.</li>
<li><strong>SNAT/DNAT Misconfiguration:</strong> VIP misused; resolved by proper VIP-to-policy implementation without NAT.</li>
<li><strong>BGP Routes Not Propagated:</strong> Verified neighbor connectivity and injected missing routes.</li>
<li><strong>Client VPN Errors:</strong> Phase 1 negotiation failed due to misconfigured gateways; analyzed routing and packet flow to resolve.</li>
<li><strong>General Lessons:</strong> Always validate routing, NAT, firewall policies, and VPN Phase 1/2 settings. Use packet captures and sniffer tools to observe live traffic.</li>
</ul>

<p><strong>Conclusion:</strong> Systematic troubleshooting with step-by-step verification helped stabilize VPNs, NAT, and BGP. This process improved understanding of routing, policy dependencies, and enterprise network debugging.</p>
