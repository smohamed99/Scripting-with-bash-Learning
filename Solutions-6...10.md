# Solutions (Levels 6–10)

---

## Level 6: Argument Parsing
```bash
## Level 6
#!/bin/bash

if [ -z "$1" ]; then
    echo "No file provided"
    exit 1
fi

if [ ! -f "$1" ]; then
    echo "File not found!"
    exit 1
fi

LINE_COUNT=$(wc -l < "$1")
echo "The file '$1' has $LINE_COUNT lines."

Key notes:
- $1: Represents the first argument passed when running the script.
- if [ -z "$1" ]: Checks if no argument was given (empty).
- if [ ! -f "$1" ]: Checks if the given file doesn’t exist.
- wc -l < "$1": Counts the number of lines in the file.
- LINE_COUNT=$(...): Stores the result in a variable.
- Example: ./6arg.sh test.txt → counts lines in test.txt.

Key Takeaways:
- You can pass arguments into scripts from the command line.
- $1, $2, etc. represent arguments in order.
 -Always check if a file exists before working on it.
 -Line-counting is a practical use of redirection and variables.


## Level 7
#!/bin/bash

DIRECTORY="Arena"

if [ ! -d "$DIRECTORY" ]; then
    echo "Directory does not exist."
    exit 1
fi

find "$DIRECTORY" -type f -name "*.txt" -exec ls -lh {} + | sort -k 5,5 -h | awk '{ print $5, $9 }'

Key notes:
- if [ ! -d "$DIRECTORY" ]: Checks if the directory doesn’t exist.
- find ... -name "*.txt": Finds all .txt files in Arena.
- ls -lh: Lists file details in human-readable format.
- sort -k 5,5 -h: Sorts by the 5th column (file size).
- awk '{ print $5, $9 }': Prints just the file size and name.

Key Takeaways:
- Learn how to search for files with find.
- Combine commands with pipes (|) to filter results.
- [Sorting and extracting specific columns helps when working with lots of files.

## Level 8
#!/bin/bash

DIRECTORY="Arena"
SEARCH_TERM="Error"

if [ ! -d "$DIRECTORY" ]; then
    echo "Directory does not exist."
    exit 1
fi

grep -l "$SEARCH_TERM" "$DIRECTORY"/*.log

Key notes:
- grep -l: Searches files and only prints filenames containing the search term.
- "$SEARCH_TERM": The word you’re searching for.
- "$DIRECTORY"/*.log: Limits search to .log files inside Arena.

Key Takeaways:
- grep is a powerful tool for searching text in files.
- -l option lists filenames instead of showing the actual matches.
- This is useful for quickly finding logs or errors across multiple files.

## Level 9
#!/bin/bash

DIRECTORY="Arena"
LOG_FILE="change_log.txt"

if [ ! -d "$DIRECTORY" ]; then
    echo "Directory does not exist."
    exit 1
fi

fswatch -r "$DIRECTORY" | while read event; do
    if [ -e "$event" ]; then
        echo "$(date +'%Y-%m-%d %H:%M:%S') File modified/created: $event" >> "$LOG_FILE"
    else
        echo "$(date +'%Y-%m-%d %H:%M:%S') File deleted: $event" >> "$LOG_FILE"
    fi
done

Key notes:
- fswatch -r: Monitors the Arena folder and subfolders for changes.
- while read event: Loops through each change detected.
- if [ -e "$event" ]: Checks if the file still exists.
- Logs the event with a timestamp and whether it was created, modified, or deleted.

Key Takeaways:
- You can watch directories for changes in real time.
- Useful for logging file changes or detecting suspicious activity.
- (Combines monitoring with conditionals to capture more detail.

## Level 10
#!/bin/bash

mkdir Arena_Boss

for i in {1..5}
do
    FILE="Arena_Boss/file$i.txt"
    LINES=$((RANDOM % 11 + 10))
    for j in $(seq 1 $LINES)
    do
        echo "This is line $j" >> "$FILE"
    done
done

echo "Files sorted by size:"
find Arena_Boss -type f -exec ls -lh {} + | sort -k 5,5 -h

mkdir -p Victory_Archive
for FILE in Arena_Boss/*.txt
do
    if grep -q "Victory" "$FILE"; then
        mv "$FILE" Victory_Archive/
        echo "$FILE contains 'Victory' and has been moved to Victory_Archive."
    fi
done

Key notes:
- Creates 5 text files with a random number of lines.
- RANDOM % 11 + 10: Generates a number between 10–20 for line count.
- Each file gets filled with lines of text.
- Files are then listed and sorted by size.
- If a file contains the word “Victory”, it gets moved to Victory_Archive.

Key Takeaways:
- You can generate random values in Bash ($RANDOM).
- Nested loops let you create and fill files dynamically.
- Searching with grep can control how files are handled.
- A boss battle combines loops, conditionals, file creation, sorting, and searching all in one script.


























