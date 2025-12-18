# Defense in Depth

## Summary
_Defense in Depth_ meaning using multiple layers of security. If one control fails there are more layers to keep out threat actors.<br> 

A common analogy is a castle:<br>
a moat, outer walls, inner walls, guards, and locked doors. Multiple layers.

## The main idea
No security control is perfect. 

Defense in Depth assumes that:

- Systems will be misconfigured
- Software will have vulnerabilities
- Users will make mistakes
- Attackers may bypass individual controls

By combining technical, administrative, and physical controls, attackers are slowed down, detected earlier, and limited in what they can access.

## Examples
 
### Network level 
- Firewall + IDS/IPS
- Segmentation
- VPN for remote access

### System Level 
- OS hardening
- Least privilege on users and accounts 
- Patch management -> Fix known vulnerabilities
- Logging and monotoring 

### Application level 
- Validate all input -> Avoide SQL injection, XSS And so on
- Authentication and authorization 
- Rate limiting -> Slowing down brute force attacks 
- Safe Error messages

### User level
- MFA -> Multi factor authentication  
- Security Awareness training 
- Strong password policies


## Concequenses when violating
If you would rely on one layer of security a failur become critical:

- One vulnerability can lead to full compromise
- Attackers move laterally without resistance
- No detection until damage is done
- Increased impact of phishing or credential leaks

Example:
If authentication is the only protection and credentials are stolen, the attacker gains full access.<br>
But if MFA was in place it would stop an attacker that only had username + passowrd.


## Best Practices
- Allways have multiple security layers!
- Use both preventitive, detective and corrective controls to be able to stop and detect potential attacks. And return to normal usage quickly after incident.   
- Assume that the system has already been hacked. And design with that in mind.
- Apply least privilegie on each layer. No one should be able to do more than they need.
- Log and monitor all critical systems.
- Regularly test defenses and backups. 


## Related concept 
- [Zero Trust](./zero-trust.md)
- [Least privilege](./least-privilege.md)
- [Least functionality](./least-functionality.md)

 
## Sources 
[wikiipedia on defence in Depth](https://en.wikipedia.org/wiki/Defence_in_depth) 