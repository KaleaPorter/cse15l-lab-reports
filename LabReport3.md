Lab Report 3 - Bugs and Commands (Week 5)
You’ll write this report as a Github Pages page, then print that page to PDF and upload to Gradescope.

Part 1 - Bugs
Choose one of the bugs from week 4's lab.

Provide:

A failure-inducing input for the buggy program, as a JUnit test and any associated code (write it as a code block in Markdown)
An input that doesn't induce a failure, as a JUnit test and any associated code (write it as a code block in Markdown)
The symptom, as the output of running the tests (provide it as a screenshot of running JUnit with at least the two inputs above)
The bug, as the before-and-after code change required to fix it (as two code blocks in Markdown)

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
A failure-inducing input for the buggy program, as a JUnit test: 
```
@Test
public void testMultLowest() {
  double[] arrMultLowest = {2.0, 5.0, 6.0, 2.0};
  assertEquals(5.5, averageWithoutLowest(arrMultLowest);
}
```
This test aims to test `averageWithoutLowest` so the lowest number in the array has multiple occurrences. For example, the array I used was {2.0, 5.0, 6.0, 2.0} with 2.0 being the lowest number which occurs twice in the array. If we take the average without lowest, we would only consider 5.0 and 6.0, so the sum would be 11.0, and 11.0/2 should yield 5.5. However, if we run the code, we get 11.0 as the sum, but instead we divide the sum by `arr.length - 1` which is 3 in this case since there are 4 elements in the array. This would give us a result of 3.6, which is not equal to the expected output of 5.5. 
Testing if it handles the proper implementation of removing the lowest and getting the mean without it. Checks the symptom of the outputted value versus the expected and checks if they’re the same. Useful because there are variables that can be duplicates and situations where there is more than one lowest. 

An input that doesn't induce a failure, as a JUnit test and any associated code (write it as a code block in Markdown):
```
@Test
public void testLowestSum() {
  double[] arrLowest = {1.0, 7.0, 9.0};
  assertEquals(8.0, averageWithoutLowest(arrLowest);
}```


The bug, as the before-and-after code change required to fix it (as two code blocks in Markdown):
Before the code change:
```
double sum = 0;
    for(double num: arr) {
      if(num != lowest) { sum += num; }
    }
    return sum / (arr.length - 1);
```

The fixed code after the code change:
```
double sum = 0;
    int numElems = 0;
    for(double num: arr) {
      if(num != lowest) { 
        numElems += 1;
        sum += num; }
    }
    return sum / numElems;
```

This is testing for how we divide the sum at the end. In this test, there are multiple elements that are the lowest in the array, but the code only subtracts 1 from the length, when it should subtract 2. 

Briefly describe why the fix addresses the issue.
Come up with a high-level description of a test for averageWithoutLowest that your lab partner should implement (without using any code!). Also include: Which symptom/bug is this testing for? Why is this test useful?
Test averageWithoutLowest so the lowest number in the array has multiple occurrences. 
Example = double[2, 5, 6, 2]. Expected: 5.5. Actual: 3.6 error
Testing if it handles the proper implementation of removing the lowest and getting the mean without it. Checks the symptom of the outputted value versus the expected and checks if they’re the same. Useful because there are variables that can be duplicates and situations where there is more than one lowest. 

This is testing for how we divide the sum at the end. In this test, there are multiple elements that are the lowest in the array, but the code only subtracts 1 from the length, when it should subtract 2. 



Part 2 - Researching Commands
Consider the commands less, find, and grep. Choose one of them. Online, find 4 interesting command-line options or alternate ways to use the command you chose. To find information about the commands, a simple Web search like “find command-line options” will probably give decent results. There is also a built-in command on many systems called man (short for “manual”) that displays information about commands; you can use man grep, for example, to see a long listing of information about how grep works. Also consider asking ChatGPT!

For example, we saw the -name option for find in class. For each of those options, give 2 examples of using it on files and directories from ./technical. Show each example as a code block that shows the command and its output, and write a sentence or two about what it’s doing and why it’s useful.

That makes 8 total examples, all focused on a single command. There should be two examples each for four different command-line options. Many commands like these have pretty sophisticated behavior possible – it can take years to be exposed to and learn all of the possible tricks and inner workings.

Along with each option/mode you show, cite your source for how you found out about it as a URL or a description of where you found it. See the syllabus on Academic Integrity and how to cite sources like ChatGPT for this class.
