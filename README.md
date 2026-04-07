# Linux Firewall Configuration & Hardening (UFW)

 This project demonstrates how to harden a Linux system using UFW (Uncomplicated Firewall).
 The goal is to configure firewall rules, restrict SSH access, enable logging,
 verify active rules, and understand where firewall settings are stored.


# Step 1: Check Firewall Status


sudo ufw status verbose

Shows if firewall is active and lists current rules



# Step 2: Enable the Firewall


sudo ufw enable

Turns on the firewall and begins enforcing rules



# Step 3: Set Default Policies


sudo ufw default deny incoming

sudo ufw default allow outgoing

sudo ufw status verbose

deny incoming = blocks unauthorized inbound traffic

allow outgoing = allows normal outbound traffic



# Step 4: Enable Logging


sudo ufw logging on

Enables firewall logging

sudo journalctl -u ufw --no-pager

sudo tail -f /var/log/ufw.log

View firewall logs (real-time monitoring)



# Step 5: Allow Required Services

# Allow SSH

sudo ufw allow ssh

sudo ufw allow 22/tcp

# Allow HTTP/HTTPS

sudo ufw allow http

sudo ufw allow https

sudo ufw allow 80/tcp

sudo ufw allow 443/tcp

# Allow ICMP (ping)

sudo ufw allow icmp



# Step 6: Restrict SSH to Specific IP


sudo ufw allow from 192.168.1.100 to any port 22

Only allows SSH access from this IP (more secure)



# Step 7: Allow Trusted Network


sudo ufw allow from 192.168.1.0/24

Allows traffic from entire subnet



# Step 8: Block Unwanted Traffic


# Block specific IP

sudo ufw deny from 203.0.113.5

Block subnet

sudo ufw deny from 203.0.113.0/24

Block FTP port

sudo ufw deny 21/tcp

Reduces attack surface



# Step 9: Verify Firewall Rules


sudo ufw status numbered

sudo ufw show raw

sudo ufw default

Shows active rules and default policies

Delete rule by number

sudo ufw delete 3



# Step 10: Inspect iptables Rules


sudo iptables -L > rules.txt

vi rules.txt

Exports firewall rules to file for review



# Step 11: View Firewall Config Files


sudo cat /etc/ufw/user.rules

sudo cat /etc/ufw/user6.rules

sudo cat /etc/default/ufw

ls /etc/ufw/applications.d/

sudo cat /etc/ufw/applications.d/openssh

sudo iptables -L -v -n

sudo ip6tables -L -v -n

Shows stored rules and active configurations



# Step 12: Manually Edit Rules


sudo vi /etc/ufw/user.rules

sudo ufw reload

sudo ufw status verbose

Applies manual changes



# Step 13: Reset or Disable Firewall


sudo ufw reset

sudo ufw disable

reset = clears rules
disable = turns firewall off



# Step 14: Backup and Restore Rules


# Backup rules

sudo ufw status numbered > ufw-rules.txt

sudo cp -r /etc/ufw/*.* etc-ufw

Transfer to another machine

scp -r ufw-rules.txt etc-ufw user@destination:/home/user/

# Restore rules

sudo cp /home/user/etc-ufw/*.* /etc/ufw/

cat ufw-rules.txt

sudo ufw allow 22

sudo ufw allow 80

sudo ufw status verbose



# Key Security Takeaways


 - Default deny incoming improves security
 - Restricting SSH reduces attack surface
 - Logging helps detect suspicious activity
 - Verifying rules ensures correct configuration
 - Backups allow easy recovery



# Files Included


# README.md → step-by-step guide
# rules.txt → firewall rule output




# Skills Demonstrated


 Linux system administration
 Firewall configuration (UFW)
 Access control and SSH hardening
 Log analysis
 Security-focused system hardening
