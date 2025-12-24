# John the Ripper

> **Legal note**<br>
> This tool must only be used on systems you own or have explicit permission to test.

**Status**: In progress

## Purpose / What does it do? 
John The Ripper is a password cracking tool used to test the strength of passwords by attempting to crack hashed passwords.<br>
It is used when we need to turn stored password [hashes](./hashes.md) into readable passwords.


### In a Nutshell
- Cracks hashed passwords offline
- Supports many hash types
- Dictionary attacks, brute force and rule-based attacks
- Can be combined with wordlists like rockyou.txt


## When to use
- You have obtained password hashes (e.g. /etc/shadow, NTLM, dumped databases)
- You want to verify password policies
- After data breaches to assess damage
- In controlled lab environments



## Commands  
```bash
    # john: Starts John the Ripper
    # options ..is the options
    # And then a path to a file containing the hashes we want to crack
    
    john --wordlist=list_of_password.txt crack_it.txt
    john --format=raw-md5 crack_it.txt
```

# Identify type of hash 
[Identify hash types](https://hashes.com/en/tools/hash_identifier)
[hash-identifier](https://gitlab.com/kalilinux/packages/hash-identifier/-/tree/kali/master)


## Resources 
- [Openwall - John-the-ripper](https://www.openwall.com/john/)
- [Jumbo John](https://github.com/openwall/john/blob/bleeding-jumbo/doc/INSTALL) 
- [Wikipedia on John-the-ripper](https://en.wikipedia.org/wiki/John_the_Ripper)