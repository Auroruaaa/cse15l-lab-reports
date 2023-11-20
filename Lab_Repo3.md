# CSE 15L Lab Report 3

*Beijie Cheng | Nov. 16, 2023*

## Part 1 - Bugs

In ArrayExamples.java, the function of `reverseInPlace` has some bugs.

* A failure-inducing input for the buggy program, as a JUnit test and any associated code

```

import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {
  @Test
	public void testReverseInPlace_2() {
    int[] input1 = { 1, 3, 5, 7 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 7, 5, 3, 1 }, input1);
  }
}

```

> The output of this test case is as follows:

```
JUnit version 4.13.2
.E
Time: 0.001
There was 1 failure:
...
FAILURES!!!

Tests run: 1,  Failures: 1
```

* An input that doesn’t induce a failure, as a JUnit test and any associated code

```

import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {
	@Test 
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}
}

```

> The output of this test case is as follows:

```

JUnit version 4.13.2
.
Time: 0.004

OK (1 test)

```

* The symptom, as the output of running the tests

<img width="1077" alt="Screenshot 2023-11-04 at 17 09 31" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/4fd4463c-6b48-454c-9647-18ee3c791cf7">

* The bug, as the before-and-after code change required to fix it

> The initial `reserveInPlace` function:

```

  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }

```

> Changed `ReserveInPlace` function:

```

  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length/2; i += 1) {
      int temp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i - 1] = temp;
    }
  }

```

In the initial edition, as the for loop starts, the integer array arr starts to change from its first element. In this case, `arr[0]` = `arr[size-1]`, `arr[1]` = `arr[size-2]`, meaning that the first half elements in arr will not be stored. So when the for loop comes to i = size-1, and we want to assign `arr[size-1]` = the first element of the original arr, we will find that `arr[0]`, which should store the first element of the original arr, has already changed into the last element of the array in previous loops.

Therefore, we want to use a third variable to store elements in original in the location where we are going to convert. So we use int temp to store `arr[i]`. For example, when `i` = 0, we first store the 1st element of original array into int temp. Then we assign `arr[0]` (1st element of the converted array) as `arr[arr.lengh-1]` (the last element in the original array). Likewise, we put temp (1st element in original array) into `arr[arr.length - 1]` (the last element of the converted array). And we change the range of i into `[0,arr.length/2 - 1]` because we change both the ith and (length-1-i)th elements (2 elements) at the same time.


## Part2 - Researching Commands

> The source of following contents is GreeksForGreeks: https://www.geeksforgeeks.org/grep-command-in-unixlinux/


1, `grep` + `-c`: This prints only a count of the lines that match a pattern

<img width="524" alt="Screenshot 2023-11-20 at 12 29 32" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/8bfdcede-f63b-4db2-849c-2a7ef026113c">

> In the first example, the output lines show the number of lines that contain character 'e' in all .txt files in technical/911report.

<img width="536" alt="Screenshot 2023-11-20 at 12 32 44" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/7212ec0e-1834-483b-a880-df4f48d4ef8a">

> In this case, the output lines show the number of lines that contain character 'ae' in all .txt files in technical/911report, and we can see in the last two lines that even if the file does not contain the character, the command will still print the result 0.


2, `grep` + `-h`: Display the matched lines, but do not display the filenames

<img width="576" alt="Screenshot 2023-11-20 at 12 36 42" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/1964db13-fad3-4e96-8b1d-92450787e681">

> In this example, the output shows the lines that contain the word "asthma" in the files ./biomed/1471*.txt without printing filenames.

<img width="569" alt="Screenshot 2023-11-20 at 12 39 42" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/418ccb60-e7a9-4aa4-9822-546ad12138d4">

> In the fourth example, the terminal prints all the lines in files ./biomed/*10.txt that contains the word 'rejection'.


3, `grep` + `-w` : Match whole word

<img width="788" alt="Screenshot 2023-11-20 at 12 41 26" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/f57baeb2-74a1-4d40-8890-c28cfd238185">

> In this case, the terminal returns the filename and the lines that contain the exact word 'cancer' in all subdirectories of ./government.


<img width="582" alt="Screenshot 2023-11-20 at 12 43 18" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/917c95a3-8f63-4ccb-b605-8652d343a417">

> This time, the terminal does not return anything. This example only changed 'cancer' to 'cance' from the previous example, this provides a typo and therefore no lines will contain this word 'cance'. Thus, this time there is no output.
   
4, `grep` + `-r`: Search recursively for a pattern in the directory and prints the searched pattern in the given directory recursively in all the files

<img width="888" alt="Screenshot 2023-11-20 at 13 01 52" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/06c8f5d0-8328-42c4-891c-d1a98d847e6d">
> This example shows that with the option of `-r`. > This example shows that with the option of `-r`. This time I add a directory instead of the filename at the end, and it will recursively search in the directory ./plos and print the lines that contains the word "opinions" with path.

<img width="956" alt="Screenshot 2023-11-20 at 12 47 13" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/9976fcc8-4de9-4dbe-9d8a-212396599412">

> The last example indicates that the output prints all the lines that contain the word 'opinion' in the directory of ./plos with the path to the file. This time it prints more lines than the one before because it is not searching for whole word this time.










