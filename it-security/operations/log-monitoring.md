# Log Monitoring

## Summary
_Log Monitoring_ is a core practice in IT-security. <br>
The idea is to continuously collect, review and analyze logs that has been generated.<br>
In logs we can find events such as user login attempts, configuration changes, errors and system activity.<br>  

Monitoring logs can give us early warnings of security threats and help us investigate incidents.  
They can point us to suspicious patterns such as:
### Repeated faild login attempts
-> Could be brute force attack <br>
(Do we use fail2ban and account lockout?)

Standards and Regulations:  
- ISO 27002:2022 – [Control 8.15 (Logging)](https://www.isms.online/iso-27002/control-8-15-logging/) & [hightable.io/iso-27001-annex-a-8-15-logging/](https://hightable.io/iso-27001-annex-a-8-15-logging/)<br>
Requires logging of authentication attempts and review of logs.
- NIS2 – Article 21 (Risk management measures)<br>
Requires detection and prevention of unauthorized access.
- Benchmarks (CIS Controls v8 – Control 8)<br>
Emphasizes logging and alerting for authentication failures.

### Accesss from unusual location
-> Credentials could have been leaked or stolen.<br> 
(Do we enforce Multi Factor Authentication and check strange geolocation trafic?)<br>
 
Standards and Regulations:  
- ISO 27002 – [Control 8.16 (Monitoring activities)](https://www.isms.online/iso-27002/control-8-16-monitoring-activities/)<br> 
Requires detection of anomalous behavior.
- NIS2 – Article 23 (Incident handling)<br> 
Requires timely detection of security incidents.
- GDPR – Article 32 (Security of processing)<br> 
Requires appropriate technical measures to prevent unauthorized access.

### Privilege escalation attempts
→ An attacker or compromised account is trying to gain higher access rights<br>
(Are [Least Privilege](../principles/least-privilege.md) principles applied and are admin actions logged and reviewed?)

Standards and Regulations: 
- ISO 27002 – [Control 8.2 (Privileged access rights)](https://www.isms.online/iso-27002/control-8-2-privileged-access-rights/) <br>
Requires strict control and monitoring of privileged accounts.
- Benchmarks (CIS Control 5 – Account Management)
Requires monitoring changes to account privileges.

## Why log monitoring is mandatory, not optional

- Detection: It helps us to identify attacks and misuse in an early stage
- Response: It helps us handle incidents. Se when and from were
- Compliance: Required by ISO standards, NIS2, and GDPR
- Accountability: Ensures traceability of user and admin actions

So lets do it! 

## Logs of Interest

So what logs should we look into and build scripts that scan through? 

We should focus on logs that anser these questions:
1. Who did what? 
2. From where?
3. Did it succees?
4. What changed?
5. What broke or crached? 

### Linux systems

#### Who did what?

Purpose: Identify users, accounts, processes, and actions.
 
- /var/log/auth.log -> Debian/Ubuntu
- /var/log/secure -> RHEL/CentOS 

Here we find the answer to:<br>
-> Who tried to login?<br>
-> How did they try to log in?<br>
-> Did they succeed or fail?<br>
-> Did they use `sudo` or other priv?<br>

#### Examples

**logins**
```bash 
# faild authentication
# Password-based login
# wrong password for a user that does NOT exist on the system
# from (source) ip 185.123.45.67 and client (source) port 54321 
# using service SSH 
# Protocol: SSH version 2 
Failed password for invalid user admin from 185.123.45.67 port 54321 ssh2

 
# faild authentication
# Password-based login
# wrong password for a user thjat EXIST on the system Jacqueline
# from (source) ip 203.0.113.10 and client (source) port 60214 
# using service SSH
# Protocol: SSH version 2 
Failed password for Jacqueline from 203.0.113.10 port 60214 ssh2

# Accepted login
# using key
# for a user that EXIST on the system Lena
# from (source) ip 192.0.2.50 and client (source) port 49822 
# using service SSH 
# Protocol: SSH version 2  
Accepted publickey for Lena from 192.0.2.50 port 49822 ssh2
```  

**sudo activity**
```bash 
# User Lena 
# using terminal pts/0
# From /home/lena
# As root
# Ran the command apt update 
Lena : TTY=pts/0 ; PWD=/home/lena ; USER=root ; COMMAND=/usr/bin/apt update
```  

 
### Windows systems
In windows we will mostly be reading Event Logs via Event Viewer or scripts using Get-WinEvent.

#### Who did what?

**Security log (logons, account use, privileges)** <br>
Key events to monitor:<br>
- 4624 Successful logon
- 4625 Failed logon
- 4634 / 4647 Logoff
- 4672 Special privileges assigned to new logon (admin-like)
- 4688 Process creation (if enabled)
- 4720/4722/4725/4726 User created/enabled/disabled/deleted
- 4728/4732/4756 Added to privileged groups
- 4739 Domain policy changes (domain environments)

System log (services, drivers, reboots)<br>
- Alert on: unexpected service installs, frequent restarts, driver failures, time sync issues.

Application log<br>
- Alert on: app crashes, authentication errors, unusual exceptions, repeated failures.

PowerShell logging<br>
- Alert on: encoded commands, downloads, Invoke-Expression, suspicious modules.

Windows Defender / AV logs<br>

RDP / Remote access<br>
- Alert on: RDP brute force patterns, logons outside expected hours.
 

# What to build scripts for  
In the [IT-security course](../../education/it-security/it-security_developer.md) we are building scripts.<br>
So what could be the lowest hanging fruite we could pick to get the most out of our log scans?
 
- Brute force: N failed logins within X minutes (per user + per IP)
- Suspicious success: login success after many failures
- Privilege changes: user added to admin group / sudoers change
- Persistence: new cron task / new Windows scheduled task / new service installed
- Lateral movement clues: remote logons/RDP spikes, new SMB-related activity (environment dependent)
- Service crash loops: repeated restart events + error logs