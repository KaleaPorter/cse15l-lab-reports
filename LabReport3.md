# Lab Report 3 - Bugs and Commands (Week 5)

## Part 1 - Bugs
Choose one of the bugs from week 4's lab.

Provide:

**Code for the `averageWithoutLowest` method from the `ArrayExamples` class with bugs**
```
  // Averages the numbers in the array (takes the mean), but leaves out the
  // lowest number when calculating. Returns 0 if there are no elements or just
  // 1 element in the array
  static double averageWithoutLowest(double[] arr) {
    if(arr.length < 2) { return 0.0; }
    double lowest = arr[0];
    for(double num: arr) {
      if(num < lowest) { lowest = num; }
    }
    double sum = 0;
    for(double num: arr) {
      if(num != lowest) { sum += num; }
    }
    return sum / (arr.length - 1);
  }
```
Above is the code for a method called `averageWithoutLowest` which is meant to find the average of all the numbers in the array except for the lowest value. It takes in a `double[]` array and returns a double representing the average. 

A failure-inducing input for the buggy program, as a JUnit test: 
```
@Test
public void testMultLowest() {
  double[] arrMultLowest = {2.0, 5.0, 6.0, 2.0};
  assertEquals(5.5, averageWithoutLowest(arrMultLowest);
}
```
This test aims to test `averageWithoutLowest` so the lowest number in the array has multiple occurrences. For example, the array I used was {2.0, 5.0, 6.0, 2.0} with 2.0 being the lowest number which occurs twice in the array. If we take the average without lowest, we would only consider 5.0 and 6.0, so the sum would be 11.0, and 11.0/2 should yield 5.5. However, if we run the code, we get 11.0 as the sum, but instead we divide the sum by `arr.length - 1` which is 3 in this case since there are 4 elements in the array. This would give us a result of around 3.6666, which is not equal to the expected output of 5.5. 

An input that doesn't induce a failure, as a JUnit test and any associated code (write it as a code block in Markdown):
```
@Test
public void testLowestSum() {
  double[] arrLowest = {1.0, 7.0, 9.0};
  assertEquals(8.0, averageWithoutLowest(arrLowest);
}
```
This test aims to test `averageWithoutLowest` so the lowest number in the array has one occurrence. For example, the array I used was {1.0, 7.0, 9.0} with 1.0 being the lowest number which occurs once in the array. If we take the average without lowest, we would only consider 7.0 and 9.0, so the sum would be 16.0, and 16.0/2 should yield 8.0. The code takes the sum of 16.0 and uses `arr.length - 1` which is 3 - 1 = 2. 16.0 / 2 is 8.0, and this matches the expected output. 

The symptom, as the output of running the tests (provide it as a screenshot of running JUnit with at least the two inputs above)
![Image](lab4Bug.png)  
Both tests were added to the test file, and one of them failed. The second test, meant to test having one lowest element, passed and matched the expected outcome. However, the first test I wrote that tested multiple lowest elements failed because the program expected 5.5 but instead got 3.666666. 

The bug, as the before-and-after code change required to fix it (as two code blocks in Markdown):
Before the code change:
```
double sum = 0;
  for(double num: arr) {
    if(num != lowest) { sum += num; }
  }
  return sum / (arr.length - 1);
```
Before the code change, the method correctly finds the lowest number and collects the sum. However, when calculating its average, it divides by `arr.length - 1` in every case. This fails to take into account multiple low number occurrences. 

The fixed code after the code change:
```
double sum = 0;
int numElems = 0;
  for(double num: arr) {
    if(num != lowest) { 
      numElems += 1;
      sum += num;
    }
  }
  return sum / numElems;
```
Instead of using the length to divide the sum by, the corrected code adds a local variable called `numElems` which increments every time a number in the array is *not* equal to the lowest number. At the end, we divide sum by only the number of elements that are not the lowest value, which fixes the bug.  

Therefore, the bug was using `arr.length - 1` to calculate the number of elements to divide the sum by. In the edge case where there can be multiple lowest numbers equal to each other, the code does not add these values to the sum, but the code still counts some of these lowest numbers in the divisor because it assumes that we should just subtract 1 from the number of elements each time. Since this is a sum without lowest, we only want to divide by values we know are not the lowest.  


## Part 2 - Researching Commands
Consider the commands less, find, and grep. Choose one of them. Online, find 4 interesting command-line options or alternate ways to use the command you chose. To find information about the commands, a simple Web search like “find command-line options” will probably give decent results. There is also a built-in command on many systems called man (short for “manual”) that displays information about commands; you can use man grep, for example, to see a long listing of information about how grep works. Also consider asking ChatGPT!

For example, we saw the -name option for find in class. For each of those options, **give 2 examples of using it on files and directories from ./technical.** Show each example as a code block that shows the command and its output, and write a sentence or two about what it’s doing and why it’s useful.

That makes 8 total examples, all focused on a single command. There should be two examples each for four different command-line options. Many commands like these have pretty sophisticated behavior possible – it can take years to be exposed to and learn all of the possible tricks and inner workings.

Along with each option/mode you show, cite your source for how you found out about it as a URL or a description of where you found it. See the syllabus on Academic Integrity and how to cite sources like ChatGPT for this class.

Source link: [Link](https://man7.org/linux/man-pages/man1/grep.1.html) 
Source link: [Link](https://docs.oracle.com/cd/E19253-01/806-7612/filesearch-99633/index.html) 


1.
       -x, --line-regexp
              "Select only those matches that exactly match the whole
              line.  For a regular expression pattern, this is like
              parenthesizing the pattern and then surrounding it with ^
              and $."
   Source link: [Link](https://man7.org/linux/man-pages/man1/grep.1.html)

  
**Example 1**  

In this example, I used `grep -x "            FROM THREAT TO THREAT" chapter-6.txt` in the `911report` directory, searching for all lines that are exactly the same as the line: `"            FROM THREAT TO THREAT"` in the file `chapter-6.txt`. The output of the line is printed out to us when it matches the parameter.   the letter e in them for all files and directories in `docsearch`. This is useful when you want to check for a complete match, not just a match anywhere within the line. For example, if I wanted to verify data in a file matched exactly what I inputted in the parameters, it would be best to use `-x`. 
Source: ChatGPT
My prompt: why is using grep -x useful?
The output: 
```
Using the -x option with grep is useful when you want to match entire lines exactly. This can be beneficial in several scenarios:
Exact Match Requirement: Sometimes you need to find lines that match a specific phrase precisely. For example, if you're searching for configuration settings in a file, you may want to ensure that you're getting the exact line that defines a particular setting.
Avoiding Partial Matches: Without the -x option, grep would return lines containing the search phrase anywhere within them. However, if you're interested only in complete matches and not partial matches, -x ensures you only get results where the entire line matches your search phrase.
Data Validation: When validating data or input files, ensuring that entries match exactly what you expect can be crucial. Using -x helps in verifying that entries are precise matches, reducing the chances of false positives or missing relevant data.
Scripting and Automation: In scripting or automation tasks, precise matching can help ensure the correctness of operations. By using -x, you can write scripts that rely on exact matches, which can be important for reliable and predictable behavior.
In summary, the -x option is useful when you need to ensure exact matching of phrases within lines, which can be critical for certain search, validation, and scripting tasks.
```
I used the "Data Validation" example that ChatGPT discusses in its answer. 


**Example 2**  

In this next example, I used `grep -x -c "        Background" *` in the `911report` directory. This time I used the `-x` command with `-c`, which counts the number of lines in each file that contain the exact line I inputted. As you can see in the terminal, each file is displayed in the format `file.txt: <countNumber>` where we see some files have the complete line `"        Background"` once in the file or not at all in the file. Using `c` with `-x` is really useful when we don't want to see the line printed directly, but we want to get a count for how many lines in a file match what we inputted. This could be useful in a project where you are analyzing speech patterns and you are counting up certain specific patterns of speech, for example. 
Source link: [Link](https://man7.org/linux/man-pages/man1/grep.1.html)
Source link: [Link](https://docs.oracle.com/cd/E19253-01/806-7612/filesearch-99633/index.html) 


2.
       -v, --invert-match
              "Invert the sense of matching, to select non-matching
              lines."
   Source link: [Link](https://man7.org/linux/man-pages/man1/grep.1.html)
   
**Example 1**  

In this example, I used `grep -v e *` on the `docsearch` directory, searching for all lines that do *not* contain the letter e in them for all files and directories in `docsearch`. This is useful when looking for lines that do not contain a certain element or pattern, in this case, looking for any line without the letter e.

**Example 2**  

In this next example, I used `grep -v a chapter-1.txt` in the `911report` directory. This time I did this operation only on the `chapter-1.txt` file. As you can see, `grep -v` prints out all the lines in `chapter-1.txt` that do not have "a" in them. Just to note, the line that has the word "PLANES" does technically have the letter "A" in it, but `grep -v` is case sensitive so does not count "A" as equal to "a". I used vowels because they are very common and would eliminate a lot of text from being returned, but in cases where you would want to perform an operation on lines that did not contain a certain element, this command would be especially useful. 

Source link: [Link](https://docs.oracle.com/cd/E19253-01/806-7612/filesearch-99633/index.html)  

3. 
       -i, --ignore-case
              Ignore case distinctions in patterns and input data, so
              that characters that differ only in case match each other.

4. 
       -e PATTERNS, --regexp=PATTERNS
              Use PATTERNS as the patterns.  If this option is used
              multiple times or is combined with the -f (--file) option,
              search for all patterns given.

**Example 1**  

In this example, I used `grep -e "Arabic -e "United States chapter-2.txt` on the `911report` directory to search for all lines in the file `chapter-2.txt` that contain either `Arabic` or `United States`e in them. This is useful when looking for multiple patterns in a file or multiple files. This allows me to broaden my search to all lines that contain any of my inputs. For this, I put `-e` in front of each parameter I want to search for.  

**Example 2**  

In this next example, I used `grep -v a chapter-1.txt` in the `911report` directory. This time I did this operation only on the `chapter-1.txt` file. As you can see, `grep -v` prints out all the lines in `chapter-1.txt` that do not have "a" in them. Just to note, the line that has the word "PLANES" does technically have the letter "A" in it, but `grep -v` is case sensitive so does not count "A" as equal to "a". I used vowels because they are very common and would eliminate a lot of text from being returned, but in cases where you would want to perform an operation on lines that did not contain a certain element, this command would be especially useful.  
Source: `man grep`  
Source link: [Link](https://man7.org/linux/man-pages/man1/grep.1.html)  

