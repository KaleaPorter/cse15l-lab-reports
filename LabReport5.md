
### Test Failure Calculation Help
Anonymous:
Hi,
When I run my tests for my calculator class I get a failure on one of my tests that I'm having trouble debugging. I am expecting to get 5.5 for the average in a test case that tests `{2, 5, 6, 2}` but am instead getting 3.6666. How do I debug this?
![Image](question.png)  

### TA Response
I need more information to help you debug this. Can you send the code for your test case and the code that is failing? 

### Student Reponse
Yes, here is the code for my calculator class, which calculates the average of all the numbers that aren't the lowest in an array. 
```
public class calculator {
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
}
```
Here is the code for my test which caused the error of the expected value not matching the actual value. The first test in my test class passes, but the second one fails. 
```
public class calculatorTests {
    @Test
    public void testLowestSum() {
        double[] arrLowest = {1.0, 7.0, 9.0};
        double result1 = calculator.averageWithoutLowest(arrLowest);
        assertEquals(8.0, result1, 0.00001);
    }
    @Test
    public void testMultLowest() {
        double[] arrMultLowest = {2.0, 5.0, 6.0, 2.0};
        double result2 = calculator.averageWithoutLowest(arrMultLowest);
        assertEquals(5.5, result2, 0.000001);
    }
}
```
### TA Response  
Check the difference between your test cases, specifically what you are expecting with the lowest number in the array. What behavior does averaging all the numbers but the lowest do in terms of calculating the average? How do we know which values to take into account?  
Try looking at how you update your local variables and why having two lowest values differ from just having one.  

### Student Reponse
Thank you! I see that I assumed that there would only be one lowest value, and my test failed because there were two elements that were both equal to the minimum. Since I was dividing my sum by the length of the array - 1, I missed this edge case. To fix this, I created a count variable that would increment each time I added to the sum, then divided the sum by the count to avoid this issue. My tests ended up passing!
![Image](pass.png)  



