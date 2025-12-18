# Bash
 
## Purpose / What does it do?
Bash (Bourn again shell) is a shell and a scripting language that let you control operating system throgugh text commands. You can use bash to:
- Navigate the file system
- Run programs and tools
- Automate actions like backup, deploy, log analysis, batch jobs and things like that. 
- Kan chain commands togeather and filer data. 
- And much much more. 

It is commonly used in linux and maxOS. A lot in servers and so on. <br>
 In windows it can be used with WSL. 
 
## Contents
- [Bash Common Comands](./bash-commands.md) 
- [Basic Bash](./basic-bash.md) 
- [Bash Looping ](./bash-looping.md) 

## Tips and common errors

### Use quotations! 
Ponder this:
```bash
filePath="/home/User/My Files/test.txt"
rm $filePath
```
Bash try to delete two files.

```bash
rm /home/User/My  Files/test.txt
```

But with quotes `rm "$filePath"` bash treats it like one argument: `/home/User/My Files/test.txt`

## Related resources

 