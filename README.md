<h2 style="text-align: center;"><u>POC - Proof of competence</u></h2>
<p>This is a POC test for DevOps position. It contains Jenkins pipeline running Vgarant script to build 3 ubuntu VMs, Ansible playbooks for running Dockerized nginx and apache servers and a test phase.</p>
<h4><strong>Prerequisites:</strong></h4>
<p>1. Jenkins Server (v2.332.3) with Ansible plugin (v1.1)</p>
<p>2. Oracle VirtualBox (v6.1)</p>
<p>3. Docker (v20.10.15)</p>
<p>4. Python (v3.8.10)</p>
<p>5. Ansible (core v2.12.5, ansible v5.7.1) with community.docker plugin (v.2.4.0)</p>
<p>6. Vagrant (v2.2.19)</p>
<p>7. Public and private SSH keys (default naming) stored in /var/lib/jenkins/.ssh</p>
<p>&nbsp;</p>
<h4><strong>Instructions for use:</strong></h4>
<p>Please pull code from git with Jenkins and run the pipeline or copy the contents of Jenkinsfile in a new pipeline script.</p>
<p>&nbsp;</p>
<h4><strong>Testing:</strong></h4>
<p>After the Ansible provisioning stage, Jenkins will send get requests to the nginx server (192.168.80.10), these requests will be directed to web-1 (192.168.80.20) and web-2 (192.168.82.30) servers in a round-robin pattern, and we'll be able to see that the reply will be received from different server each time.</p>
