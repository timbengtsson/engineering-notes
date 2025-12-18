# Threat Modeling 
 
As one of my instructors often says:  
> “We cannot protect what we do not understand.”

Threat Modeling aims to answer question like:
- What are we protecting?
- From whom?
- Where will the system fail first?
- What matters most if (when) something goes wrong?

Threat Modeling is the process of systematically identifying what needs to be protected, where a system is vulnerable, and how an attacker is most likely to succeed.
Starting with a clear understanding of the system and its assets gives us a foundation on which we can harden the systems in practice.

---

## Purpose
The goal of threat modeling is to:
- Identify realistic threats early
- Prioritize security efforts where they matter most
- Reduce assumptions about how systems are used or attacked
- Improve communication between developers, operations, and security

Threat modeling is not about predicting every possible attack. 
It is about making informed decisions under uncertainty and prioritize the identified weak points of the system.

---

## Questions to Ponder 
- What are the critical assets? 
- Who are the likely attackers?
- What are the trust boundaries?
- Where does data enter and leave the system?
- What would have the highest impact if compromised?
- Which risks are acceptable, and which are not?