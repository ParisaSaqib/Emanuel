## Emmanuel-Ethical-Hacking-Project
## Disclaimer:

The project described herein, including the methodologies, tools, and techniques employed, is presented solely for educational and instructional purposes. It is not intended for malicious or unauthorized use. The project's objective was to simulate various cybersecurity scenarios to enhance understanding and knowledge in the fields of network security, industrial control systems, and cybersecurity. Any actions or simulations described involving potential attacks, modifications to PLC code, or network configurations were conducted in a controlled, educational environment with explicit permission and under supervision.

The project does not endorse, encourage, or condone any illegal or unauthorized activities. All information, tools, and techniques provided are for educational purposes only. Users are advised to use this information responsibly and within the boundaries of applicable laws, regulations, and ethical standards.

## Objective


Our project aimed to simulate a sophisticated cyber attack scenario where an unsuspecting user clicks on a malicious link from a phishing email, leading to the download of a disguised PowerShell script. This script facilitated unauthorized remote access to the Domain Controller (DC) and DNS server, enabling the attacker to gather sensitive information from the maintenance workstation and forcibly change user credentials. Furthermore, the attack extended to modifying the Programmable Logic Controller (PLC) code, causing the water tank to overflow, demonstrating potential physical harm resulting from cyber vulnerabilities.

### Skills Learned

- Configuration and rules management using pfSense for firewall and router security.
- Management of servers including Domain Controller (DC), DNS server, and maintenance server, with emphasis on remote administration and maintenance.
- Utilization of obfuscation techniques to disguise malicious code and enhance cybersecurity defenses.
- Proficiency in modifying Programmable Logic Controller (PLC) code for industrial automation and control systems.
- Implementation of networking solutions, including VLANs, subnets, and routing, to optimize network performance and security.
- Hands-on experience using various tools to simulate cyber attacks, enhancing understanding of attack vectors and defense strategies.
- Familiarity with cybersecurity best practices and methodologies in assessing and securing network infrastructure.

  
### Tools Used

- Click PLC: Controls inlet and outlet pumps of a water tank, including PIT for water level measurement.
- pfSense: Firewall and router configuration and management.
- Canva: Network design tool.
- VMware: Virtualization platform for network simulation.
- Windows Server 2022: Used as Domain Controller (DC), DNS server, maintenance management server, and Windows Server in Operational Technology (OT).
- Windows: Client and admin operating system for both OT and IT environments.
- Kali Linux: Used as an attacker platform for simulating attacks.
- Wireshark: Network protocol analyzer for monitoring and analyzing network traffic.
- Obfuscation Tools: Used for obfuscating code to protect intellectual property or sensitive information.
- Website Spoofing Attack Tools: Tools designed to simulate and test website spoofing attacks.
- HMIs (Human-Machine Interfaces): Interfaces used for monitoring and controlling industrial processes.
- PLC (Programmable Logic Controller): Used for automation and control of machinery and processes in industrial settings.
- Water Tank: Part of the physical infrastructure used for simulation and testing purposes in the project.


## Steps
Here's a step-by-step summary for the project described:

1. **Network Setup and Design**
   a. Set up a hybrid network using VMware Workstation 17 Pro.
   ![image](https://github.com/ParisaSaqib/Emanuel-Ethical-Hacking-Project/assets/96464987/424dcfcc-e7c0-4a1f-b5db-254770d8df4b)


   b. Configure pfSense for firewall and router functions for both IT and OT networks.
   - Always look into Advanced setting, static routes, and your rules while configuring pfSense. The defualt (*) does not apply to all conditions, hence, sometimes there is a need to configure rules manually. The example of rules set up below is for the first pfsense acting as a firewall and router.
   - To avoid routing loops, configure static routes.
   - If you want to connect your pfSense to internet, keep one interface connected through DHCP.
   - You can ping from each interface to another one to make sure of connectivity.
   - Through pfsense itself, you can configure basics, and if interested, try to configure web page for more user friendly setting.
     
![pfsense 1](https://github.com/ParisaSaqib/Emanuel-Ethical-Hacking-Project/assets/96464987/3bbde5a1-ef2e-469a-926f-abdd6520ec81)
![pfsense2](https://github.com/ParisaSaqib/Emanuel-Ethical-Hacking-Project/assets/96464987/7e6c26e8-99be-4427-8463-53e2969b1b99)
![pfsense3](https://github.com/ParisaSaqib/Emanuel-Ethical-Hacking-Project/assets/96464987/f09ed949-0e20-425e-adef-4592004e7f1d)
![pfsense 4](https://github.com/ParisaSaqib/Emanuel-Ethical-Hacking-Project/assets/96464987/9964b291-d114-4bac-9cc6-25bf3fa2d3dd)

   c. Integrate Windows Server 2022 for domain controller, DNS, and maintenance management.
   d. Design network with IT (Enterprise) and OT (Supervisor and Process Control) levels, connected through routers and firewalls.
   
 ![image](https://github.com/ParisaSaqib/Emanuel-Ethical-Hacking-Project/assets/96464987/c9c203a8-0eaa-4f2b-a99d-26841026022b)

3. **OT Process Implementation**
   a. Deploy a physical tank system with inlet and outlet pumps controlled by a CLICK PLC.
    PLC controls an inlet and outlet pump of a water tank with a PIT to discover % of water in the tank
    When water level below 30%, runs inlet pump until 60% full before stopping
    When water level is above 80%, runs outlet pump until 50% empty before stopping
   
![image](https://github.com/ParisaSaqib/Emanuel-Ethical-Hacking-Project/assets/96464987/3b815e68-76b9-4bdb-a496-d3e66504d394)
![image](https://github.com/ParisaSaqib/Emanuel-Ethical-Hacking-Project/assets/96464987/7297d7c8-2964-4bf5-8ad2-a2b29c5378ef)

   b. Utilize AutomationDirect HMI to monitor and control tank operations.
   Screen 1: Start and stop pushbutton and an indicator of if the system is running
   Screen 2: Indicator of status of inlet and outlet pump, percentage of water in the tank in numerical values and graphical view
   Both have change screen buttons
   
![image](https://github.com/ParisaSaqib/Emanuel-Ethical-Hacking-Project/assets/96464987/531f48d5-baa5-4d40-9c5a-851e1efcd8db)
![image](https://github.com/ParisaSaqib/Emanuel-Ethical-Hacking-Project/assets/96464987/c09c0cf4-0086-4afb-9af9-fbadc6b06c02)

   c. Integrate a Pressure Indicating Transmitter (PIT) to measure water levels in the tank.

5. **Attack Simulation**
   a. Send a phishing email spoofed as AutomationDirect, enticing users to download a driver update.
   
   ![image](https://github.com/ParisaSaqib/Emanuel-Ethical-Hacking-Project/assets/96464987/186939a9-8a17-4c3c-9635-623d57681f98)

   b. Victim clicks on the link and unwittingly downloads a malicious PowerShell script (DriverUpdate.ps1) that establishes a reverse shell.
   
     ![image](https://github.com/ParisaSaqib/Emanuel-Ethical-Hacking-Project/assets/96464987/8c7a5e74-1e79-4f01-97d8-9ada6b02ec9e)

   c. Attacker gains remote access to the victim's workstation and escalates privileges to access the MaintenanceWorkstationUP.
   
   ![image](https://github.com/ParisaSaqib/Emanuel-Ethical-Hacking-Project/assets/96464987/e30dde1e-2b4e-43dd-88fb-15953e2a6b85)

   d. Modify the ladder logic on the CLICK PLC to cause the tank to overflow.
   
   ![image](https://github.com/ParisaSaqib/Emanuel-Ethical-Hacking-Project/assets/96464987/58335e85-520d-467c-a910-08a507336d6b)

   e. Change the IP address of the PLC to disrupt communication with the HMI, further compromising operations.
     
![image](https://github.com/ParisaSaqib/Emanuel-Ethical-Hacking-Project/assets/96464987/c4066170-472b-415f-a93b-b8c166052720)
![image](https://github.com/ParisaSaqib/Emanuel-Ethical-Hacking-Project/assets/96464987/e77f41a9-de29-484c-81ec-fd8412ba2f53)


8. **Technical Challenges and Solutions**
   a. Address VMware network connectivity issues and firewall configuration challenges with pfSense.
   b. Troubleshoot communication problems between IT and OT networks, including routing and firewall rules.
   c. Resolve hardware and software integration issues with CLICK PLC, HMI, and PIT.

9. **Recommendations**
   - Implement a Demilitarized Zone (DMZ) to segregate IT and OT networks, enhancing security.
   - Strengthen firewall rules and access controls to prevent lateral movement within the network.
   - Introduce network monitoring tools and regular patching to mitigate future vulnerabilities.
   - Install physical alarms and emergency switches on the OT plant for immediate response to critical situations.

![image](https://github.com/ParisaSaqib/Emanuel-Ethical-Hacking-Project/assets/96464987/2e27ad0e-7026-4e38-9c0c-0b4eb26ddaee)


## References 
- Firewall — Rule methodology | PfSense Documentation. (n.d.). https://docs.netgate.com/pfsense/en/latest/firewall/rule-methodology.html
- The Network Berg. (2022, June 13). pfSense Firewall (totally) Rules! Basic rule setup. . .🤫[Video]. YouTube. https://www.youtube.com/watch?v=Vm98ofYp05g

## Acknowledgement:

This project was completed in collaboration with Marian Aquilizan and Maggie Pan as our culminating project for Industrial Network Cybersecurity program at BCIT. Their contributions and teamwork were invaluable to the successful execution of this project.


