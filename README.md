# Cybersecurity Adversary Simulation & Detection Lab

## Objective

There are so many great resources on how to build a proper cybersecurity lab. Tony Robinson's ["Building Virtual Machine Labs"](https://leanpub.com/avatar2) is choose your own adventure guide on how to set up a lab on Mac, Linux, and Windows with the hypervisor of your own choosing! Content creator Day (aka CyberwoxAcademy) has a [great guide on setting up a Security Onion/Splunk centric homelab](https://cyberwoxacademy.com/building-a-cybersecurity-homelab-for-detection-monitoring/). 

But I do have to say, I have not seen one with as much breadth as the [10-part beast-of-a-guide](https://blog.davidvarghese.net/posts/building-home-lab-part-1/) by David Varghese. Be warned! Putting this one together is a serious test of one's endurance and patience. I framed my entire lab off of this design. So thank you very much Mr. Varghese for laying down the foundation of this lab!

Some of you who have come may have already put together a lab, only to let it rot afterwards. And when you do decided come back, your documentation is so bad that you may be better off scrapping it altogether! Rather than reinvent the wheel, my main objective here is to make use of your lab after putting it together! As you'll see, I combine a lot of built out resources like OWASP Juice Shop and Damn Vulnerable Web Application (DVWA), get an IPS/IDS installed and configured on the servers, plug them into the SIEM server you will have already built out, attack and then analyze! 

This cybersecurity homelab is designed to provide hands-on experience in both offensive (Red Team) and defensive (Blue Team) security. The primary goal is to:

✅ Develop hands-on Blue Team expertise by setting up and analyzing SIEM logs, network traffic, and endpoint security alerts to understand real-world detection methodologies.
✅ Simulate real-world adversary tactics to gain insight into how attackers operate while using defensive technologies to monitor, analyze, and mitigate attacks.
✅ Strengthen cybersecurity fundamentals by deploying and securing critical infrastructure, including web applications, Active Directory, and forensic analysis tools.
✅ Enhance detection evasion techniques by studying security monitoring tools and identifying gaps in logging, SIEM filtering, and network defenses.
✅ Build practical cybersecurity experience through offensive and defensive lab exercises, ensuring readiness for both SOC analyst and future Red Team roles.

The lab is structured as a multi-subnet network running in VirtualBox, managed by pfSense as the core firewall/router. It includes offensive, defensive, and analysis systems to support both attack simulation and forensic analysis.

## Network Architecture Overview

This lab consists of five core subnets, each designed for a specific purpose:

                   +-------------------+
                   |  VirtualBox Host  |
                   +---------+---------+
                             |
             +---------------+----------------+
             |    pfSense Firewall & Router   |
             +---------------+----------------+
                             |
         -------------------------------------------------
        |            |           |            |           |
    (Red Team)  (Vuln Lab)  (Blue Team)  (Active Dir) (Malware)
    Attack Sub  Target Sub   Analysis     AD Subnet    Sandbox
  


### Red Team (Attacking & Management Machine)
- Hosts Kali Linux as the primary attacking system, also used for managing the lab.
- Functions as the offensive operations center for penetration testing, reconnaissance, and exploit research.

### Vulnerable Machines (Target Systems)
- Hosts Metasploitable 2, VulnHub VMs, and a custom Ubuntu server with DVWA and OWASP Juice Shop.
- Designed for exploit development, vulnerability scanning, and adversary simulation.

### Blue Team (Detection & Forensics)
- Hosts Tsurugi Linux (Forensic Distro) and Splunk.
- Used for SIEM log analysis, network forensics, and malware analysis.

### Active Directory (Windows Domain Network)
- Windows Server 2019 (Domain Controller)
- Two Windows 10 Enterprise Workstations
- Used for Active Directory attacks, Kerberoasting, Pass-the-Hash, and AD enumeration.

### Isolated Malware Analysis Network
- Used for sandboxing malware samples and analyzing behavior.
- Completely air-gapped from other networks.

## Subprojects

1️⃣ OWASP Juice Shop & Splunk Integration
Summary: Built a vulnerable web app integrated with Splunk to analyze security threats and attack patterns.
Key Features:
  - Configured log forwarding from Juice Shop to Splunk.
  - Built Splunk dashboards to detect SQL injection, XSS, and brute-force attempts.
  - Simulated real-world attack traffic and monitored detections.
Platforms Used: Ubuntu, VirtualBox, Docker, Splunk, OWASP Juice Shop.

2️⃣ Automated Web Traffic Simulation & Analysis
Summary: Developed AI-assisted traffic bots using Selenium & Playwright to mimic real-world browsing behavior.
Key Features:
  - Automated traffic to simulate human-like interactions.
  - Analyzed bot detection techniques and evasions.
  - Configured Splunk SIEM to detect anomalies.
Platforms Used: Ubuntu, Docker, Playwright, Selenium, Splunk.

3️⃣ DVWA Security Analysis & SIEM Integration
Summary: Conducted web attack simulations against Damn Vulnerable Web App (DVWA) with Splunk log analysis.
Key Features:
 - Configured SIEM alerts for SQL injection and XSS.
 - Used Burp Suite, Nmap, and Wireshark for deep packet analysis.
 - Simulated brute-force attacks against login forms.
Platforms Used: Ubuntu, Apache2, MariaDB, Splunk, DVWA.


