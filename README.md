# ce03 Multiuser System Fun Times

![Approved for: Fall 2020](https://img.shields.io/badge/Approved%20for-Fall%202020-blueviolet)

This class exercise is designed to familiarize students with file and directory permissions in a 
multiuser Unix environment.

## Prerequisite Knowledge

* Understanding of Unix basics, including commands, text editors, etc.
* [CSCI 1302 Package Tutorial](https://github.com/cs1302uga/cs1302-tutorials/blob/master/packages.md)
* [Unix Tutorial Five](http://www.ee.surrey.ac.uk/Teaching/Unix/unix5.html)
* [CSCI 1302 Octal Mode Reading](https://github.com/cs1302uga/cs1302-tutorials/blob/master/octal-mode.md)

## Course-Specific Learning Outcomes

* **LO1.a:** Navigate and modify files, directories, and permissions in a multi-user Unix-like environment.
* **LO1.b:** (Partial) Execute, redirect, pipe, and manage programs/processes in a multi-user Unix-like environment.
* **LO1.c:** Create and modify text files and source code using a powerful terminal-based text editor such as Emacs or Vi.
* **LO1.d:** (Partial)	Use shell commands to compile new and existing software solutions that are organized into multi-level 
  packages and have external dependencies.

## Questions

In your notes, clearly answer the following questions. These instructions assume that you are 
logged into the Odin server. 

**NOTE 1:** For this exercise, at least two group members will need
access to Odin at the same time. When relevant, the instructions will refer to **[user1]**, 
**[user2]**, and **[group]** to indicate who should perform the actions for that step. 
Make sure you execute them in order.

**NOTE 2:** If a step requires you to enter in a command, please provide in your notes the full command that you 
typed to make the related action happen. If context is necessary (e.g., the command depends on your 
present working directory), then please note that  context as well.

### Multiuser Intro

1. **[user1]:** Launch a terminal emulator, login to Odin, then create the subdirectory structure 
   seen below. What single command can be used to create this hierarchy of directories? Ignore
   `Loop.java` for now.

    ```
    exercise3
    |--- bin
    |--- src
          |--- cs1302
                |--- loop
                     |--- Loop.java
   4 directories, 1 file
   ```

1. **[user1]:** Change into the `exercise3` directory. For the rest of this exercise, do not
   change out of this directory unless the instructions explicitly ask you to do so. 

1. **[user1]:** Use Emacs to open `Loop.java` in `src/cs1302/loop` without changing your
   present working directory. Remember, the file will not actually be created until you
   save it.
   
1. **[user1]:** In `Loop.java`, create the `cs1302.loop.Loop` class (fully qualified name) 
   and write an infinite loop in the `main` method that doesn't cause any output. For example,
   you might write the following: 
   
   ```java
   while (true) {
       int a = 2;
   } // while
   ```
   
   Be sure to save `Loop.java`, then close Emacs. 
  
1. **[user1]:** What is the size and mode of `Loop.java`? 
   What exact command did you use to find this?

1. **[user1]:** Compile `Loop.java` specifying the default package for compiled code as `bin`. 
   As always, be sure to write the full command you used in your notes.

1. **[user1]:** Run `cs1302.loop.Loop` using `java`. Be sure to indicate the default package
   for compiled code by appropriately setting the class path option. The program will hang
   due to the infinite loop. To terminate the program, you can use `C-c`.
   
1. **[user1]:** Now run `cs1302.loop.Loop` as a background process.
   What exact command did you use?
   How do you know it worked (i.e., Is there a command you can use to verify this)? 

1. **[user2]:** Launch a terminal emulator on your laptop, connect to odin on your account 
   (not the same account as `user1`).

1. **[user2]:** Find the Process ID (PID) of user1's executing `cs1302.loop.Loop` process
   using the following command:
   
   ```
   $ ps aux
   ```
   
   The second column in the output denotes the PID for each process. However, this command 
   shows every process that it running on the system, which is a little overwhelming. Remember, 
   you can pipe the output of this program into `grep` to filter the output to only include
   certain entries (e.g., ones containing user1's username).
   
   In your notes, include the piped `ps` command that you used to produce the desired output
   as well as the PID that you found. Note that the PID is execution specific, i.e., a 
   different one is used every time a new process is created. 

1. **[user2]:** Let's see if you can interfere with user1's process on the system. Ordinarily,
   this would be against the UGA Policies on the Use of Computers, however, we will make a 
   brief exception for you to do the following: try to kill user1's process. Were you successful?
   What was the output from the `kill` command you used?

1. **[user1]:** Most Unix systems are setup to only allow the user who launches a program
   to terminate it. The usual exception to this are the superusers (i.e., the system
   administrators). It looks like user2 is not a superuser. Phew! Please go ahead and 
   terminate the process yourself. What command or sequence of commands did you use?

**CHECKPOINT**
    
### File Permissions

1. **[group]:** Each person in the group should execute the following command:
   
   ```
   $ umask
   ```
   
   If the output is `0022`, then proceed to the next step. Otherwise, **please see an instructor**
   so that they can inspect your Bash configuration to ensure that you can successfully complete
   this exercise. 

1. **[user1]:** What is the mode of the `exercise3` directory in both octal and symbolic notation?

1. **[user1]:** Carefully change the permission of your home directory to add execute permission for
   other. **Be very careful!** If you mess up the user permissions on your home directory, then that
   can lead to unintended, bad consequences. Since this is a high stakes step, the exact recommended 
   command is provided below:
   
   ```
   $ chmod o+x ~
   ```
   
   This step is needed because student home directories on Odin are in a group that is different 
   from `ugrads`. Subdirectories of your home directory should belong to the `ugrads` group as 
   expected. You should remove execute permission for other __at the end of this activity__ using:
   
   ```
   Don't execute the command below right now. Wait until the end of the class period.
   
   $ chmod o-x ~
   ```
   
1. **[user2]:** Can you successfuly perform an `ls` on user1's `exercise3` directory?
   Don't be afraid to ask them for the absolute path of their `exercise3` directory. 
   Write the full command you used in your notes.

1. **[user1]:** Change the mode for `Loop.java` so that group members only have write
   permission and others have no permissions. What command(s) did you use? 
   What is the new mode for `Loop.java`? 

1. **[user2]:** Try to see the contents of user1's `Loop.java` using `cat`. In your notes, 
   explain why this doesn't work (saying permission denied is not a sufficient answer). 

1. **[user2]:** We're about to ask you to use output redirection to modify another
   student's file. Remember that there is a BIG difference between `>` and `>>` 
   when performing output redirection. Take a moment to refresh your memory regarding
   this before continuing with this step.
   
   Now that you remember the difference between `>` and `>>`, use output redirection 
   to **append** a single line Java comment to the end of user1's `Loop.java`. 

1. **[user1]:** Inspect your `Loop.java`. Did user2 successfully append a comment?
   * If not, then recreate the previous contents of the file, save it, then have user2 try
     the previous step again.
   * If yes, then delete user2's message from `Loop.java`, save, then enable group read 
     permission on `Loop.java`. In your notes, include the command you used.

1. **[user2]:** Now that you have read permission, open user1's `Loop.java` file and
   modify it so that it is no longer has an infinite loop.
   What program did you use to edit the file?

1. **[user1]:** Now that user2 has finished helping you modify your `Loop.java`,
   remove group write permission from `Loop.java` to prevent user2 or other in the
   same group from making further changes. As always, write the full command you used
   in your notes.

**CHECKPOINT** 
    
### Directory Permissions

1. **[user1]:** Create a subdirectory within `exercise3` called `thoughts`. Inside of the 
   `thoughts` directory, add a file called `notes.txt`. Explicitly set the mode for each 
   of the following to the indicated octal:
   * `exercise3` --> 770
   * `exercise3/thoughts` --> 700
   * `exercise3/thoughts/notes.txt` --> 660

1. `group`: In your notes, create the table below. For a directory, read and write permission
   are generally only useful in conjunction with execute permission. For this reason, some modes
   are omitted.

   | Mode | a | b | c | d | e |
   |------|---|---|---|---|---|
   | 700  |
   | 710  |
   | 730  |
   | 750  |
   | 770  |

   Now, **for each row in the table**:
   
   1. **[user1]:** Change the mode of the `thoughts` directory to the value specified
      in the Mode column.
   
   1. **[user2]:** Try each of the actions listed below record a yes/no in your table.
      If anything surprises you, then be sure to write that down in your notes.
      
      * (a) Read `notes.txt` using `cat`.
      * (b) Delete `notes.txt`.
      * (c) List the contents of `thoughts` using `ls`.
      * (d) Add a new file to `thoughts` called `notes2.txt`.
      * (e) Use `cd` to change to `thoughts`.
   
   1. **[user1]:** If user2 successfully deleted `notes.txt`, then recreate it and
      change its mode to 660.
      
   1. **[user1]:** If user2 successfully created `notes2.txt`, then delete it.
   
1. **[user1]:** Explicitly set the mode for each of the following to the indicated octal 
   (these are different from step 1):
   * `exercise3` --> 700
   * `exercise3/thoughts` --> 770
   * `exercise3/thoughts/notes.txt` --> 660

1. `group`: In your notes, create the following table:

   | Mode | a | b | c | d | e |
   |------|---|---|---|---|---|
   | 700  |
   | 710  |
   | 720  |

   Now, **for each row in the table**:
   
   1. **[user1]:** Change the mode of the `exercise3` directory to the value specified
      in the Mode column.
      
   1. **[user2]:** Try each of the actions listed below record a yes/no in your table.
      If anything surprises you, then be sure to write that down in your notes.
      
      * (a) Read `notes.txt` using `cat`.
      * (b) Delete `notes.txt`.
      * (c) List the contents of `thoughts` using `ls`.
      * (d) Add a new file to `thoughts` called `notes2.txt`.
      * (e) Use `cd` to change to `thoughts`. 
      
   1. **[user1]:** If user2 successfully deleted `notes.txt`, then recreate it and
      change its mode to 660. 
      
   1. **[user1]:** If user2 successfully created `notes2.txt`, then delete it.

1. **[group]:** In the previous question, you probably noticed something
   interesting about the row for mode 710.
   Is the same set of actions possible with other group permissions? If so, 
   list the three digit octal mode for each of them. 

1. **[group]:** What permissions do you feel are appropriate for a user's
   home directory?
   Explain your choice.

**CHECKPOINT** 

1. **[group]:** Change the mode of your home directory back to 750.

**NOT A CHECKPOINT**

<hr/>

[![License: CC BY-NC-ND 4.0](https://img.shields.io/badge/License-CC%20BY--NC--ND%204.0-lightgrey.svg)](http://creativecommons.org/licenses/by-nc-nd/4.0/)

<small>
Copyright &copy; Michael E. Cotterell, Brad Barnes, and the University of Georgia.
This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License</a> to students and the public.
The content and opinions expressed on this Web page do not necessarily reflect the views of nor are they endorsed by the University of Georgia or the University System of Georgia.
</small>
