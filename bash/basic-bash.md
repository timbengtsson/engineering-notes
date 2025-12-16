# Bash Basics
 

## Variables

In bash a variable is just the bvariable name, equal sign and then the value. No spaces.<br>
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

## Looping

Bash has got some looping going on.<br>

### For loops
 
Used when we have a known list. <br>
Like files, words or things like that. <br>
_(Similar to `foreach` in PHP or `for...of` in JavaScript)_<br>

```bash
# bash
for file in *.log; do
    echo "Processing $file"
done
``` 

```javascript
// JavasScript
for (const file of files) {
    console.log(`Processing ${file}`);
}
```  

```php
// PHP
foreach ($files as $file) {
    echo $file;
}

foreach ($files as $key => $value) {
    echo $file;
}
```


C-style for loop, if we need a counter. <br>
_(Similar to a for loop in PHP)_<br>
```bash
for ((i=0; i<5; i++)); do
    echo "$i"
done
```

```javascript
// JavaScript
for (let i = 0; i < 5; i++) {
    console.log(i);
}
```

```php
// PHP
for ($i=0; $i<5; $i++) {
    echo $i;
} 
```

### While loops 

Use when processing a streaming input or when a condition becomes false<br>
Like the last row of a file.
```Bash
while read -r line; do
    echo "$line"
done
```


## Functions

Params sent in to the function is position based. <br>
So the first one after calling the functtion is $1.<br> 
The second one $2 and so on.

```bash
check_user (){
    echo "Doing serious checking of user: $1"
}

check_user "Michael" 
```
 

## Tools & tips

Check your shell scripts on [ShellCheck](https://www.shellcheck.net/)