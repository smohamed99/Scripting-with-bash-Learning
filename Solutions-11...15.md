    # Solutions (Levels 11–15)

---

## Level 11: Automated Disk Space Report
```bash
## Level 11
#!/bin/bash

DIRECTORY="Arena"
THRESHOLD=1

USAGE=$(du -sm "$DIRECTORY" | awk '{print $1}')

if [ "$USAGE" -gt "$THRESHOLD" ]; then
    echo "Warning: Disk usage for $DIRECTORY is at $USAGE MB!"
else
    echo "Disk usage for $DIRECTORY is at $USAGE MB. All is well."
fi

Key notes:
- du -sm "$DIRECTORY": Checks the folder size in megabytes.
- awk '{print $1}': Pulls out just the size value.
- if [ "$USAGE" -gt "$THRESHOLD" ]: Compares the size to a set threshold.
- Prints a warning if the folder is too big, otherwise says everything’s fine.

Key Takeaways:
- du is used to check folder size.
- You can use variables like USAGE to store command outputs.
- Scripts like this can be automated to monitor space before it becomes a problem

## Level 12
#!/bin/bash

CONFIG_FILE="settings.conf"

if [ ! -f "$CONFIG_FILE" ]; then
    echo "Configuration file does not exist."
    exit 1
fi

while IFS='=' read -r key value; do
    echo "Key: $key, Value: $value"
done < "$CONFIG_FILE"

Key notes:
- IFS='=': Splits each line at the = sign.
- read -r key value: Reads the line into two variables.
- Prints the key/value pair for each line in the config file.

Key Takeaways:
- Learn how to read files line by line in Bash.
- IFS lets you split input into multiple parts.
- Config parsing is a real-world task, which useful for settings files.

## Level 13
#!/bin/bash

SOURCE_DIR="Arena"
BACKUP_DIR="Backups"

mkdir -p "$BACKUP_DIR"

TIMESTAMP=$(date +"%Y-%m-%d_%H-%M-%S")
BACKUP_NAME="backup_$TIMESTAMP.tar.gz"
tar -czf "$BACKUP_DIR/$BACKUP_NAME" "$SOURCE_DIR"
echo "Created backup: $BACKUP_NAME"

cd "$BACKUP_DIR" || exit
ls -t | sed -e '1,5d' | while IFS= read -r file; do
    rm -f "$file"
done

Key notes:
- tar -czf: Creates a compressed archive of Arena.
- Timestamp makes each backup unique.
- Keeps only the 5 most recent backups, deleting older ones.

Key Takeaways:
- tar is used for creating backups.
- Adding timestamps makes backups easy to track.
- Backup rotation is essential to avoid filling storage.

## Level 14
#!/bin/bash

echo "Choose an option:"
echo "1. Check disk space"
echo "2. Show system uptime"
echo "3. List users"

read -rp "Enter your choice [1-3]: " choice

case $choice in
    1) df -h ;;
    2) uptime ;;
    3) cut -d: -f1 /etc/passwd ;;
    *) echo "Invalid option" ;;
esac

Key notes:
	•	Shows a menu and waits for user input.
	•	case ... esac: Matches the user’s choice and runs the right command.
	•	Runs different system commands based on the option selected.

Key Takeaways:
- Menus make scripts interactive and user friendly.
- case statements are a clean way to handle multiple choices.
- You can tie commands together into a simple CLI tool.

## Level 15
#!/bin/bash

echo "Choose an option:"
echo "1. Check disk space"
echo "2. Show system uptime"
echo "3. Backup Arena directory"
echo "4. Parse configuration file"

read -rp "Enter your choice [1-4]: " choice

case $choice in
    1)
        df -h
        ;;
    2)
        uptime
        ;;
    3)
        SOURCE_DIR="Arena"
        BACKUP_DIR="Backups"

        mkdir -p "$BACKUP_DIR"

        TIMESTAMP=$(date +"%Y-%m-%d_%H-%M-%S")
        BACKUP_NAME="backup_$TIMESTAMP.tar.gz"
        tar -czf "$BACKUP_DIR/$BACKUP_NAME" "$SOURCE_DIR"
        echo "Created backup: $BACKUP_NAME"

        cd "$BACKUP_DIR" || exit
        ls -t | sed -e '1,5d' | while IFS= read -r file; do
            rm -f "$file"
        done
        ;;
    4)
        CONFIG_FILE="settings.conf"
        if [ ! -f "$CONFIG_FILE" ]; then
            echo "Configuration file does not exist."
            exit 1
        fi
        while IFS='=' read -r key value; do
            echo "Key: $key, Value: $value"
        done < "$CONFIG_FILE"
        ;;
    *)
        echo "Invalid option"
        ;;
esac

Key notes:
- Combines menu options with real tasks from earlier levels.
- Option 3 backs up the Arena folder.
- Option 4 parses a config file.
- Brings everything together in one script with multiple choices.

Key Takeaways:
- Boss battles bring all the skills together into one bigger script.
- Menus, conditionals, loops, backups, and parsing all work in harmony.
- This is closer to a real world script you’d actually use.

