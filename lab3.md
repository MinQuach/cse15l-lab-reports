# **Lab Report 3**

**Part 1:**

1. A failure-inducing input for the buggy program, as a JUnit test and any associated code
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

    ![Image](symptom_lab3.png)

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
Explanation: The "0" in the "add" method ```result.add(0, s)``` indicates that "s" will always be substituted to index 0 and replace the old string at index 0, instead of being appended to the end of the list. By removing "0", we now use the "add" method to append "s".

**Part 2:**
I use the "man find" command to look for the find -option that I found here.
- iname option: perform a case-insensitive search. This option is useful when you can't remember the exact name of the file. 
```
    find ./technical/biomed/ -iname "*rr*txt"
```
This command will find files that have "rr" in the filename or have a similar filename with "rr.txt" in the ./technical/biomed/ directory. Like "Rr123.txt".
```
    find . -iname "*14*txt"
```
This command will find files that have "14" in the filename or have a similar filename with "14.txt" in the current working directory. Like "abc147.txt".
Source: [Link](https://www.redhat.com/sysadmin/linux-find-command)

- atime option: search for files based on their last access time. This kind of command can be useful for identifying files that haven't been accessed in a long time. 
```
    find ./technical/biomed/ -atime +180
```
This command will search for files in the ./technical/biomed/ directory that have not been accessed in the last 180 days.
```
    find ./technical/biomed/ -atime -90
```
This command will find and display files in the current directory that have been accessed within the last 90 days.
Source: [Link](https://geekflare.com/how-to-use-find-command-in-linux/)

- size option: search for files based on their size. This option is used for identifying and listing files based on their sizes, allowing you to manage or analyze files based on their storage requirements.
```
    find ./technical/ -size +100M
```
This command will find and display files in the ./technical/ directory that are larger than 100 megabytes.
```
    find . -size -1G
```
This command will find and display files in the current directory that are smaller than 1 gigabyte.
Source: [Link](https://linuxconfig.org/how-to-use-find-command-to-search-for-files-based-on-file-size)

- mtime option: search for files based on their last modification time. This is useful for identifying and listing files that have been modified recently, allowing you to manage or analyze files based on their modification times.
```
    find ~ -mtime -30
```
This command will find and display files in the home directory that have been modified within the last 30 days.
```
    find ./technical/plos/ -mtime -60
```
This command will find and display files in the ./technical/plos/ directory that have been modified within the last 60 days.
Source: [Link](https://opensource.com/article/21/9/linux-find-command)
