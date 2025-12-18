# Bash Basics
 
## Strict and secure
use this:
`set -euo pipefail`

**It will:**
- Stop Scripts early
- Make errors visible
- Minimize the risk for scilent bugs
- It is a standard in serious bash-projects
 

### Exit on error -e
When setting this:
```bash
set -euo pipefail

# the -e flag = exit on error
set -e
cp file_that_does_not_exist /tmp
echo "This will never run"
```
Without `-e` the script would have kept going, hiding the error.

### Undefined variable -u
Makes the sctipt crash when using a variable that do not exist.

```bash 
set -u
echo "$notDefined"
# bash: notDefined: unbound variable
```

### Fail on pipeline error -o
Makes the entire pipe fail if one step fails
```bash 
set -o pipefail
false | grep something
echo $?   # exit code != 0
```

 

 
## Variables 
In bash a variable is just the variable name, equal sign and then the value. No spaces.<br>
Print it with echo and prepending dollar sign to the variable.
```bash
name="Garfield"
echo $name

# using it in a string like so:
echo "Your name is $name"
```

## Getting input from user 
Get input from user with _read_

```bash
read -p “What file should be analyzed:” file
echo “Checking $file”
```

## if
```bash
if [-f "$file"]; then
    echo "File exist"
else 
    echo "File does not exist"
fi
```

## Tools & tips
Check your shell scripts on [ShellCheck](https://www.shellcheck.net/)