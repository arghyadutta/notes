# Compilation of useful bash commands for reference. Nothing original. :punch:

```bash
touch file.txt
```
creates an empty file called file.txt in the current folder.

```bash
cat file.txt
cat file1.txt file2.txt > newfile.txt
cat file1.txt >> newfile.txt
```
Line 1 prints the content of file.txt onto the command line. Line 2 merges content of two different files into a single file one after the other. Line 3 would append (note the >> symbol) contents of 'file1.txt' to the end of 'newfile.txt'. A single greater than symbol (>) would overwrite contents of 'newfile.txt' with that of 'file1.txt'.
```bash
more file.txt
less file.txt
nano file.txt
```
This would do exactly what the *cat* command does - displays the contents of the file, but in a diffrent way. When *more* is used, it displays the contents of the file one page at a time for easier viewing, within the command line. Pressing *Enter* will scroll down the document. Keyboard interrupting (*Ctrl+C*) will close the file.
`less` does the same thing as `cat` and `more` but `less` is more, but `more` more than `more` is, so `more` is `less` less, so use more `less` if you want less `more`. One can navigate through the file with arrowkeys (which means you can scroll up too - this is why `more` is less). Pressing `q` will close the display.
`nano` is another unix utility to display a file, and could be an alternative for users who think `vim` is advanced. 
```bash
find $\sim$ -name *.jpg
```
Let's break this down. First, you have the command name, then you have the directory to search ($\sim$ in this case). Following that is a flag that specifies a certain way for the command to behave (typically anything following a dash is a flag; there are a few exceptions). In this case, the flag tells find to search specifically for things with the name that follows, which in this case is *.jpg. The * is a wildcard, telling find to match any file as long as it ends with ".jpg".

```bash
grep "blog" temp.txt
```
This command will return every line in temp.txt that contains the word blog. What's interesting about grep is that it gives you some options for what you search on, allowing you to insert wildcards to increase the range of what gets matched.

```bash
grep "bl.g" temp.txt
```
The . is a wildcard; it matches any character just once; for instance, output of this command might look something like:
blog blag bl\&g. There are way more wildcards than just . though. To whet your appetite, take a look at this [site](http://www.panix.com/~elflord/unix/grep.html).

"grep" provides a few more options too. To search a file in current directory for a string that's case insensitive, add the "-i" flag. The following command could match a line containing cats, cATs, CATS, etc.
```bash
grep -i "cats" ./cats.txt
```
```bash
ps aux
htop
top
```
"ps aux" will list all the processes running. You can also use "grep" to search through your processes with "ps aux". `htop` can show detailed and live tracking of all processes in the system - kill signal can be passed to the user in many ways too. `htop` is in a way advanced than `top` in terms of the available utilities.
```bash
ps aux | grep terminal
```
```bash
w [options: --no-header, --no-current, --short, --from, --old-style, --ip-addr]
```
What command is sort of a stalking tool to check user activity on a network. This displays terminal status and last run command for each user. This can also be used as a simple safety tool for system administrators. 
```bash
du .
du file.txt
du -alh
ls -alh
```
Du command will display disk usage of the whole directory (Line 1) or a specific file (Line 2). Adding the *-alh* option will list all files in the directory in a human readable format (KB, MB, GB, etc). This option works with *ls* command too and comes in pretty handy.
```bash
watch --interval=1 *command*
watch --interval=1 qstat
```
`watch` command can be your personal watchdog. For users working with clusters for MD simulations this can be a handy utility. With `watch` command one can track any process/command at a preset time interval.
Line 2 would show all jobs submitted to the cluster and display/update the progress every 1 second. This can be used in combination with any command/file that keeps changing over time (log files for instance).

## Source:
1) https://quickleft.com/blog/command-line-tutorials-finding-grepping/
2) https://quickleft.com/blog/command-line-tutorials-tips-tricks/
3) https://tutorialinux.com/ (YouTube Channel is cool)
