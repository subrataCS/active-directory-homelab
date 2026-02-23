<h1>Active Directory Homelab Setup Guide</h1>

<hr>

<h2>Phase 1 – Configure Network on Domain Controller</h2>

<ol>
  <li>Open <b>Network Settings</b></li>
  <li>Search → Network → Change Adapter Options</li>
  <li>Right-click <b>Ethernet</b> → Properties</li>
  <li>Select <b>Internet Protocol Version 4 (IPv4)</b> → Double-click</li>
  <li>Configure IP address according to your NAT Network subnet</li>
</ol>

<pre>
IP Address: 10.0.2.10
Subnet Mask: 255.255.255.0
Default Gateway: 10.0.2.1
Preferred DNS: 127.0.0.1
</pre>

<p>Save the configuration and close all windows.</p>

<hr>

<h2>Phase 2 – Install Active Directory Domain Services</h2>

<h3>1. Install AD DS Role</h3>
<ol>
  <li>Open <b>Server Manager</b></li>
  <li>Click <b>Manage → Add Roles and Features</b></li>
  <li>Select <b>Role-based or feature-based installation</b></li>
  <li>Choose <b>Active Directory Domain Services</b></li>
  <li>Click <b>Install</b></li>
</ol>

<h3>2. Promote Server to Domain Controller</h3>
<ol>
  <li>Click the notification flag in Server Manager</li>
  <li>Select <b>Promote this server to a domain controller</b></li>
  <li>Choose <b>Add a new forest</b></li>
</ol>

<pre>
Domain Name: lab.local
NetBIOS Name: LAB
DSRM Password: Password@123
</pre>

<ol start="4">
  <li>Ignore DNS warning if shown</li>
  <li>Complete the wizard and allow the server to reboot</li>
</ol>

<hr>

<h2>Phase 3 – Restore Internet on Domain Controller</h2>

<h3>3. Add DNS Forwarders</h3>
<ol>
  <li>Open <b>DNS Manager</b></li>
  <li>Right-click your server → Properties</li>
  <li>Go to the <b>Forwarders</b> tab → Click <b>Add</b></li>
</ol>

<pre>
8.8.8.8
1.1.1.1
</pre>

<h3>4. Restart DNS Service</h3>

<pre>
services.msc → DNS Server → Restart
</pre>

<hr>

<h2>Phase 4 – Create a Domain User</h2>

<h3>5. Create User in Active Directory</h3>
<ol>
  <li>Open <b>Active Directory Users and Computers</b></li>
  <li>Right-click your domain → New → User</li>
</ol>

<pre>
Username: test.user
Password: Password@123
</pre>

<hr>

<h2>Phase 5 – Join Client Machine to Domain</h2>

<h3>6. Configure Client DNS</h3>

<pre>
Preferred DNS: &lt;Domain Controller IP&gt;
</pre>

<h3>7. Join Domain</h3>
<ol>
  <li>This PC → Properties → Rename this PC (Advanced)</li>
  <li>Select <b>Domain</b></li>
  <li>Enter:</li>
</ol>

<pre>
lab.local
</pre>

<pre>
Username: LAB\Administrator
Password: (Domain Admin password)
</pre>

<ol start="4">
  <li>Restart the client virtual machine</li>
</ol>

<hr>

<h2>Phase 6 – Test Authentication</h2>

<h3>8. Log in as Domain User</h3>

<pre>
Username: LAB\test.user
Password: Password@123
</pre>

<p>If login succeeds, Active Directory is working correctly.</p>

<hr>

<h2>What This Lab Demonstrates</h2>

<ul>
  <li>Active Directory relies heavily on DNS</li>
  <li>Clients authenticate against the Domain Controller</li>
  <li>User accounts are centralized rather than local</li>
  <li>Incorrect network configuration can immediately break AD functionality</li>
</ul>

<hr>

<p><em>Personal reference document for Active Directory homelab setup.</em></p>
