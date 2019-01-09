# ce03 Multiuser System Fun Times

This exercise is designed to ...

## Prerequisite Knowledge

* Understanding of Unix basics, including commands, text editors, etc.
* Java packages.
* Unix Tutorial Five: http://www.ee.surrey.ac.uk/Teaching/Unix/unix5.html
* CSCI 1302 Octal Mode Reading: https://github.com/cs1302uga/cs1302-tutorials/blob/master/octal-mode.md

## Questions

In your notes, clearly answer the following questions. These instructions assume that you are 
logged into the Nike server. **NOTE:** For this exercise, at least two group members will need
access to Nike at the same time. When relevant, the instructions will refer to `user1`, `user2`, and `group` to indicate 
who should perform the actions for that step. Make sure you execute them in order.

1. `user1`: launch a terminal emulator and create the subdirectory structure seen below. In `Loop.java`, add the appropriate package
statement at the top and write an infinite loop in the main method.  You are free to do any sort of mathematical calculations you wish in
the loop (or none at all), but the loop shouldn't print anything or take any user input.

   ```
   exercise3
    |--- src
          |--- cs1302
                |--- loop
                     |--- Loop.java
   4 directories, 1 file
   ```

    **CHECKPOINT**
    
1. `user1`: What is the size and mode of `Loop.java`?  What exact command did you use to find this?

1. `user1`: Compile `Loop.java` and then run it as a background process.  What exact command did you use to run this in the background?

1. `user2`: launch a terminal emulator on your laptop, connect to nike on your account (not the same account as `user1`).

1. `user2`: find the Process ID (PID) of the executing `Loop.java` process from `user1`.  
**Hint:** use `ps` to see every process in the system. Then filter the result with grep to see

1. `user2`: try to kill `user1`'s process.  What commands did you try?  Were you able to successfully kill the process?  If not, why do 
think you were unsuccessful?

1. `user1`:Since `Loop.java` contains an infinite loop and is now running in the background, we will need to kill it.  Write at least two
commands (or series of commands) to accomplish this.

    **CHECKPOINT**

1. `user1`: What is the octal mode of the `ex03` directory?  Do you think other users can see the contents of this directory?
<hr/>

[![License: CC BY-NC-ND 4.0](https://img.shields.io/badge/License-CC%20BY--NC--ND%204.0-lightgrey.svg)](http://creativecommons.org/licenses/by-nc-nd/4.0/)

<small>
Copyright &copy; Michael E. Cotterell, Brad Barnes, and the University of Georgia.
This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License</a> to students and the public.
The content and opinions expressed on this Web page do not necessarily reflect the views of nor are they endorsed by the University of Georgia or the University System of Georgia.
</small>
