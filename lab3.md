# **Lab Report 3**

**Part 1:**
1. A failure-inducing input for the buggy program, as a JUnit test and any associated code/
```
    @Test
    public void filterRetainsOrderOfInput(){
        StringChecker sc = (s) -> true;
        List<String> inputList = new ArrayList<>();
        inputList.add("A");
        inputList.add("B");
        List<String> outList = ListExamples.filter(inputList, sc);
        assertEquals(2, outList.size());
        assertEquals("A", outList.get(0));
        assertEquals("B", outList.get(1));
    }

```

2. An input that doesn’t induce a failure, as a JUnit test and any associated code
```
    @Test
    public void filterDoesNotIncludeElementsWhereSCReturnsFalse(){
        StringChecker sc = (s) -> false;
        List<String> inputList = new ArrayList<>();
        inputList.add("A");
        inputList.add("B");
        List<String> outList = ListExamples.filter(inputList, sc);
        assertEquals(0, outList.size());
    }
```
3. The symptom, as the output of running the tests
![Image](symtom_lab3.png)

4. The bug, as the before-and-after code change required to fix it
   Before:
```
   static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(0, s);
      }
    }
    return result;
   }
```
  After:
```
    static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(s);
      }
    }
    return result;
  }

```
   
**Part 2:**
I use the "man find" command to look for the find -option that I found here.
- name option:
![Image](-name.png)

- path option:
![Image](-path.png)

- size option:
![Image](-size1.png)
![Image](-size2.png)

- type option:
![Image](-type1.png)
![Image](-type2.png)
