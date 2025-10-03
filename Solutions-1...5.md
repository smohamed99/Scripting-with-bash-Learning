# Solutions (Levels 1–5)

---

CODE:
## Level 1
```bash
#!/bin/bash
mkdir Arena
cd Arena
touch warrior.txt mage.txt archer.txt
ls

Key notes:
- mkdir Arena: Creates a directory named Arena.
- cd Arena: Changes the current directory to Arena.
- touch warrior.txt mage.txt archer.txt: Creates three empty text files.
- ls: Lists the files in the Arena directory.

 key Takeaways:
- Learn how to create and move into directories.
- Understand how to make empty files with touch.
- Use ls to confirm what exists in a folder.

CODE:
## Level 2
#!/bin/bash
for i in {1..10}
do
    echo $i
done

Key notes:
- for i in {1..10}: This sets up a loop that goes through the numbers 1 to 10.
- do: Tells the script “start running these commands for each number.”
- echo $i: Prints the current number in the loop.
- done: Tells the script “that’s the end of the loop.” Everything between do and done repeats for each number.
    
Key Takeaways:
- You can use a for loop to repeat commands automatically.
- The variable $i changes each time, holding the current number.
- The do ... done block is where you put the commands that should run in each loop.
- .Loops save time and keep your scripts short, instead of writing the same command again and again.

## Level 3
#!/bin/bash
if [ -f "Arena/hero.txt" ]; then
    echo "Hero found!"
else
    echo "Hero missing!"
fi

Key notes:
- if [ -f "Arena/hero.txt" ]: Checks whether the file hero.txt exists.
- then: If it does exist, the script will run the next command.
- echo "Hero found!": Prints a success message.
- else: Runs a different command if the file isn’t there.
- echo "Hero missing!": Prints a warning message.
- fi: Marks the end of the if-statement.

Key Takeaways:
- if statements let your script make decisions.
- -f is a test flag to check for a file.
- The structure is: if ... then ... else ... fi.
- Conditionals make scripts smarter because they react to different situations.


## Level 4
#!/bin/bash
mkdir -p Backup
cp Arena/*.txt Backup/
 
Key notes:
- mkdir -p Backup: Creates a folder called Backup, and doesn’t complain if it already exists.
- cp Arena/*.txt Backup/: Copies every .txt file from Arena into Backup.

Key Takeaways:
- Use mkdir -p when you want to make sure a folder exists.
- The * wildcard helps work with multiple files at once.
- Copying files is a key part of managing and backing up data.



## Level 5
#!/bin/bash
mkdir Battlefield
touch Battlefield/knight.txt Battlefield/sorcerer.txt Battlefield/rogue.txt

if [ -f "Battlefield/knight.txt" ]; then
    mkdir -p Archive
    mv Battlefield/knight.txt Archive/
    echo "knight.txt has been moved to Archive."
else
    echo "knight.txt not found."
fi

echo "Contents of Battlefield:"
ls Battlefield

echo "Contents of Archive:"
ls Archive

Key notes:
- Makes a new folder called Battlefield with three text files inside.
- Uses an if statement to check for knight.txt.
- If the file exists, it moves it into a new Archive folder.
- Finally, it lists what’s left in Battlefield and what’s inside Archive.

Key Takeaways:
- Brings together everything from Levels 1–4 into one script.
- Shows how to create, move, and check files in one flow.
- Reinforces using conditionals to decide what happens next.
- Boss battles are about putting your skills together instead of using them one by one.