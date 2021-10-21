# Unix-Shell_Assignment

### Question 1
How many processes are currently running on your system? Use ps and wc, the first line of output of ps is not a process!

​ps -r | expr $(wc -l) -1

### Question 2
Write a script that upon invocation shows the time and date, lists all logged-in users, and gives the system uptime. 
The script then saves this information to a logfile.

​

### Question 3
Which command would you use in order to create an empty file in the current directory, let's say empty.txt?

​$ touch empty.txt

### Question 4
You are in /home/icipe/  suppose this directory is empty. How do you create in only one command the whole path /home/icipe/Work/mini-project/RNA-Seq/?

​mkdir -p Work/mini-project/RNA-Seq/

### Question 5
Suppose your current working directory contains a file named seqs.txt. How do you rename this file into sequences.fasta? 
Does this have any effect on the content of the file, and if yes, what does it do?

​$ mv seqs.txt sequences.fasta

### Question 6
How can you create in a single command a file containing the contents "Hello, world!" and named universal_greeting.txt?

​$ echo "Hello, world" > universal_greeting.txt

### Question 7
What about creating the same file but with filename "universal greeting.txt" (the filename contains a space)?

​$ mv universal_greetings "universal greeting.txt"

### Question 8
How can you use the commandline (on whichever machine you are now, that is connected to the internet) to download directly the 
file you can see on https://github.com/Fnyasimi/my-first-repo/blob/main/directory1/test.fa ? Be careful, you need to get the raw text file itself, 
not the full HTML page presenting it.

​Go to the link, select RAW then download.
$ wget https://raw.githubusercontent.com/Fnyasimi/my-first-repo/main/directory1/test.fa

### Question 9
How can you count the number of lines in this text file (test.fa)? How do you count the number of sequences?

​grep ">" test.fa | wc -l

### Question 10
Extract only the identifier lines from this file, and write them into a file called "identifiers.txt".

​grep ">" test.fa > identifiers.txt

### Question 11
How can you process the file you got from question 8 to replace all its uppercase "A" letters into lowercase "a" letters, leaving the rest untouched?

​sed "s/A/a/g" test.fa > newTest.fa

### Question 12
In one command, ask for the display of all identifier lines from the same file test.fa without wrapping the lines, i.e. by having all lines displayed 
on your screen effectively start with the character '>'.

​setterm -linewrap off 
cat identifiers.txt

### Question 13
Can you write a very short script (possibly one single commandline) to extract from the same file the species names?

​ # !bin/bash
* # Pick lines without predicted: pattern
* grep -v PREDICTED: identifiers.txt > notpredicted.txt

* # Lines with predicted
* grep PREDICTED: identifiers.txt > predicted.txt

* # Generic and species names from subfile 1
* cut -d ' ' -f 2,3 notpredicted.txt > joy.txt

* # Generic and species names from subfile 2
* cut -d ' ' -f 3,4 predicted.txt > joy.txt

* # Species names alone
* cut -d ' ' -f 2 joy.txt > nellyspecies.txt

### Question 14
Once this is done, how do you count the species names with their order of multiplicity 
(i.e. how many sequences belong to Mus musculus, how many to Homo sapiens, etc)?

​sort nelly.txt | uniq -c > species-multiplicity.txt

### Question 15
Write a loop in Bash producing all the integers from 1 to 30, one per line?

​for integers in species-multiplicity.txt
 do seq 1 30
 done
 
### Question 16
Create at once 20 files called "trial1" to "trial20" and *then* rename them all by appending the suffix ".data". 
Of course, don't issue 20 commands, but just one.

​touch trial {1..20} | find -type f -exec bash -c 'mv $0 $0.data' {}\;

### Question 17
Try this with the command "expr 1 / 0", whose purpose is to calculate the integer result of 1 divided by 0. What happens? Why?

​expr : division by zero

### Question 18
How can you separately redirect the standard output and the standard error streams into two separate files?

​command 2> error.txt 1> output.txt

### Question 19
Write a Bash script asking "What's your name?", then waiting for you (the user) to enter you name and press Enter, 
following what the program displays some text according to the following pattern:
"Good morning/day/evening, your_name!
It's now current_time on this lovely day of current_day." and it exits.

For instance, the message written by your program would be:
```
Good day Emmanuel! It's not 12:57EAT on this lovely day of July 20. 1:00
or 'Good morning" in the morning hours, or "Good evening" in the evening hours, depending on the current time.
Of course there will be at least an if or a case construct in your script.
```

​# !bin/bash
* echo "What is your name?"
* read name

* # Assign date, time and day
* date=$(date +%H)
* time=$(date +%T)
* day=$(date +%D)

* # Prompt text
* if [ $date -lt "12" ]
* then
* echo "Good morning $name"
* echo "It is now $time on this lovely day of $day"
* elif [[ $date -gt "12" && $date -lt "16" ]]
* then
* echo ""Good afternoon $name"
* echo "It is now $time on this lovely day of $day"
* else
* echo ""Good evening $name"
* echo "It is now $time on this lovely day of $day"
* fi

### Question 20
Suppose your current working directory is /home/icipe/Linux/Exercises/. What is the command that will enable to move to /home/icipe/Fun_stuff/?
* 
