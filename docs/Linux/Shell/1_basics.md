# Basics

## Variables and positional parameters
Declaring and assigning a value to a variable is done without any symbols **nor spaces**.
```sh
myName="John"
mySurname="Smith"
echo "Hello, $myName $mySurname! How are you?"

Hello, John Smith! How are you?
```

Some variables are assigned by the system, which can be useful when scripting. User-specific variables are called Environment Variables (`$PATH`, `$HOME`, ...etc) and are dependant on the user executing the script.

To catch the parameters (everything written after the command name), the programmer can use positional parameters. Let's use the following script:
```sh
#!/usr/bin/bash

echo "Arguments received: $#"

echo "Argument 0: $0"
echo "Argument 1: $1"
echo "Argument 2: $2"

echo "All arguments using \$@: $@"
echo "All arguments using \$*: $*"
```

The output would look like this:
```sh
./arguments.sh One Two Three Four Five

Arguments received: 5
Argument 0: ./arguments.sh
Argument 1: One
Argument 2: Two
All arguments using $@: One Two Three Four Five
All arguments using $*: One Two Three Four Five
```

## Conditionals
### if elif else
Below is a basic contitional structure. Note that **the spaces near the squared brackets are mandatory!**
```sh
if [ $myVar -gt $anotherVar ]
then
    echo "Do something"
elif [ $myVar -gt $anotherVar ]
then
    echo "Do something else"
else
    echo "Do something else"
fi
```
### Logical operators
#### AND &&
The logical operator AND (&&) is used when we want the condition to be true only if all the propositions are true. Taking the example below, the comment "Nice car!" will **only** be displayed if $MAX_SPEED is greater than 300 and $COLOR is "Orange".
```sh
if [ $MAX_SPEED -gt "300" ] && [ $COLOR == "Orange" ]
then
	echo "Nice car!"
fi
```

#### OR ||
The logical operator OR (||) is used when we want the condition to be true if one or more of the propositions are true.
```sh
if [ $TEMPERATURE -gt 25 ] || [ $SWITCH == "ON" ]
then
	echo "Time to turn on the fan!"
fi
```

## Loops
### While
```sh
while [ $myVar -gt $anotherVar ]
do
    echo "Do something until the condition is false"
done
```

### Until
```sh
until [ $myVar -gt $anotherVar ]
do
    echo "Do something until the condition is true"
done
```

### For
```sh
i=1
for line in $(cat text.txt)
do
    echo "Line $i: $line"
    i=$((i+1))
done
```

### Break and Continue
Like other programming languages, `break` and `continue` are keywords used to either "break out" of the loop or "continue to the next iteration". For example:
```sh
for number in {0..100}
do
	if [ $number -gt 10 ]
	then
		break
	else
		if [ $(($number%2)) == 0 ]
		then
			continue
		fi
		echo $number
	fi
done

```
The above script will have the following output:
```sh
1
3
5
7
9
```

## Comparison operators
### Comparing numbers

### Comparing strings


## Functions

```sh
add_two_numbers() {
	RESULT=(($1 + $2))
	return $RESULT
}
add_two_numbers 12 13
```