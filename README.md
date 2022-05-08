<p style="text-align:center"><u><span style="font-size:22px">POC - Proof of competence</span></u></p>

<p style="text-align:center">&nbsp;</p>

<p><span style="font-size:14px">This is a POC test for DevOps position. It contains Jenkins pipeline running Vgarant script to build 3 ubuntu VMs, Ansible playbooks for running Dockerized nginx and apache servers and a test phase.</span></p>

<p><strong><span style="font-size:14px">Prerequisites:</span></strong></p>

<p><span style="font-size:12px">1. Jenkins Server (v2.332.3) with Ansible plugin (v1.1)</span></p>

<p><span style="font-size:12px">2. Oracle VirtualBox (v6.1)</span></p>

<p><span style="font-size:12px">3. Docker (v20.10.15)</span></p>

<p><span style="font-size:12px">4. Python (v3.8.10)</span></p>

<p><span style="font-size:12px">5. Ansible (core v2.12.5) with community.docker plugin (v.2.4.0)</span></p>

<p><span style="font-size:12px">6. Vagrant (v2.2.19)</span></p>

<p><span style="font-size:12px">7. Public and private SSH keys (default naming) stored in /var/lib/jenkins/.ssh</span></p>

<p>&nbsp;</p>

<p><strong><span style="font-size:14px">Instructions for use:</span></strong></p>

<p>Please pull code from git with Jenkins and run the pipeline or copy the contents of Jenkinsfile in a new pipeline script.</p>

<p>&nbsp;</p>

<p><strong><span style="font-size:14px">Testing:</span></strong></p>

<p>After the Ansible provisioning stage, Jenkins will send get requests to the nginx server (192.168.80.10), these requests will be directed to web-1 (192.168.80.20) and web-2 (192.168.82.30) servers in a round-robin pattern, and we&#39;ll be able to see that the reply will be received from different server each time.</p>
