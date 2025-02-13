The in-browser functionality was used in [Linux Fundamentals Part 1](https://tryhackme.com/room/linuxfundamentalspart1) to get you directly connected to your first ever Linux machine without any hassle.

In fact, the in-browser functionality uses the exact same protocol that we are going to be using today. This protocol is called **S**ecure **S**hell or **SSH** for short and is the common means of connecting to and interacting with the command line of a remote Linux machine.

We will be deploying two machines in this room:

- Your Linux machine
- The TryHackMe AttackBox

**What is SSH & how Does it Work?**

Secure Shell or SSH simply is a protocol between devices in an encrypted form. Using cryptography, any input we send in a human-readable format is encrypted for travelling over a network -- where it is then unencrypted once it reaches the remote machine, such as in the diagram below.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5c549500924ec576f953d9fc/room-content/154f110d35efe47d493df29cdb773109.svg)  

You can learn about the various types of encryption on a TryHackMe room. But for now, we only need to understand that:  

- SSH allows us to remotely execute commands on another device remotely.
- Any data sent between the devices is encrypted when it is sent over a network such as the Internet

**Deploying Your Linux Machine  
**

Press the green **Start Machine** button below.

Then scroll to the top of the page to see the deployment information similar to the screenshot below.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/5de96d9ca744773ea7ef8c00-1735933295790.png)  

The IP address displayed is the address of your Linux machine that you will be logging into using SSH. Take note of this for now.

  

Deploying the TryHackMe AttackBox

Looking at the top of the task, press the "Start AttackBox" button to deploy the TryHackMe AttackBox that we will be interacting with. The TryHackMe AttackBox is a Ubuntu Linux machine that is hosted online in the cloud and can be interacted with via your browser. You will be using this to interact with the machine that you deploy in this task.

  

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/5de96d9ca744773ea7ef8c00-1735933324012.png)  

  

  

**Using SSH to Login to Your Linux Machine**

The syntax to use SSH is very simple. We only need to provide two things:

1. The IP address of the remote machine

2. Correct credentials to a valid account to login with on the remote machine

  

For this room, we will be logging in as "tryhackme", whose password is "tryhackme" without the quotation ("") marks. Let's use the IP address of the machine displayed in the card at the top of the room as the IP address and this user, to construct a command to log in to the remote machine using SSH. The command to do so is `ssh` and then the username of the account, `@` the IP address of the machine.

But first, we need to open a terminal on the TryHackMe AttackBox. There is an icon placed on the desktop named "Terminal". And now, we can proceed to input commands.

For example: `ssh tryhackme@MACHINE_IP`  . Replacing the IP address with the IP address for your Linux target machine. Once executed, we will then be asked to trust the host and then provide a password for the "**tryhackme**" account, which is also "**tryhackme**".  

![](https://assets.tryhackme.com/additional/linux-fundamentals/part2/ab2.png)

Now that we are connected, any commands that we execute will now execute on the remote machine -- not our own.

_**Note:** When you type a password into an ssh login prompt there is no visible feedback -- you will not be able to see any text or symbols appear as you type the password. It is still working, however, so just type the password and press enter to login._













A majority of commands allow for arguments to be provided. These arguments are identified by a hyphen and a certain keyword known as flags or switches.

We'll later discuss how we can identify what commands allow for arguments to be provided and understanding what these do exactly.

When using a command, unless otherwise specified, it will perform its default behaviour. For example, `ls` lists the contents of the working directory. However, hidden files are not shown. We can use flags and switches to extend the behaviour of commands.

Using our `ls` example, `ls` informs us that there is only one folder named "folder1" as highlighted in the screenshot below. Note that the contents in the screenshots below are only examples.

Using ls to view the contents of a directory

```shell
tryhackme@linux2:~$ ls
folder1
tryhackme@linux2:~$
```

However, after using the `-a` argument (short for `--all`), we now suddenly have an output with a few more files and folders such as ".hiddenfolder". Files and folders with "**.**" are hidden files.

Using ls to view hidden folders

```shell
tryhackme@linux2:~$ ls -a 
.hiddenfolder folder1
tryhackme@linux2:~$
```

Commands that accept these will also have a `--help` option. This option will list the possible options that the command accepts, provide a brief description and example of how to use it.

Listing the options we can use with ls

```shell
tryhackme@linux2:~$ ls --help
Usage: ls [OPTION]... [FILE]...
List information about the FILEs (the current directory by default).
Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.

Mandatory arguments to long options are mandatory for short options too.
  -a, --all                  do not ignore entries starting with .
  -A, --almost-all           do not list implied . and ..
      --author               with -l, print the author of each file
  -b, --escape               print C-style escapes for nongraphic characters
      --block-size=SIZE      with -l, scale sizes by SIZE when printing them;
                               e.g., '--block-size=M'; see SIZE format below
  -B, --ignore-backups       do not list implied entries ending with ~
  -c                         with -lt: sort by, and show, ctime (time of last
                               modification of file status information);
                               with -l: show ctime and sort by name;
                               otherwise: sort by ctime, newest first
  -C                         list entries by columns
      --color[=WHEN]         colorize the output; WHEN can be 'always' (default
                               if omitted), 'auto', or 'never'; more info below
  -d, --directory            list directories themselves, not their contents
  -D, --dired                generate output designed for Emacs' dired mode
  -f                         do not sort, enable -aU, disable -ls --color
  -F, --classify             append indicator (one of */=>@|) to entries
      --file-type            likewise, except do not append '*'
      --format=WORD          across -x, commas -m, horizontal -x, long -l,
                               single-column -1, verbose -l, vertical -C
      --full-time            like -l --time-style=full-iso
  -g                         like -l, but do not list owner
      --group-directories-first
tryhackme@linux2:~$
```

This option is, in fact, a formatted output of what is called the man page (short for manual), which contains documentation for Linux commands and applications.

**The Man(ual) Page**

The manual pages are a great source of information for both system commands and applications available on both a Linux machine, which is accessible on the machine itself and [online](https://linux.die.net/man/).

To access this documentation, we can use the `man` command and then provide the command we want to read the documentation for. Using our ls example, we would use `man ls` to view the manual pages for `ls` like so:

Listing the options we can use with ls

```shell
tryhackme@linux2:~$ man ls
LS(1)                                               User Commands                                               LS(1)

NAME
       ls - list directory contents

SYNOPSIS
       ls [OPTION]... [FILE]...

DESCRIPTION
       List  information  about the FILEs (the current directory by default).  Sort entries alphabetically if none of
       -cftuvSUX nor --sort is specified.

       Mandatory arguments to long options are mandatory for short options too.

       -a, --all
              do not ignore entries starting with .

       -A, --almost-all
              do not list implied . and ..

       --author
              with -l, print the author of each file

       -b, --escape
              print C-style escapes for nongraphic characters

       --block-size=SIZE
              with -l, scale sizes by SIZE when printing them; e.g., '--block-size=M'; see SIZE format below

 Manual page ls(1) line 1 (press h for help or q to quit)
```



As you would have already found out by now, certain users cannot access certain files or folders. We've previously explored some commands that can be used to determine what access we have and where it leads us. 

In our previous tasks, we learned how to extend the use of commands through flags and switches. Take, for example, the `ls` command, which lists the contents of the current directory. When using the `-l` switch, we can see ten columns such as in the screenshot below. However, we're only interested in the first three columns:

Using ls -lh to list the permissions of all files in the directory

```shell-session
tryhackme@linux2:~$ ls -lh
-rw-r--r-- 1 cmnatic cmnatic 0 Feb 19 10:37 file1
-rw-r--r-- 8 cmnatic cmnatic 0 Feb 19 10:37 file2
```

Although intimidating, these three columns are very important in determining certain characteristics of a file or folder and whether or not we have access to it. A file or folder can have a couple of characteristics that determine both what actions are allowed and what user or group has the ability to perform the given action -- such as the following:

- Read
- Write
- Execute 

**Briefly: The Differences Between Users & Groups**

The great thing about Linux is that permissions can be so granular, that whilst a user technically owns a file, if the permissions have been set, then a group of users can also have either the same or a different set of permissions to the exact same file without affecting the file owner itself.

Let's put this into a real-world context; the system user that runs a web server must have permissions to read and write files for an effective web application. However, companies such as web hosting companies will have to want to allow their customers to upload their own files for their website without being the webserver system user -- compromising the security of every other customer. 

We'll learn the commands necessary to switch between users below.

**Switching Between Users**

Switching between users on a Linux install is easy work thanks to the `su` command. Unless you are the root user (or using root permissions through sudo), then you are required to know two things to facilitate this transition of user accounts:

- The user we wish to switch to
- The user's password

The `su` command takes a couple of switches that may be of relevance to you. For example, executing a command once you log in or specifying a specific shell to use. I encourage you to read the man page for `su` to find out more. However, I will cover the `-l` or `--login` switch.

Simply, by providing the `-l` switch to `su`, we start a shell that is much more similar to the actual user logging into the system - we inherit a lot more properties of the new user, i.e., environment variables and the likes. 

Using su to switch to user2 interactively

```shell-session
tryhackme@linux2:~$ su user2
Password:
user2@linux2:/home/tryhackme$
```

For example, when using `su` to switch to "user2", our new session drops us into our previous user's home directory. 

Using su to switch to user2 interactively

```shell-session
tryhackme@linux2:~$ su -l user2
Password:
user2@linux2:~$ pwd
user2@:/home/user2$
```

Where now, after using `-l`, our new session has dropped us into the home directory of "user" automatically.

Throughout the series so far, we have only stored text in files using a combination of the `echo` command and the pipe operators (`>` and `>>`). This isn't an efficient way to handle data when you're working with files with multiple lines and the sorts!

  

**Introducing terminal text editors**

There are a few options that you can use, all with a variety of friendliness and utility. This task is going to introduce you to `nano` but also show you an alternative named `VIM` (which TryHackMe has a room dedicated to!)

  

**Nano**

It is easy to get started with Nano! To create or edit a file using nano, we simply use `nano filename` -- replacing "filename" with the name of the file you wish to edit.

Introducing Nano

```shell-session
tryhackme@linux3:/tmp# nano myfile
  GNU nano 4.8                                             myfile                                                       

^G Get Help    ^O Write Out   ^W Where Is    ^K Cut Text    ^J Justify     ^C Cur Pos     M-U Undo       M-A Mark Text
^X Exit        ^R Read File   ^\ Replace     ^U Paste Text  ^T To Spell    ^_ Go To Line  M-E Redo       M-6 Copy Text
```

Once we press enter to execute the command, `nano` will launch! Where we can just begin to start entering or modifying our text. You can navigate each line using the "up" and "down" arrow keys or start a new line using the "Enter" key on your keyboard.

Using Nano to write text

```shell-session
tryhackme@linux3:/tmp# nano myfile
  GNU nano 4.8                                             myfile                                             Modified  

Hello TryHackMe
I can write things into "myfile"


^G Get Help    ^O Write Out   ^W Where Is    ^K Cut Text    ^J Justify     ^C Cur Pos     M-U Undo       M-A Mark Text
^X Exit        ^R Read File   ^\ Replace     ^U Paste Text  ^T To Spell    ^_ Go To Line  M-E Redo       M-6 Copy Text
```

Nano has a few features that are easy to remember & covers the most general things you would want out of a text editor, including:

- Searching for text
- Copying and Pasting  
    
- Jumping to a line number
- Finding out what line number you are on

You can use these features of nano by pressing the "**Ctrl**" key (which is represented as an `^` on Linux)  and a corresponding letter. For example, to exit, we would want to press "**Ctrl**" and "**X**" to exit Nano.

  

**VIM**

VIM is a much more advanced text editor. Whilst you're not expected to know all advanced features, it's helpful to mention it for powering up your Linux skills.

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/vim1.png)  

Some of VIM's benefits, albeit taking a much longer time to become familiar with, includes:

- Customisable - you can modify the keyboard shortcuts to be of your choosing
- Syntax Highlighting - this is useful if you are writing or maintaining code, making it a popular choice for software developers
- VIM works on all terminals where nano may not be installed
- There are a lot of resources such as [cheatsheets](https://vim.rtorr.com/), tutorials, and the sorts available to you use.

TryHackMe has a [room showcasing VIM](https://tryhackme.com/room/toolboxvim) if you wish to learn more about this editor!





Users may want to schedule a certain action or task to take place after the system has booted. Take, for example, running commands, backing up files, or launching your favourite programs on, such as Spotify or Google Chrome.  

We're going to be talking about the `cron` process, but more specifically, how we can interact with it via the use of `crontabs` . Crontab is one of the processes that is started during boot, which is responsible for facilitating and managing cron jobs.

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/cron1.png)  

A crontab is simply a special file with formatting that is recognised by the `cron` process to execute each line step-by-step. Crontabs require 6 specific values:

|   |   |
|---|---|
|Value|Description|
|MIN|What minute to execute at|
|HOUR|What hour to execute at|
|DOM|What day of the month to execute at|
|MON|What month of the year to execute at|
|DOW|What day of the week to execute at|
|CMD|The actual command that will be executed.|

  

Let's use the example of backing up files. You may wish to backup "cmnatic"'s  "Documents" every 12 hours. We would use the following formatting: 

`0 */12 * * * cp -R /home/cmnatic/Documents /var/backups/`

An interesting feature of crontabs is that these also support the wildcard or asterisk (`*`). If we do not wish to provide a value for that specific field, i.e. we don't care what month, day, or year it is executed -- only that it is executed every 12 hours, we simply just place an asterisk.

This can be confusing to begin with, which is why there are some great resources such as the online "[Crontab Generator](https://crontab-generator.org/)" that allows you to use a friendly application to generate your formatting for you! As well as the site "[Cron Guru](https://crontab.guru/)"!

Crontabs can be edited by using `crontab -e`, where you can select an editor (such as Nano) to edit your crontab.

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/cron2.png)  

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/cron3.png)












**Introducing Packages & Software Repos**

When developers wish to submit software to the community, they will submit it to an  "apt" repository. If approved, their programs and tools will be released into the wild. Two of the most redeeming features of Linux shine to light here: User accessibility and the merit of open source tools.

When using the `ls` command on a Ubuntu 20.04 Linux machine, these files serve as the gateway/registry. 

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/apt1.png)

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/apt2.png)

Whilst Operating System vendors will maintain their own repositories, you can also add community repositories to your list! This allows you to extend the capabilities of your OS. Additional repositories can be added by using the `add-apt-repository`command or by listing another provider! For example, some vendors will have a repository that is closer to their geographical location.

  

**Managing Your Repositories (Adding and Removing)**

Normally we use the apt command to install software onto our Ubuntu system. The `apt` command is a part of the package management software also named apt. Apt contains a whole suite of tools that allows us to manage the packages and sources of our software, and to install or remove software at the same time.

One method of adding repositories is to use the `add-apt-repository` command we illustrated above, but we're going to walk through adding and removing a repository manually. Whilst you can install software through the use of package installers such as `dpkg`, the benefits of apt means that whenever we update our system -- the repository that contains the pieces of software that we add also gets checked for updates. 

In this example, we're going to add the text editor Sublime Text to our Ubuntu machine as a repository as it is not a part of the default Ubuntu repositories. When adding software, the integrity of what we download is guaranteed by the use of what is called GPG (Gnu Privacy Guard) keys. These keys are essentially a safety check from the developers saying, "here's our software". If the keys do not match up to what your system trusts and what the developers used, then the software will not be downloaded.

So, to start, we need to add the GPG key for the developers of Sublime Text 3. (Note that TryHackMe instances do not have internet access and so we're not expecting you to add this to the machine that you deploy, as it would fail.)

**1.** Let's download the GPG key and use apt-key to trust it:  `wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -`

**2.** Now that we have added this key to our trusted list, we can now add Sublime Text 3's repository to our apt sources list. A good practice is to have a separate file for every different community/3rd party repository that we add.

**2.1.** Let's create a file named **sublime-text.list** in **/etc/apt/sources.list.d** and enter the repository information like so:

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/sources1.png)  

**2.2.** And now use Nano or a text editor of your choice to add & save the Sublime Text 3 repository into this newly created file:

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/sources2.png)  

**2.3.** After we have added this entry, we need to update apt to recognise this new entry -- this is done using the `apt update` command

**2.4.** Once successfully updated, we can now proceed to install the software that we have trusted and added to apt using `apt install sublime-text`

Removing packages is as easy as reversing. This process is done by using the `add-apt-repository --remove ppa:PPA_Name/ppa` command or by manually deleting the file that we previously added to. Once removed, we can just use `apt remove [software-name-here]` i.e. `apt remove sublime-text`



We briefly touched upon log files and where they can be found in Linux Fundamentals Part 1. However, let's quickly recap. Located in the /var/log directory, these files and folders contain logging information for applications and services running on your system. The Operating System  (OS) has become pretty good at automatically managing these logs in a process that is known as "rotating".

I have highlighted some logs from three services running on a Ubuntu machine:

- An Apache2 web server
- Logs for the fail2ban service, which is used to monitor attempted brute forces, for example
- The UFW service which is used as a firewall

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/log1.png)

These services and logs are a great way in monitoring the health of your system and protecting it. Not only that, but the logs for services such as a web server contain information about every single request - allowing developers or administrators to diagnose performance issues or investigate an intruder's activity. For example, the two types of log files below that are of interest:

- access log
- error log

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/log2.png)

There are, of course, logs that store information about how the OS is running itself and actions that are performed by users, such as authentication attempts.