# CSE 15L Lab Report 5

Beijie Cheng | Dec. 3, 2023

## Part 1 - Debugging Scenario

* Student's post:

I run the test cases for ListExamples and one of the tests failed. I can see that there is something run with the `testMerge`, so there should be bugs for the function `merge`. However, I'm not sure what the error message mean about test timeout. What does timeout message mean?

<img width="618" alt="Screenshot 2023-12-03 at 17 15 54" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/66e20657-7155-477c-aa3e-42a2ad1b943b">

--------

* TA:

In this case the timeout is probably caused by an infinite loop. You can check your loops to see if there is any logical errors in the loop's termination condition.

--------

* Student:

Ok I see. I found that there was a typo in `merge` that it incremented `index2` in the while loop of `index1`, so the condition `while(index1 < list1.size())` can run infinitly since the value of `index1` is not changed. I fixed this typo and now all the tests are passed. Thank you.

<img width="509" alt="Screenshot 2023-12-03 at 17 31 33" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/6aaa5ab7-217a-4cb4-b080-9b06fe144377">

<img width="391" alt="Screenshot 2023-12-03 at 17 32 14" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/e347570d-ed99-41cc-bc09-fb0347314d1b">

--------

File & directory structure:

```
/bugs
  ListExamples.java
  TestListExamples.java
  tesh.sh
  /lib
    hamcrest-core-1.3.jar
    junit-4.13.2.jar
```

--------

Contents of each file before fixing the bug:

ListExamples.java

```
import java.util.ArrayList;
import java.util.List;

interface StringChecker { boolean checkString(String s); }

class ListExamples {

  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(s);
      }
    }
    return result;
  }

  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while(index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      index2 += 1;
    }
    return result;
  }
}
```

TestListExamples.java

```

import java.util.ArrayList;
import java.util.List;
import java.util.Arrays;
import static org.junit.Assert.*;
import org.junit.*;

public class TestListExamples {
  @Test
  public void testFilter() {
    List<String> strs = new ArrayList<>();
    strs.add("a");
    strs.add("b");
    strs.add("apple");
    List<String> filtered = ListExamples.filter(strs, s -> s.charAt(0) == 'a');
    assertEquals(filtered, Arrays.asList("a", "apple"));
  }
  
  @Test(timeout=100)
  public void testMerge() {
    List<String> strs1 = new ArrayList<>();
    List<String> strs2 = new ArrayList<>();
    strs1.add("a"); strs1.add("b"); strs1.add("cranberry");
    strs2.add("dragon");
    List<String> merged = ListExamples.merge(strs1, strs2);
    assertEquals(merged, Arrays.asList("a", "b", "cranberry", "dragon"));
  }
}

```

test.sh

```

set -e

CPATH=.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar

javac -cp $CPATH *.java
java -cp $CPATH org.junit.runner.JUnitCore TestListExamples

```

--------

Ccommand line that triggers the bug:

`bash test.sh`

--------

What to edit to fix the bug:

Fix the typo in function `merge` (`index2` -> `index1`(line33)) so that it will break the while loop when `!(index1 < list1.size())`.

--------

## Part 2 – Reflection

I think it is pretty useful and cool that I learned how to use `vim` in this course. It is really convenient that now I can edit and run commands in the terminal instead of open an IDE. The java debugger is also helpful and I'm still learning how to use it to find bugs in my code. Compared to test cases and printing out each steps, the java debugger is more intuitive and I does not need to write a bunch of test cases for the code.
