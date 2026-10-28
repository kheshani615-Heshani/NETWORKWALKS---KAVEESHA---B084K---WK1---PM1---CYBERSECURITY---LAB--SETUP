<div  style="font-family: Arial, sans-serif; color: #333; line-height: 1.4;">

  <!-- Main Topic (Font Size 12px) -->
  <h1 style="font-size: 12px; font-color:Light Blue; font-weight: bold; border-bottom: 2px ; padding-bottom: 4px;">
    
  # 🔐 Cybersecurity Lab Environment Setup & Initial Reconnaissance

  <img width="750" align=center height="500" alt="image" src="https://github.com/user-attachments/assets/d1f6b1e3-a8ac-4f87-88d8-d99d94456283" />

  
  </h1>

  

  <!-- Section 1: Project View (Heading: 11px | Body: 9px) -->
  <h2 style="font-size: 11px; font-weight: bold; margin-top: 15px; color: #1a0dab;">

    
   <span>📌</span> Project View
  </h2>
  <p style="font-size: 9px; margin: 4px 0;">
    This project establishes a foundational, secure, and isolated cybersecurity testing environment. It details the deployment of a virtualization hypervisor (Oracle VM VirtualBox), the provisioning of a penetration testing operating system (Kali Linux), and the configuration of essential network reconnaissance utilities.
  </p>
  

  <!-- Section 2: Objectives (Heading: 11px | List: 9px) -->
  <h2 style="font-size: 11px; font-weight: bold; margin-top: 15px; color: #1a0dab;">
   <span>🎯</span> Objectives
  </h2>
  <ul style="font-size: 9px; margin: 4px 0; padding-left: 15px;">
    <li><strong>Infrastructure Deployment:</strong> Install and configure a hypervisor environment for running isolated virtual machines safely.</li>
    <li><strong>OS Provisioning:</strong> Set up a secure Kali Linux virtual machine with updated software repositories and network adapters[cite: 4, 5].</li>
    <li><strong>Toolchain Integration:</strong> Install and verify core security reconnaissance and scanning tools.</li>
    <li><strong>Network Mapping:</strong> Perform initial host discovery and port scanning within a controlled, authorized subnet.</li>
    <li><strong>Documentation & Compliance:</strong> Record architectural layouts, configuration steps, troubleshooting logs, and ethical guidelines.</li>
  </ul>

  

  <!-- Section 3: Purpose of the Lab (Heading: 11px | Body & List: 9px) -->
  <h2 style="font-size: 11px; font-weight: bold; margin-top: 15px; color: #1a0dab;">
  
  <span>🛡️<span/>Purpose of the Lab
  </h2>
  <p style="font-size: 9px; margin: 4px 0;">
    In cybersecurity, having an isolated, repeatable, and well-understood lab environment is paramount. This lab ensures that:
  </p>
  <ul style="font-size: 9px; margin: 4px 0; padding-left: 15px;">
    <li>Students can practice offensive and defensive security techniques without risking production networks or violating laws.</li>
    <li>Fundamental networking concepts (IP subnetting, default gateways, and TCP/IP behavior) are reinforced through hands-on observation.</li>
    <li>Standardized reporting templates are established for documenting technical lab results.</li>
  </ul>

  

  <!-- Section 4: Lab Architecture (Heading: 11px | Text & Code: 9px) -->
  <h2 style="font-size: 11px; font-weight: bold; margin-top: 15px; color: #1a0dab;">
    <span>🏗️ </span> Lab Architecture
  </h2>
  <p style="font-size: 9px; margin: 4px 0;">
    The lab uses a hybrid host-guest virtualization model supported by Oracle VM VirtualBox and custom NAT network configurations[cite: 3, 5]:

    
  </p>
  <pre style="font-size: 9px; background-color: #f4f4f4; padding: 6px; border: 1px solid #ddd; font-family: monospace;">

  

  <img width="1920" height="1080" alt="3-screenshot-title-image png" src="https://github.com/user-attachments/assets/78787dad-6254-4420-bba0-de7bd862638c" />


  


  <!-- Section 5: Lab Configuration (Heading: 11px | List: 9px) -->

  
  <h2 style=font-size: 11px; font-weight: bold; align=center; margin-top: 15px; color: #1a0dab;">
    
  <span>⚙️</span>Lab Configuration
    
  </h2>
  <ul style=font-size: 9px; margin: 4px 0; aligncenter;padding-left: 15px;">
    <li><strong>Hypervisor Version:</strong> Oracle VM VirtualBox 7.x[cite: 3, 5]</li>
    <li><strong>Guest OS:</strong> Kali Linux (XFCE Desktop)[cite: 5, 6]</li>
    <li><strong>Virtual Hardware Specs:</strong> 2 vCPUs, 2048 MB+ Base Memory[cite: 5]</li>
    <li><strong>Network Addressing Scheme:</strong> NAT Network configured with IPv4 Prefix <code>10.0.0.0/24</code> and DHCP enabled[cite: 3]</li>
  </ul>

</div>



<span>🐞<span/>Problems Encountered & Solutions


<table border="1" cellpadding="8" cellspacing="0" style="border-collapse: collapse; width: 100%;">
  
  <thead>
    <tr style="background-color: #f2f2f2;">
      <th style="text-align: left; padding: 8px;">Problem Encountered</th>
      <th style="text-align: left; padding: 8px;">Root Cause</th>
      <th style="text-align: left; padding: 8px;">Solution Applied</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="padding: 8px;"><strong>No IP Address assigned to Kali VM</strong></td>
      <td style="padding: 8px;">Default VirtualBox NAT mode was blocking inbound/outbound local segment bridging.</td>
      <td style="padding: 8px;">Switched VirtualBox adapter setting from <em>NAT</em> to <strong>Bridged Adapter</strong> matching the active host network card, then restarted networking (<code>sudo systemctl restart networking</code>).</td>
    </tr>
    <tr>
      <td style="padding: 8px;"><strong>Nmap "Permission Denied" / Raw Sockets Error</strong></td>
      <td style="padding: 8px;">Standard user accounts lack privileges to send raw ICMP/SYN packets.</td>
      <td style="padding: 8px;">Pre-pended <code>sudo</code> to the Nmap command or executed the session as the root user.</td>
    </tr>
    <tr>
      <td style="padding: 8px;"><strong>Host Firewall blocking ping responses</strong></td>
      <td style="padding: 8px;">Windows Defender Firewall dropping ICMP echo requests originating from the VM.</td>
      <td style="padding: 8px;">Allowed File and Printer Sharing (Echo Request - ICMPv4-In) in Windows Defender Firewall rules.</td>
    </tr>
  </tbody>
</table>


<div style="font-family: Arial, sans-serif; color:#333; line-height: 1.4;">

  <!-- Section Heading (Font Size 11px) -->
  <h2 style="font-size: 11px; font-weight: bold; align:center;margin-top: 15px; color: #1a0dab;">
    
  <span>🛠️</span>Lab Setup Procedure
  </h2>

  <!-- Step 1 (Subheading: 10px | Text/List: 9px) -->
  <h3 style="font-size: 10px; font-weight: bold; margin-top: 10px;">Step 1: Install 7-Zip</h3>
  <p style="font-size: 9px; margin: 2px 0;"><strong>Purpose:</strong> To extract compressed archive files (such as .7z, .zip, or archive bundles) that are frequently packaged with virtual machine images or lab software.</p>
  <ul style="font-size: 9px; margin: 2px 0; padding-left: 15px;">
    <li>Go to the official 7-Zip download page[cite: 2].</li>
    <li>Download the appropriate installer for your host operating system (e.g., 64-bit Windows x64 .exe)[cite: 2].</li>
    <li>Run the installer executable and click Install to complete the wizard in your destination folder[cite: 2].</li>

  <img width="100%" height="1080" alt="2-screenshot-title-image png" src="https://github.com/user-attachments/assets/3ad22a42-02b5-4eff-8b76-c51dcf319fdb" />

  </ul>

  <!-- Step 2 (Subheading: 10px | Text/List: 9px) -->
  <h3 style="font-size: 10px; font-weight: bold; margin-top: 10px;">Step 2: Install VirtualBox</h3>
  <p style="font-size: 9px; margin: 2px 0;"><strong>Purpose:</strong> To provide the hypervisor environment required to run virtual machines on your host computer[cite: 3, 5].</p>
  <ul style="font-size: 9px; margin: 2px 0; padding-left: 15px;">
    <li>Download the Oracle VM VirtualBox installer and Extension Pack for your host OS[cite: 3, 5].</li>
    <li>Run the installer with administrative privileges.</li>
    <li>Accept the default settings, allow the network interface installation prompts (which may briefly reset your network connection), and finish the wizard.</li>

   <img width="100%" height="1080" alt="5-screenshot-title-image png" src="https://github.com/user-attachments/assets/0a44490a-e77f-4ed6-b611-fe0d9a2fe3d3" />

  </ul>

  <!-- Step 3 (Subheading: 10px | Text/List: 9px) -->
  <h3 style="font-size: 10px; font-weight: bold; margin-top: 10px;">Step 3: Create the NAT Network</h3>
  <p style="font-size: 9px; margin: 2px 0;"><strong>Purpose:</strong> To establish a secure, isolated virtual network where multiple guest virtual machines can communicate with each other and the internet without exposing raw host interfaces directly[cite: 3].</p>
  <ul style="font-size: 9px; margin: 2px 0; padding-left: 15px;">
    <li>Open Oracle VM VirtualBox Manager[cite: 3].</li>
    <li>Go to the top menu and select File > Tools > Network Manager (or click Network from the top bar)[cite: 3].</li>
    <li>Switch to the NAT Networks tab and click Create[cite: 3].</li>
    <li>Configure the network properties with an IPv4 Prefix (e.g., 10.0.0.0/24) and ensure Enable DHCP is checked. Click Apply[cite: 3].</li>

  <img width="100%" height="1080" alt="3-screenshot-title-image png" src="https://github.com/user-attachments/assets/5f68db21-7115-4165-8e46-ee4068092a99" />

  </ul>

  <!-- Step 4 (Subheading: 10px | Text/List: 9px) -->
  <h3 style="font-size: 10px; font-weight: bold; margin-top: 10px;">Step 4: Import Kali Linux</h3>
  <p style="font-size: 9px; margin: 2px 0;"><strong>Purpose:</strong> To provision the penetration testing guest operating system into your hypervisor[cite: 4, 5].</p>
  <ul style="font-size: 9px; margin: 2px 0; padding-left: 15px;">
    <li>Go to the official Kali Linux downloads website and navigate to the Pre-built VMs section[cite: 4].</li>
    <li>Download the pre-built VirtualBox appliance (.ova or .vdi)[cite: 4, 5].</li>
    <li>Import the appliance into VirtualBox by double-clicking the file or selecting File > Import Appliance in VirtualBox Manager[cite: 5].</li>
    <li>Allocate appropriate resources (at least 2 CPU cores and 4 GB / 2048 MB+ RAM)[cite: 5].</li>

  <img width="1920" height="1080" alt="4-screenshot-title-image png" src="https://github.com/user-attachments/assets/9a9e2e30-db6f-426d-8aab-07080a17c22c" />


  </ul>

  <!-- Step 5 (Subheading: 10px | Text/List: 9px) -->
  <h3 style="font-size: 10px; font-weight: bold; margin-top: 10px;">Step 5: Configure the Kali Linux Network</h3>
  <p style="font-size: 9px; margin: 2px 0;"><strong>Purpose:</strong> To attach the Kali Linux virtual machine to the custom NAT network created in Step 3 so it has proper isolated IP connectivity[cite: 3, 5].</p>
  <ul style="font-size: 9px; margin: 2px 0; padding-left: 15px;">
    <li>Select your imported Kali Linux VM in VirtualBox Manager and click Settings[cite: 5].</li>
    <li>Navigate to the Network tab[cite: 5].</li>
    <li>Under Adapter 1, change the "Attached to" dropdown from NAT to NAT Network[cite: 3, 5].</li>
    <li>Select the NAT Network name you created earlier (NatNetwork) and click OK[cite: 3].</li>
    <li>Power on the VM, log in (default username: kali, password: kali), and open a terminal to verify the IP address using ip a[cite: 5, 6].</li>

    
  </ul>

  <!-- Step 6 (Subheading: 10px | Text/List: 9px) -->
  <h3 style="font-size: 10px; font-weight: bold; margin-top: 10px;">Step 6: Create a Clean VM Snapshot</h3>
  <p style="font-size: 9px; margin: 2px 0;"><strong>Purpose:</strong> To save a baseline, known-good state of the virtual machine right after initial configuration so you can easily revert back if any future lab experiment breaks the system[cite: 5].</p>
  <ul style="font-size: 9px; margin: 2px 0; padding-left: 15px;">
    <li>Ensure the Kali Linux virtual machine is fully powered off or in a saved state[cite: 5].</li>
    <li>In VirtualBox Manager, click the menu next to the VM name or go to the Snapshots menu (hamburger/stacked icon next to Details)[cite: 5].</li>
    <li>Click Take (Take Snapshot)[cite: 5].</li>
    <li>Enter a descriptive snapshot name (e.g., Baseline-Fresh-Install) and a description detailing that the network and tools are configured[cite: 5].</li>

 <img width="100%" height="509" alt="6-screenshot-title-image png - Copy" src="https://github.com/user-attachments/assets/148d643f-ebd7-48d6-9cb2-925509634cc7" />


  </ul>

  

  <div style="font-family: Arial, sans-serif; color: #333; line-height: 1.4;">

  <!-- Section 7: Lab Verifications -->
  <h2 style="font-size: 11px; font-weight: bold; margin-top: 15px; color: #1a0dab;">
    
  <span>🔍<span/> Lab Verifications
  
  </h2>
  <ul style="font-size: 9px; margin: 4px 0; padding-left: 15px;">
    <li><strong>IP Assignment Check:</strong> Verified that the Kali VM successfully acquired a valid IP address on the local NAT network subnet (`10.0.0.x`)[cite: 3, 5].</li>
    <li><strong>Ping Sweep Verification:</strong> Executed a host discovery scan across the subnet to identify live nodes:
      <code style="font-size: 9px; background-color: #f4f4f4; padding: 2px 4px;">nmap -sn 10.0.0.0/24</code>
      <br><em>Result:</em> Successfully listed active hosts within the isolated virtual environment[cite: 3].
    </li>
    <li><strong>Port Scan Verification:</strong> Ran a TCP SYN scan against the test target to confirm service availability[cite: 6].</li>
  </ul>

  <!-- Section 8: Problem Encountered and Solutions -->
  <h2 style="font-size: 11px; font-weight: bold; margin-top: 15px; color: #1a0dab;">
  
    
  <span>⚠️</span>Problem Encountered and Solutions
  
  
  </h2>
  <table border="1" cellpadding="6" cellspacing="0" style="border-collapse: collapse; width: 100%; font-size: 9px; margin-top: 5px;">
    <thead>
      <tr style="background-color: #f2f2f2; font-size: 10px;">
        <th style="text-align: left; padding: 6px;">Problem Encountered</th>
        <th style="text-align: left; padding: 6px;">Root Cause</th>
        <th style="text-align: left; padding: 6px;">Solution Applied</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td style="padding: 6px;"><strong>No IP Address assigned to Kali VM</strong></td>
        <td style="padding: 6px;">Default VirtualBox network attachment was not properly linked to the custom NAT network segment[cite: 3, 5].</td>
        <td style="padding: 6px;">Switched VirtualBox adapter setting to <em>NAT Network</em> (`NatNetwork`), then restarted networking[cite: 3, 5].</td>
      </tr>
      <tr>
        <td style="padding: 6px;"><strong>Nmap "Permission Denied" / Raw Sockets Error</strong></td>
        <td style="padding: 6px;">Standard user accounts lack privileges to send raw ICMP/SYN packets.</td>
        <td style="padding: 6px;">Pre-pended <code>sudo</code> to the Nmap command or executed the session as the root user.</td>
      </tr>
      <tr>
        <td style="padding: 6px;"><strong>Host Firewall blocking ping responses</strong></td>
        <td style="padding: 6px;">Host firewall dropping ICMP echo requests originating from the virtual segment.</td>
        <td style="padding: 6px;">Allowed ICMP/Echo Request rules in the host firewall settings.</td>
      </tr>
    </tbody>
  </table>

  

  <!-- Section 9: What I Learned -->
  <h2 style="font-size: 11px; font-weight: bold; margin-top: 15px; color: #1a0dab;">

    
  <span>💡<span/> What I Learned
  


  </h2>
  <ul style="font-size: 9px; margin: 4px 0; padding-left: 15px;">
    <li><strong>Virtualization Dynamics:</strong> Gained practical proficiency in configuring hypervisor virtual networks (`NatNetwork`) and managing guest resource allocation[cite: 3, 5].</li>
    <li><strong>Reconnaissance Fundamentals:</strong> Understood how Nmap constructs packet flags to map network topologies and discover running services[cite: 6].</li>
    <li><strong>Troubleshooting Methodology:</strong> Developed a systematic approach to diagnosing packet routing and interface configuration issues between host hypervisors and guest virtual machines[cite: 3, 5].</li>
  </ul>

  

  <!-- Section 10: Security and Ethical Use -->
  <h2 style="font-size: 11px; font-weight: bold; margin-top: 15px; color: #1a0dab;">
    <span>🛡️</span></san>Security and Ethical Use

    
  </h2>

  
  <ul style="font-size: 9px; margin: 4px 0; padding-left: 15px;">
    <li><strong>Scope of Engagement:</strong> All scanning and reconnaissance activities were restricted strictly to our isolated lab subnet (`10.0.0.0/24`) and authorized test targets[cite: 3].</li>
    <li><strong>Legal Compliance:</strong> Adhered strictly to ethical hacking guidelines, ensuring no unauthorized external systems were probed or scanned without explicit permission.</li>
  </ul>

  <!-- Section 11: Tools and Resources -->
  <h2 style="font-size: 11px; font-weight: bold; margin-top: 15px; color: #1a0dab;">
    
   <span>🧰</span> Tools and Resources
  </h2>
  
  <ul style="font-size: 9px; margin: 4px 0; padding-left: 15px;">
    <li><strong>7-Zip:</strong> Archive utility used for handling compressed installer packages[cite: 2].</li>
    <li><strong>Oracle VM VirtualBox:</strong> Hypervisor platform for running virtual machines[cite: 3, 5].</li>
    <li><strong>Kali Linux:</strong> Penetration testing Linux distribution[cite: 4, 5, 6].</li>
    <li><strong>Nmap / Zenmap:</strong> Network exploration tool and security scanner.</li>
  </ul>

  

  <!-- Section 12: Author -->
  <h2 style="font-size: 11px; font-weight: bold; margin-top: 15px; color: #1a0dab;">
    
  <span>👤</span> Author
  
  </h2>
  
  <p style="font-size: 9px; margin: 4px 0;">
    <strong>Project Author:</strong> Kaveesha Heshani <br>
    <strong>LinkedIn :</strong>  https://www.linkedin.com/in/kaveesha-heshani-7b942537b?utm_source=share_via&utm_content=profile&utm_medium=member_android  <br>
    <strong>Course/Module:</strong> Networkwalks Cybersecurity Program – Week 1, Project Module 1 
  </p>

</div>

</div>


