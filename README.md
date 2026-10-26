<div style="font-family: Arial, sans-serif; color: #333; line-height: 1.4;">

  <!-- Main Topic (Font Size 12px) -->
  <h1 style="font-size: 12px;font-color:Light Blue; font-weight: bold; border-bottom: 2px ; padding-bottom: 4px;">
            Cybersecurity Lab Environment Setup & Initial Reconnaissance
  </h1>

  <!-- Section 1: Project View (Heading: 11px | Body: 9px) -->
  <h2 style="font-size: 11px; font-weight: bold; margin-top: 15px; color: #1a0dab;">
    1. Project View
  </h2>
  <p style="font-size: 9px; margin: 4px 0;">
    This project establishes a foundational, secure, and isolated cybersecurity testing environment. It details the deployment of a virtualization hypervisor (Oracle VM VirtualBox), the provisioning of a penetration testing operating system (Kali Linux), and the configuration of essential network reconnaissance utilities.
  </p>

  <!-- Section 2: Objectives (Heading: 11px | List: 9px) -->
  <h2 style="font-size: 11px; font-weight: bold; margin-top: 15px; color: #1a0dab;">
    2. Objectives
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
    3. Purpose of the Lab
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
    4. Lab Architecture
  </h2>
  <p style="font-size: 9px; margin: 4px 0;">
    The lab uses a hybrid host-guest virtualization model supported by Oracle VM VirtualBox and custom NAT network configurations[cite: 3, 5]:
  </p>
  <pre style="font-size: 9px; background-color: #f4f4f4; padding: 6px; border: 1px solid #ddd; font-family: monospace;">

    <img width="1920" height="1080" alt="3-screenshot-title-image png" src="https://github.com/user-attachments/assets/78787dad-6254-4420-bba0-de7bd862638c" />


  <!-- Section 5: Lab Configuration (Heading: 11px | List: 9px) -->
  <h2 style="font-size: 11px; font-weight: bold; margin-top: 15px; color: #1a0dab;">
    5. Lab Configuration
  </h2>
  <ul style="font-size: 9px; margin: 4px 0; padding-left: 15px;">
    <li><strong>Hypervisor Version:</strong> Oracle VM VirtualBox 7.x[cite: 3, 5]</li>
    <li><strong>Guest OS:</strong> Kali Linux (XFCE Desktop)[cite: 5, 6]</li>
    <li><strong>Virtual Hardware Specs:</strong> 2 vCPUs, 2048 MB+ Base Memory[cite: 5]</li>
    <li><strong>Network Addressing Scheme:</strong> NAT Network configured with IPv4 Prefix <code>10.0.0.0/24</code> and DHCP enabled[cite: 3]</li>
  </ul>

</div>

🐞 Problems Encountered & Solutions


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


<div style="font-family: Arial, sans-serif; color: #333; line-height: 1.4;">

  <!-- Section Heading (Font Size 11px) -->
  <h2 style="font-size: 11px; font-weight: bold; margin-top: 15px; color: #1a0dab;">
    6. Lab Setup Procedure
  </h2>

  <!-- Step 1 (Subheading: 10px | Text/List: 9px) -->
  <h3 style="font-size: 10px; font-weight: bold; margin-top: 10px;">Step 1: Install 7-Zip</h3>
  <p style="font-size: 9px; margin: 2px 0;"><strong>Purpose:</strong> To extract compressed archive files (such as .7z, .zip, or archive bundles) that are frequently packaged with virtual machine images or lab software.</p>
  <ul style="font-size: 9px; margin: 2px 0; padding-left: 15px;">
    <li>Go to the official 7-Zip download page[cite: 2].</li>
    <li>Download the appropriate installer for your host operating system (e.g., 64-bit Windows x64 .exe)[cite: 2].</li>
    <li>Run the installer executable and click Install to complete the wizard in your destination folder[cite: 2].</li>
  </ul>

  <!-- Step 2 (Subheading: 10px | Text/List: 9px) -->
  <h3 style="font-size: 10px; font-weight: bold; margin-top: 10px;">Step 2: Install VirtualBox</h3>
  <p style="font-size: 9px; margin: 2px 0;"><strong>Purpose:</strong> To provide the hypervisor environment required to run virtual machines on your host computer[cite: 3, 5].</p>
  <ul style="font-size: 9px; margin: 2px 0; padding-left: 15px;">
    <li>Download the Oracle VM VirtualBox installer and Extension Pack for your host OS[cite: 3, 5].</li>
    <li>Run the installer with administrative privileges.</li>
    <li>Accept the default settings, allow the network interface installation prompts (which may briefly reset your network connection), and finish the wizard.</li>
  </ul>

  <!-- Step 3 (Subheading: 10px | Text/List: 9px) -->
  <h3 style="font-size: 10px; font-weight: bold; margin-top: 10px;">Step 3: Create the NAT Network</h3>
  <p style="font-size: 9px; margin: 2px 0;"><strong>Purpose:</strong> To establish a secure, isolated virtual network where multiple guest virtual machines can communicate with each other and the internet without exposing raw host interfaces directly[cite: 3].</p>
  <ul style="font-size: 9px; margin: 2px 0; padding-left: 15px;">
    <li>Open Oracle VM VirtualBox Manager[cite: 3].</li>
    <li>Go to the top menu and select File > Tools > Network Manager (or click Network from the top bar)[cite: 3].</li>
    <li>Switch to the NAT Networks tab and click Create[cite: 3].</li>
    <li>Configure the network properties with an IPv4 Prefix (e.g., 10.0.0.0/24) and ensure Enable DHCP is checked. Click Apply[cite: 3].</li>
  </ul>

  <!-- Step 4 (Subheading: 10px | Text/List: 9px) -->
  <h3 style="font-size: 10px; font-weight: bold; margin-top: 10px;">Step 4: Import Kali Linux</h3>
  <p style="font-size: 9px; margin: 2px 0;"><strong>Purpose:</strong> To provision the penetration testing guest operating system into your hypervisor[cite: 4, 5].</p>
  <ul style="font-size: 9px; margin: 2px 0; padding-left: 15px;">
    <li>Go to the official Kali Linux downloads website and navigate to the Pre-built VMs section[cite: 4].</li>
    <li>Download the pre-built VirtualBox appliance (.ova or .vdi)[cite: 4, 5].</li>
    <li>Import the appliance into VirtualBox by double-clicking the file or selecting File > Import Appliance in VirtualBox Manager[cite: 5].</li>
    <li>Allocate appropriate resources (at least 2 CPU cores and 4 GB / 2048 MB+ RAM)[cite: 5].</li>
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
  </ul>

</div>


