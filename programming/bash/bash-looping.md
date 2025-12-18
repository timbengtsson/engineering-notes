# Looping in Bash
 
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

for current_number in {1..10}
do
    echo $current_numer
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
 

# Resources 

[Bash For Loops](https://www.youtube.com/watch?v=HvzI7c3eK5k)