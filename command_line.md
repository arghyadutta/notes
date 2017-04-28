# Compilation of useful bash commands for reference. Nothing original. :punch:
###### command line navigation ######
 * To jump to the beginning of the line: `ctrl + a`.
 * To get to the end of the line:  `ctrl + e`.
 * To move back and forth between individual characters (just like the left and right arrow keys, but now you don't have to move your hand): `ctrl + b` and `ctrl + f`
 * To move between words in the command line, use `esc + b` and `esc + f`. 

* pushd and popd 
Let's say you accidentally change directories and you don't want to type out the whole filepath to get back to where you were. You can just type:
```bash
cd - / pushd / popd
```
That'll take you back to the last directory you were in. 

* touch 
Creates an empty file called `file.txt` in the current folder. 
```bash
touch file.txt
```

* cat
```bash
cat file.txt
cat file1.txt file2.txt > newfile.txt
cat file1.txt >> newfile.txt
```
Line 1 prints the contents of `file.txt` onto the command line. Line 2 merges content of two different files into a single file one after the other. Line 3 would append (note the `>>` symbol) contents of `file1.txt` to the end of `newfile.txt`. A single `>` symbol would overwrite contents of `newfile.txt` with that of `file1.txt`.

* more 
```bash
more file.txt
nano file.txt
```
This would do exactly what the `cat` command does - displays the contents of the file, but in a diffrent way. When `more` is used, it displays the contents of the file one page at a time for easier viewing, within the command line. Pressing `Enter` will let you scroll down the document. Keyboard interrupt will close the file.`nano` is yet another unix utility to display a file, and could be an alternative for users who think `vim` is advanced. 

* find 
```bash
find $\sim$ -name *.jpg
```
Let's break this down. First, you have the command name, then you have the directory to search (`$\sim$` in this case). Following that is a flag that specifies a certain way for the command to behave (typically anything following a dash is a flag; there are a few exceptions). In this case, the flag tells find to search specifically for things with the name that follows, which in this case is `*.jpg`. The `*` is a wildcard, telling find to match any file as long as it ends with `.jpg`.

* grep
```bash
grep "blog" temp.txt
```
This command will return every line in `temp.txt` that contains the word blog. What's interesting about `grep` is that it gives you some options for what you search on, allowing you to insert wildcards to increase the range of what gets matched.

```bash
grep "bl.g" temp.txt
grep -i "cats" ./cats.txt
```
The `.` is a wildcard; it matches any character just once; for instance, output of this command might look something like:
`blog blag bl\&g`. There are way more wildcards than just `.` though. To whet your appetite, take a look at this [site](http://www.panix.com/~elflord/unix/grep.html).

`grep` provides a few more options too. To search a file in current directory for a string that's case insensitive, add the `-i` flag. The following command could match a line containing cats, cATs, CATS, etc.

* cut
```bash
cut -d' ' -f1-6 /var/logs/*
usermame date group hello 23
cut -c1 file.txt
``` 
`cut` command is a very useful tool if you want to extract entries from a huge, formatted file. In Line 1 `-d` sets the delimiter - a single character that could separate entries into fields. For instance in a space separated document with data represented in a 20x10 matrix, the logical delimiter one would chose is `space`. In log files `:` could also be a sensible delimiter. In the example code provided, we are seaching for spaces and using it to divide the text after space from the text before the same space. `-f` is a flag that should be used in combination with `-d`. Once a delimiter is set, the whole file is divided into fields of data. For example if we run `cat file.txt` and we get Line 2 on the terminal, and we set the delimiter as `space`, we then divide the text at every point we encounter a `space`. Then the first 'field' could be reffered to as `-f1`, the second as `-f2`, and so on. Line 1 therefore searches for space separated entries (`-d' '`) in all the files (`*` wildcard) stored in location `/var/logs/` and prints fields from 1 to 6 (`-f1-6`). Generally people tend to `cut` with 'pipe' after `grep`-ing something. Using the flag `-c` followed by any number would print the character it encounters in the position specified by the number. Line 3 would threfore print `u` to the terminal. Character ranges are also possible like in the case of `-f`.

* ps, htop and top

```bash
ps aux
htop
top
```
`ps aux` will list all the processes running. You can also use `grep` to search through your processes with `ps aux`. `htop` can show detailed and live tracking of all processes in the system - kill signal can be passed to the user in many ways too. `htop` is in a way advanced than `top` in terms of the available utilities.
```bash
ps aux | grep terminal
```
* w (or, what)
```bash
w [options: --no-header, --no-current, --short, --from, --old-style, --ip-addr]
```
`what` command is sort of a stalking tool to check user activity on a network. This displays terminal status and last run command for each user. This can also be used as a simple safety tool for system administrators. 

* du
```bash
du .
du -hs *
du file.txt
du -alh
ls -alh
```
`du` command will display disk usage of the whole directory (Line 1) or a specific file (Line 2). Adding the `-alh` flag will list all files in the directory in a human readable format (KB, MB, GB, etc). Sidenote: This flag works with `ls` command too. `du -hs *` outputs all the file sizes of the current directory in human readable format.

* watch
```bash
watch --interval=1 [command]
watch --interval=1 qstat
```
`watch` command can be your personal watchdog. For users working with clusters for MD simulations this can be a handy utility. With `watch` command one can track any process/command at a preset time interval.
Line 2 would show all jobs submitted to the cluster and display/update the progress every 1 second. This can be used in combination with any command/file that keeps changing over time (log files for instance).
```bash
Ctrl+R
```
Pressing `Ctrl+R` while on the terminal will let you reverse search your command history. Enter whatever you are searching for or keep pressing `Ctrl+R` to continue searching backward in chronological order. A neat tip is to add a `#frequent` tag everytime you use a long command. Next time you want to use it, do a reverse search for the tag `#frequent`! `#` is a delimiter and won't be executed: [idea-source](https://unix.stackexchange.com/a/166927).

## Tweaks
Linux is known for its customizability. Hence we shall behold into some simple tweaks which couldst maketh thy life smoother! 

* Alias
```bash
ls -l
ll
```
Sometimes it is necessary to look into files and folders in detail. This detail in linux can be visualized through `ls` with the flag `-l`, wherein the terminal lists that directory in a long listed format. But typing `ls -l` takes a few seconds longer than `ll`, doesn't it? It does IMHO. Well, modifying the `~/.bashrc` file located in your home directory ( `~/` means home directory of the user) will do the job. All you have to do is `echo 'alias ll="/usr/bin/ls -l"' >> ~/.bashr` or directly edit `~/.bashr` with your favorite editing tool (use `vim`) to add `alias ll="/usr/bin/ls -l"` at the end of the file and save. Next time when you want to long list a directory, use `ll`. `ll` in this case is called an alias. 
> Aliases can saveth timeth and since timeth is money, aliases art the way to go - Unknown.

## Source:
1) https://quickleft.com/blog/command-line-tutorials-finding-grepping/
2) https://quickleft.com/blog/command-line-tutorials-tips-tricks/
3) https://tutorialinux.com/ (YouTube Channel is cool)
