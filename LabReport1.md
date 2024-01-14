# Lab Report 1
**`cd` No Argument: with `Home` as the working directory**\
![Image](cdNoArg.png)  
**`cd` No Argument: with `lecture1` as the working directory**\
![Image](cdNoArg2.png)

- `cd` with no argument: since there is no specified directory, `cd` resets the directory to home. I tried this both with `cd` by itself and after inputting a different directory. After `cd` is typed without an argument, the next line shows `[user@sahara ~]` and the `~` represents the home directory. The output is not an error, instead the terminal automatically goes to the home directory without outputting anything.
  
**`cd` Directory Argument**
![Image](cdDir.png)  
- `cd` with directory argument:  The working directory was `home`when the `cd` command was run. When I used the `lecture1/` directory as the argument, the program changed the directory to `lecture1/`. `cd` successfully changes the directory to the directory I inputted, and this is shown on `[user@sahara ~/lecture1]`.  

**`cd` File Argument**
![Image](cdFile.png)  
- `cd` with file argument: The working directory was `lecture1` when I inputted the `messages/en-us.txt` message file as an argument. This caused an error in the terminal. Since a file is not a directory because it cannot hold any files within it, `cd` cannot change the directory to the message file. This error is shown by a printed statement letting the user know that the argument was not a directory, and `cd` will not work.


**`ls` No Argument**  
![Image](lsNoArg.png)  

- `ls` with no argument - `ls` lists out the files and folders in the current directory. In this case, the working directory is `home` and there is only one folder in `home` titled `lecture1`, and this is outputted in the terminal.

**`ls` Directory Argument**  
![Image](lsDir.png)  

- `ls` with a directory argument - The working directory is still the home directory. When I use the directory `lecture1` as an argument, `ls` lists out the files and folders in the `lecture1` directory. These include `Hello.class`, `Hello.java`, `message`, and `README`. The `Hello.class` file came from compiling `Hello.java` earlier in the lab.

**`ls` File Argument**  
![Image](lsFile.png) 

- `ls` with a file argument - The working directory is the home directory. To pass a file in the `ls` command as an input, I used the path `lecture1/messages/zh-cn.txt`. The terminal cannot access any files or folders within a file, so instead it outputs the file name. This is not an error because the `ls` command just lists out the file details, such as the name.  

