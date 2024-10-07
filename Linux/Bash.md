# Bash
## Important bash information
### Terminal Shorcuts
```
alt-f  - go forward word
alt-b  - go backwards word

ctrl-f - go forward char
ctrl-b - go backwards char

alt-t  - swap words
ctrl-t - swap char

ctrl-w - delete one word backwards
alt-d  - delete one word forwards
ctrl-u - delete entire line to left

ctrl-a - go to the start of the line
ctrl-e - go to the end of the line

ctrl-r - reverse search
```

### Misc
```
type -a echo
alias echo='echo foo'
function echo() { command echo bar "$@"; }

command - Execute shell builtin
sudo - Runs external command and not shell builtin
echo -e - Special sequences are recognized
```

## Bash Scripting
### Accessing files in directory
```bash
for f in ./files/*; do
	echo "File $f"
done
```

### Listing arguments
```bash
for arg in "$@"; do
	echo "<$arg>"
done
```

### Reading data line by line
```bash
while IFS=: read -r name id desc; do
	echo "$id: $name is $desc"
done < data.txt
```

Example data.txt
```
Name1:001:desc1
Name2:002:d e s c 2 
```

### Regex
```bash
regex='^()()$'      # Demo - Match groups
for f in ./files/*; do
	if [[ $f =~ $regex ]]; then
		var1=${BASH_REMATCH[1]}
		var2=${BASH_REMATCH[2]}
		echo "$var1: $var2"
	fi
done
```


### Printing time
```bash
date +'The time is %H:%M:%S'
printf '%T\n'
printf '%()T\n'
printf '%(%H:%M:%S)T\n' -1  # Strftime

date +%s
echo $EPOCHSECONDS
echo $EPOCHREALTIME
```
