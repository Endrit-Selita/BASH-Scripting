# Change PATH Permanently with ZSH

The PATH environment variable is a critical system variable that specifies the directories where the shell should look for executable files.

We may need to add our own directories to the PATH, particularly when installing a new software or when we want our scripts/binaries to be available system wide.

## To add a directory to a PATH
- Remember changes made in the terminals are temporary and lost when the shell session ends. To make it permanent we need to add it to the ZSHRC file.

To change the PATH permanently:
- `echo export PATH=$path:~/directory_name >> ~/.zshrc` (# the tilde sign means home directory then / your directory name)
- So no any binaries or executables that the system finds in the directory we put into the PATH, it will take as a binary that we can run system wide.

This makes this script accessible in the zsh PATH, so if we reload zshrc by command: `source ~/.zshrc`

Then you execute your command without the ./ as that runs it from the current directory, it will now run from and is accessible from any directory as well, in this case it will work even though it is a bash script

Example; we have a script hello_world.sh from my_Script directory. So if we now enter hello_world.sh into the command line it will respond with Hello World!

---

# Reading Environment Variables

Environment variables allow us to store and retrieve important information within our bash script. They are like containers which hold valuable information for our scripts.They provide a way to store settings and configurations that our scripts can access when needed.

Home directory is $HOME 
- e.g echo `Home Directory: $HOME`

Current user is $USER 
- e.g echo `Current User: $USER`
  
Current operating system type is $OSTYPE 
- e.g echo `OS Type: $OSTYPE`

You can make a local variables

example:

```
my_home=”$HOME”
echo “Home Directory: $my_home”     # this will give you the same result as we assigned $HOME to the local variable
```

---

# Standard Environment Variables

Standard environment variables give us valuable insights into various aspects of the system, user and runtime environment. They provide information that can help us create more robust and adaptable bash scripts.

- Username (log in name of current user) is `$LOGNAME`
- The shell is `$SHELL`
- Current directory is `$PWD`
- Current PATH is `$PATH`
- Default language is `$LANG`

---

# Reading Files

To read a any file line by line (to process their content) you can create this script

```
1 #!/bin/bash
2 process_file() {
3 	local file_path=”$1”
4	cat “$file_path” | while IFS= read -r line
5 	do	
6 	echo “Processing line: $line”
7 done
8 }
9 process_file “./textfile_name.txt”
```

Then when we want ro read a txt file we can command: process_file “./xyz.txt”

---

# Writing to Files

Writing to files is a fundamental task in Bash scripting, useful for logging, automation, and data processing. It also allows us to create, modify and store information in various formats. This guide covers creating, overwriting, and appending files, as well as making your script executable and running it from the terminal.


| Operator | Action     | Effect on File        |
|----------|------------|-----------------------|
| `>`      | Overwrite  | Replaces all content  |
| `>>`     | Append     | Adds to existing data |


vim writing_to_files.sh

To overwrite:
```
#!/bin/bash
write_to_file() {
local file_path="$1"
local data="$2"
echo "$data" > "$file_path" # Overwrites file
}
write_to_file "output.txt" "Hello, World!"
```

To Append:

```
#!/bin/bash
write_to_file() {
local file_path="$1"
local data="$2"
echo "$data" >> "$file_path" # Appends to file
}
write_to_file "output.txt" "Another line"

Chmod +x writing_to_files.sh
./writing_to_files.sh

cat output.txt   # check the contents of output.txt and you can see "another line" was appended
Hello, World!
Another line
```

---

# File Checksums

File checksums are cryptographic hashes that provide a unique fingerprint for a file which allows us to verify the authenticity of the file. All files have different checksums.

You can generate a file checksum using the md5sum command - if you do not have md5sum installed you can by command `brew install md5sha1sum`

Once installed you run the script

```
vim checksum.sh
1 #!/bin/bash
2 calculate_md5sum() {
3 	local file_path=”$1”
4 	md5sum “$file_path”
5 }
6 calculate_md5sum “file.txt”
:wq!
Chmod +x checksum.sh
./checksum.sh
checksum of file.txt
```

This can also be done with sha256sum - just do exactly the same but replace md5sum with sha256sum.

Checksums are especially useful when we need to compare the integrity of a file over time or across different systems so we can use it to compare 2 different checksums and see if their values match

We can do this by setting up a script

```
1 #!/bin/bash
2 compare_checksums() {
3 	local checksum1=”$1”
4 	local checksum2=”$2”
5 if [[ “$checksum1” == “checksum2” ]]
6 	echo “Checksums match. File is intact.”
7 else
8	echo “Checksums do not match. File integrity compromised”
9 fi
10 }
11 compare_checksums “abc” “xyz”
```
