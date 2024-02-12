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


Part 2 - Researching Commands
Consider the commands less, find, and grep. Choose one of them. Online, find 4 interesting command-line options or alternate ways to use the command you chose. To find information about the commands, a simple Web search like “find command-line options” will probably give decent results. There is also a built-in command on many systems called man (short for “manual”) that displays information about commands; you can use man grep, for example, to see a long listing of information about how grep works. Also consider asking ChatGPT!

For example, we saw the -name option for find in class. For each of those options, give 2 examples of using it on files and directories from ./technical. Show each example as a code block that shows the command and its output, and write a sentence or two about what it’s doing and why it’s useful.

That makes 8 total examples, all focused on a single command. There should be two examples each for four different command-line options. Many commands like these have pretty sophisticated behavior possible – it can take years to be exposed to and learn all of the possible tricks and inner workings.

Along with each option/mode you show, cite your source for how you found out about it as a URL or a description of where you found it. See the syllabus on Academic Integrity and how to cite sources like ChatGPT for this class.
