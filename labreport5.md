# Christopher Schrader - Lab Report 5

# Part 1

(Note that this code is from Lab 7 that I modified to break)

## 1. Edstem post

Hello class,

I recently was developing a merge function where two Lists are taken as inputs to my merge function, and a resulting single List that is composed of the two input Lists merged in alphabetical order is returned.
I ran my code by running `bash test.sh` that compiles my code and runs my JUnit test file, and it passed one test, but it does not pass the second test.

Test that passes:

Input Lists: `["a", "b", "c"]` and `["c", "d", "e"]`
Correct list returned and expected: `["a", "b", "c", "c", "d", "e"]`

Test that fails:

Input Lists: `["x", "y"]` and `["a", "b"]`
Expected list: `["a", "b", "x", "y"]`
Based on the output from my JUnit test, I think that my merge function is returning this wrong merged List as this, since it says it expected a 'b' but found an 'a':
Actual list returned: `["a", "a", "x", "y"]`

Based on the two different tests that worked and didn't work, I sense that it has something to do with not going past the 'a' in my second input List.

Running my code with `bash test.sh` and output:

![img](lab5_1.png)

My merge code:

```
import java.util.ArrayList;
import java.util.List;

interface StringChecker { boolean checkString(String s); }

class ListExamples {

  // Returns a new list that has all the elements of the input list for which
  // the StringChecker returns true, and not the elements that return false, in
  // the same order they appeared in the input list;
  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(s);
      }
    }
    return result;
  }


  // Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
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
        index1 += 1;
      }
    }
    while(index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      // change index1 below to index2 to fix test
      index2 += 1;
    }
    return result;
  }


}

```

Any ideas?

## 2. TA Response

Hello,

It looks like, yes, your code is not moving past the "a" String item in your second input list. How are you handling moving to the next element in a list once you've added one? Based on your input and output, it tells me that some index is not being incremented properly. Maybe try examining this part of your code?

## 3. 

Hi,

Thank you, that was the problem. I was improperly incrementing the index of index1 and not index2 once we merged an item from my second List to the merged List.

Bug in code:
