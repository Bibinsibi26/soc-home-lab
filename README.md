<h1>SOC Home Lab: Splunk SIEM & Log Analysis</h1>

<h2>🎯 Objective</h2>

This project aims to establish a functional SOC environment to ingest, analyze, and monitor logs from multiple endpoints. By configuring a Universal Forwarder on Ubuntu to send data to Splunk Enterprise on Windows, I simulated real-world log telemetry and built custom detection rules.

<h2>🛠️ Tools Used</h2>

• SIEM: Splunk Enterprise (Windows)

• Endpoints: Ubuntu (Linux)

• Agent: Splunk Universal Forwarder

• Networking: VirtualBox/VMware Host-Only Adapter


<h2>📁 Repository Structure</h2>


<a href="https://github.com/Bibinsibi26/soc-home-lab/edit/main/README.md#network-diagrams-of-the-lab-setup
">• /Architecture: Network diagrams of the lab setup.</a>

<a href="https://github.com/Bibinsibi26/soc-home-lab/edit/main/README.md#%EF%B8%8F-configuration-files-splunk-forwarding">• /Configs: Custom inputs.conf and outputs.conf files.</a>

<a href="https://github.com/Bibinsibi26/soc-home-lab/edit/main/README.md#%EF%B8%8F-installation-guide-splunk-enterprise-windows">. /Installation Guide: Splunk Enterprise (Windows)</a>


<a href="https://github.com/Bibinsibi26/soc-home-lab/edit/main/README.md#-conclusion">. /conclusion </a>



<h2>🛜Network diagrams of the lab setup</h2>


<p align="center">
  <img src="https://github.com/Bibinsibi26/soc-home-lab/raw/b3c24ef7b0e0e0d8b0f9d25a0e5ef3fd46c22453/WhatsApp%20Image%202026-02-18%20at%205.46.06%20PM.jpeg" width="600">
</p>

<a href="https://github.com/Bibinsibi26/soc-home-lab/edit/main/README.md#%EF%B8%8F-installation-guide-splunk-enterprise-windows">link text</a>


In this lab, the communication between the Ubuntu Endpoint and the Windows SIEM is governed by two critical configuration files located on the Ubuntu Universal Forwarder (UF).

<h3>1.Outputs.conf</h3>

Location: /opt/splunkforwarder/etc/system/local/

Purpose: This file tells the Universal Forwarder where to send the data.

• Target IP: It contains the IP address of your Windows Splunk Enterprise instance.

• Port: It specifies Port 9997, which is the default Splunk receiving port.

• Function: Without this, the logs would just sit on the Ubuntu VM with nowhere to go.


<h3>2.Inputs.conf</h3>

Location: /opt/splunkforwarder/etc/system/local/

Purpose: This file tells the Universal Forwarder what data to collect.

• Monitor Path: It specifies the file paths to watch (e.g., /var/log/auth.log for login data or /var/log/syslog).

• Index: It assigns the data to a specific index (like main or a custom linux_logs index) to keep the SIEM organized.

• Sourcetype: It labels the data so Splunk knows how to parse it (e.g., sourcetype = linux_secure).

<h2>🛠️ Installation Guide: Splunk Enterprise (Windows)</h2>

<h3>1. Prerequisites</h3>

• Operating System: Windows 10/11 or Windows Server.

• Hardware: Minimum 4GB RAM (8GB recommended for VMs).

• Account: Administrative privileges on the Windows machine.

<h3>2. Download the Installer</h3>
   
• Go to the Splunk Official Downloads page.

• Choose the Windows 64-bit (msi) installer.

• (Note: You may need to create a free Splunk account to access the download).

<h3>3. Installation Steps</h3>
  
1. Launch the .msi file: Double-click the installer to begin.
2. Check License Agreement: Accept the terms and click Next.
3. Customer Information: * Select "An enterprise installation" (default).

• Create an Administrator Username (e.g., admin) and a Strong Password.

• Crucial: Save these credentials; you will need them to log into the web interface.

4. Installation Path: Use the default path (C:\Program Files\Splunk) or choose a dedicated drive.
5. Step through the Wizard: Click Install. The process usually takes 3–5 minutes.
6. Launch Splunk: Once finished, ensure "Launch Splunk Web" is checked and click Finish.
7. Accessing the Web Interface

• Open your browser and go to: http://localhost:8000 (or the IP of your VM).

• Log in using the credentials you created in Step 3.

<h3>4. Post-Installation Configuration</h3>

To allow your Ubuntu VM to send data to this Windows instance, you must enable the "Receiver" port:

1. In Splunk Web, go to Settings > Forwarding and receiving.
2. Click Add new under "Receive data".
3. Enter Port: 9997.
4. Click Save.

<h2>🏁 Conclusion</h2>

This SOC Home Lab project successfully demonstrates the end-to-end process of security log management—from raw data generation on a Linux endpoint to centralized analysis and threat detection in Splunk Enterprise.




