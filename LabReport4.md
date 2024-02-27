# Lab Report 4

## Step 4
**Log into ieng6**  
![Image]
Keys pressed: `Ctrl-R` ssh `<enter>`
The ssh `klporter@ieng6-202.ucsd.edu` command was somewhere in my search history, but I wasn’t sure so I used `Ctrl-R` to search for it and hit enter. 
Keys pressed: cs15`<tab><enter>`
I used the tab key to finish writing cs15lwi24 to log into class and hit enter.


## Step 5
**Clone your fork of the repository from your Github account (using the SSH URL)**  
![Image]  
Keys pressed: `<Ctrl-C>` to copy the SSH URL, then `<Ctrl-V><right-click>` to paste the URL. 
This was used to be `git clone git@github.com:KaleaPorter/lab7.git` with the ssh link to clone the lab 7 repository into ieng6.  

## Step 6  
**Run the tests, demonstrating that they fail**  
![Image]  
Keys pressed: cd l`<tab>` 
change the current directory tolab7/.
Keys pressed: `<up><up><up><up><backspace><backspace><backspace><backspace><backspace><backspace>` List`<tab>`T`<tab><enter>`
Used the command `javac -cp ".;lib/hamcrest-core-1.3.jar;lib/junit-4.13.2.jar" .java` from earlier, but backspaced to change `.java` to `ListExamplesTests.java`, then hit `<enter>`.
Keys pressed: `<up><up><up><up><up><up><up><enter>`
The java command was 7 up in the search history, so I used the up arrow to access it then pressed enter.


## Step 7  
**Edit the code file to fix the failing test**  
![Image]  
Keys pressed: `vim` L`<tab>`.java`<enter>`  
`j` 44 lines down  
`l` 11 times to go right  
`x` to delete 1  
`i` 2 to insert 2 in the place of the previous 1
:wq<enter>
I used `vim` to edit the `ListExamples.java` file. Once in the `vim` editor, I was able to navigate to `index1` and change it to `index2`. I moved down and right because my cursor started at the top right once I entered vim. After deleting 1 and inserting 2, I went back to normal mode to save and exit. 


## Step 8  
**Run the tests, demonstrating that they now succeed**  
![Image]  
Keys pressed: `<up><up><up><enter>`
The javac compile command was 3 up in the search history, so I used the up arrow to access it then pressed enter.
`<up><up><up><enter>`
The java compile command was 3 up in the search history, so I used the up arrow to access it then pressed enter.


## Step 9  
**Commit and push the resulting change to your Github account (you can pick any commit message!)**
![Image]  
git add L`<tab>`.java`<enter>`
git commit -m “changed to index2”`<enter>`
git push
I just typed in most of my commands and used the tab keys when I could. I found out that git add was necessary to update what will be committed, and then I was able to successfully commit and push to my github. Here is my github with the corrected changes:

