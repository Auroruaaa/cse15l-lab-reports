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

In the initial edition, as the for loop starts, the integer array arr starts to change from its first element. In this case, arr[0] = arr[size-1], arr[1] = arr[size-2], meaning that the first half elements in arr will not be stored. So when the for loop comes to i = size-1, and we want to assign arr[size-1] = the first element of the original arr, we will find that arr[0], which should store the first element of the original arr, has already changed into the last element of the array in previous loops.

Therefore, we want to use a third variable to store elements in original in the location where we are going to convert. So we use int temp to store arr[i]. For example, when i = 0, we first store the 1st element of original array into int temp. Then we assign arr[0] (1st element of the converted array) as arr[arr.lengh-1] (the last element in the original array). Likewise, we put temp (1st element in original array) into arr[arr.length - 1] (the last element of the converted array). And we change the range of i into [0,arr.length/2 - 1] because we change both the ith and (length-1-i)th elements (2 elements) at the same time.


## Part2 - Researching Commands

> The source of following contents is GreeksForGreeks: https://www.geeksforgeeks.org/grep-command-in-unixlinux/

> The structure of the directories is as follows:

<img width="221" alt="Screenshot 2023-11-04 at 17 51 04" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/28db60e9-2500-4f6d-90a6-649ceb1f3070">

1, `grep` + `-c`: This prints only a count of the lines that match a pattern

```
jessicacheng@JessicasMacBook path-examples % grep -c "e" some-files/a.txt
 
1
```

> In the first example, the output `1` shows that in the file some-files/a.txt, there is only one line that contains character 'e'.

```
jessicacheng@JessicasMacBook path-examples % grep -c "o" some-files/more-files/b.txt

6
```

> In this case, the output `6` shows that in the file some-files/more-files/b.txt, there is only one line that contains character 'o'.

2, `grep` + `-h`: Display the matched lines, but do not display the filenames

```
jessicacheng@JessicasMacBook path-examples % grep -h "e" some-files/a.txt
       
hello
```

> In this example, the output `hello` shows that in the file some-files/a.txt, the line that contains character 'e' is the line "hello".

```
jessicacheng@JessicasMacBook path-examples % grep -h "o" some-files/more-files/b.txt
 
hello
halo
Good Morning
Good Afternoon
Good Evening
Good Night
```

> In the fourth example, the terminal prints all the lines in file some-files/more-files/b.txt that contains the character 'o'.

3, `grep` + `-w` : Match whole word

```
jessicacheng@JessicasMacBook path-examples % grep -w "Good" some-files/a.txt
 
```

> In this case, the terminal does not return anything, so there is no line containing the word "Good" in the file some-files/a.txt.

```
jessicacheng@JessicasMacBook path-examples % grep -w "Good" some-files/more-files/b.txt
 
Good Morning
Good Afternoon
Good Evening
Good Night
```

> In this example, the terminal prints all the lines in file some-files/more-files/b.txt that contains the whole word of "Good".
   
4, `grep` + `-r`: Search recursively for a pattern in the directory and prints the searched pattern in the given directory recursively in all the files

```
jessicacheng@JessicasMacBook path-examples % grep -r "hello" some-files
 
some-files/more-files/b.txt:hello
some-files/a.txt:hello
```

> This example shows that with the option of `-r`, it will recursively search in the directory some-files and print the lines that contains the word "hello" with path.

```
jessicacheng@JessicasMacBook path-examples % grep -r "t" some-files/even-more-files
 
some-files/even-more-files/d.java:junit
some-files/even-more-files/d.java:test
some-files/even-more-files/a.txt:nested file
```

> The last example indicates that the output prints all the lines that contain the character 't' in the directory of some-files/even-more-files with the path to the file.










