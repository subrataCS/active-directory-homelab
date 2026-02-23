<h1>After Joining Windows 10 Client to Domain — Next Steps</h1>

<hr>

<h2>Phase 1 – Verify Domain Membership</h2>

<ol>
  <li>Login using a domain account</li>
</ol>

<pre>
Username: LAB\test.user
Password: Password@123
</pre>

<ol start="2">
  <li>Open Command Prompt and verify user context</li>
</ol>

<pre>
whoami
</pre>

<p>You should see the domain username.</p>

<ol start="3">
  <li>Check logon server</li>
</ol>

<pre>
echo %logonserver%
</pre>

<p>This should display your Domain Controller name.</p>

<hr>

<h2>Phase 2 – Confirm Client Appears in Active Directory</h2>

<ol>
  <li>Go to Domain Controller</li>
  <li>Open <b>Active Directory Users and Computers</b></li>
  <li>Navigate to <b>Computers</b> container</li>
</ol>

<p>You should see the Windows 10 client machine listed.</p>

<hr>

<h2>Phase 3 – Test Domain Authentication Features</h2>

<ol>
  <li>Create a new folder on the client desktop</li>
  <li>Logout and login again using the same domain user</li>
</ol>

<p>This confirms user profile creation from the domain.</p>

<hr>

<h2>Phase 4 – Test Network Communication with Domain Controller</h2>

<pre>
ping lab.local
nslookup lab.local
</pre>

<p>If successful, DNS and domain communication are working correctly.</p>

<hr>

<h2>Phase 5 – (Recommended) Move Computer to Organizational Unit (OU)</h2>

<ol>
  <li>On Domain Controller open <b>Active Directory Users and Computers</b></li>
  <li>Create a new Organizational Unit (OU)</li>
</ol>

<pre>
OU Name: Workstations
</pre>

<ol start="3">
  <li>Move the client computer into this OU</li>
</ol>

<p>This helps with policy management later.</p>

<hr>

<h2>Phase 6 – Apply a Test Group Policy (Optional but Important)</h2>

<ol>
  <li>Open <b>Group Policy Management</b></li>
  <li>Create a new GPO linked to the Workstations OU</li>
  <li>Example Policy: Disable Control Panel</li>
</ol>

<ol start="4">
  <li>On the client machine run:</li>
</ol>

<pre>
gpupdate /force
</pre>

<p>This confirms Group Policy is working.</p>

<hr>

<h2>Phase 7 – Useful Verification Commands</h2>

<pre>
hostname
whoami /fqdn
ipconfig /all
nltest /dsgetdc:lab.local
</pre>

<hr>

<h2>What You Have Achieved</h2>

<ul>
  <li>Client successfully joined to domain</li>
  <li>Centralized authentication working</li>
  <li>Domain Controller communication verified</li>
  <li>Ready for Group Policy and security testing</li>
</ul>

<hr>

<h2>Recommended Next Lab Steps</h2>

<ul>
  <li>Create multiple domain users</li>
  <li>Configure shared folders with permissions</li>
  <li>Deploy Group Policies</li>
  <li>Install monitoring tools (example: SIEM agent)</li>
  <li>Generate authentication logs for SOC practice</li>
</ul>

<hr>

<p><em>Post-domain-join checklist for homelab environment.</em></p>
