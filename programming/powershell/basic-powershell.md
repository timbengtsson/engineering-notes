# Basic Powershell
 


## Looping  

### For
The for loop in powershell takes a turn with the `-le` (less than equal to) flag. <br>
I am more used to the `<=` 

Commonly used when we know how many times we need to loop.

```PowerShell
# Starting off with $i is 1. 
# as long as $i is less then equal to (-le) 5  
# continue adding one to $i 
for ($i = 1; $i -le 5; $i++) {
    Write-Host "For Loop: count is $i"
}
```

### Foreach
Iterate each item in a list.

```PowerShell
$colors = @("Red", "Green", "Kevin")

foreach ($color in $colors) {
    Write-Host "Foreach Loop: Item is $color"
}
```

### Foreach-Object (Pipeline)
Iterate each item in a list.

So.. this one looks creepy. Lets break it down:<br> 
`Get-Process` -> Gets all processes on the computer. Each process is an object.<br>
`| Select-Object -First 3` -> Takes the first three objects from the list and sends them to the next function in the pipe. <br>
`| ForEach-Object` -> Here the actual loop is happening. A foreach loop. Iterating over each object. <br>
`$_` -> The current object in the loop <br>
`.Name` -> Takes the Name prop from the current Process object.  

```PowerShell
Get-Process | Select-Object -First 3 | ForEach-Object {
    Write-Host "Process: $($_.Name)"
} 

# Also allowed -> No filtering. Takes ALL processes.
Get-Process |  ForEach-Object {
    Write-Host "Process: $($_.Name)"
}  
```

#### Notice

PowerShell streams the objects.<br> 
Memory effective. 
 

### While loop
Iterate while a value is true.<br>
Usually used when we dont know the end of something.

```PowerShell
$count = 1

while ($count -le 3) {
    Write-Host "Foreach Loop: Count is $count"
    $count++
}

$running = $true

while ($running ) {
    if("Something has happend that is a signal to close the loop"){
        $runnign = $false
    }
}   
```

### Do While loop
Do thing first, then check if we should do it again.<br>
  
```PowerShell
$retry = 1

do {
    Write-Host "Do loop: Attempt $retry" 
}
while ($retry -le 3)  
```
 
## Mini Challenge

- Create an array of 5 animals.
- Use a foreach loop to print a message like "I love!" for each one.
- Then, use a for loop to number them from 1 to 5.


```PowerShell
$animals = $("cat", "dog", "snake", "frog", "another cat")

foreach ($animal in $animals){
    Write-Host "I love $animal"
} 


# using -lt less than
for ($i = 0; $i -lt 5; $i++) {
    Write-Host "$i $($animals[$i])"
}
```



# Resources 

[Working with PowerShell Loops](https://www.youtube.com/watch?v=Q5iPZm_fHbQ)