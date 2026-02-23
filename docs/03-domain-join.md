<h1>Windows 10 Pro Client — Join to Active Directory Domain</h1>

<hr>

<h2>Phase 1 – Configure Network on Windows 10 Client</h2>

<ol>
  <li>Open <b>Network Settings</b></li>
  <li>Search → Network Status → Change Adapter Options</li>
  <li>Right-click <b>Ethernet</b> → Properties</li>
  <li>Select <b>Internet Protocol Version 4 (IPv4)</b> → Double-click</li>
</ol>

<h3>Recommended Configuration</h3>

<ul>
  <li>Obtain an IP address automatically (DHCP)</li>
  <li>Set DNS manually to Domain Controller</li>
</ul>

<pre>
Preferred DNS: 10.0.2.10   (Domain Controller IP)
Alternate DNS: (leave blank)
</pre>

<p><b>Important:</b> Do NOT use public DNS (8.8.8.8 / 1.1.1.1) on the client.</p>

<hr>

<h2>Phase 2 – Verify Connectivity</h2>

<ol>
  <li>Open Command Prompt</li>
  <li>Check IP configuration</li>
</ol>

<pre>
ipconfig /all
</pre>

<ol start="3">
  <li>Ping the Domain Controller</li>
</ol>

<pre>
ping 10.0.2.10
</pre>

<ol start="4">
  <li>Verify domain resolution</li>
</ol>

<pre>
ping lab.local
</pre>

<p>If successful, network configuration is correct.</p>

<hr>

<h2>Phase 3 – Join Windows 10 to Domain</h2>

<ol>
  <li>Right-click <b>This PC</b> → Properties</li>
  <li>Click <b>Rename this PC (Advanced)</b></li>
  <li>Click <b>Change</b></li>
  <li>Select <b>Domain</b></li>
  <li>Enter:</li>
</ol>

<pre>
lab.local
</pre>

<ol start="6">
  <li>Click OK</li>
  <li>Enter Domain Administrator credentials</li>
</ol>

<pre>
Username: LAB\Administrator
Password: (Domain Admin password)
</pre>

<ol start="8">
  <li>You should see: <b>Welcome to the lab.local domain</b></li>
  <li>Restart the computer</li>
</ol>

<hr>

<h2>Phase 4 – Login Using Domain User</h2>

<pre>
Username: LAB\test.user
Password: Password@123
</pre>

<hr>

<h2>Why DNS Must Point to Domain Controller</h2>

<ul>
  <li>Domain join uses DNS to locate Domain Controller</li>
  <li>Authentication relies on Active Directory DNS records (SRV records)</li>
  <li>Public DNS will break domain login</li>
</ul>

<hr>

<p><em>Personal reference for Windows client domain join.</em></p>
