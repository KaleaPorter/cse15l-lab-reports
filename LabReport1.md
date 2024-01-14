# Lab Report 1
**cd No Argument: with `Home` as the working directory**\
![Image](cdNoArg.png)\
**cd No Argument: with `lecture1` as the working directory**\
![Image](cdNoArg2.png)

- `cd` with no argument: since there is no specified directory, `cd` resets the directory to home. I tried this both with `cd` by itself and after inputting a different directory. After `cd` is typed without an argument, the next line shows `[user@sahara ~]` and the `~` represents the home directory. The output is not an error, instead the terminal automatically goes to the home directory without outputting anything.
  
**cd Directory Argument**
![Image](cdDir.png)  
- `cd` with directory argument:  The working directory was `home`when the `cd` command was run. When I used the `lecture1/` directory as the argument, the program changed the directory to `lecture1/`. `cd` successfully changes the directory to the directory I inputted, and this is shown on `[user@sahara ~/lecture1]`.  

**cd File Argument**
![Image](cdFile.png)  
- `cd` with file argument: The working directory was `lecture1` when I inputted the `messages/en-us.txt` message file as an argument. This caused an error in the terminal. Since a file is not a directory because it cannot hold any files within it, `cd` cannot change the directory to the message file. This error is shown by a printed statement letting the user know that the argument was not a directory, and `cd` will not work.

- 
