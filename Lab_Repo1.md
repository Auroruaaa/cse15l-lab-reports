# CSE 15L Lab Report 1
*Beijie Cheng | Oct. 4, 2023*

In the first lab report, I will explain the command `cd`, `ls`, `cat`, and provide examples of using these commands to explore their application.


## `cd` : Change Directory

1、 Using the command `cd` with no arguments

  ```
  [user@beijie ~/lecture1]$ cd


  [user@beijie ~]$ 
  ```

  * The directory was initially */home/lecture1/*. After the command `cd`, the directory is changed back to */home/*.

  * This command means going back to the home directory of your computer.
  
  * The output shows that you are in home directory now.

2、 Using the command `cd` with a path to a directory as an argument
   
  ```
  [user@beijie ~/lecture1]$ cd lab1


  [user@beijie ~/lecture1/lab1]$ 
  ```

  * The directory was initially */home/lecture1/*. After the command `cd lab1`, the directory is changed to */home/lecture1/lab1*.

  * This command means moving into the directory with the path going after cd.
  
  * The output shows that you are in directory */home/lecture1/lab1* now.

3、 Using the command `cd` with a path to a file as an argument
   
  ```
  [user@beijie ~/lecture1]$ cd Hello.java


  bash: cd: Hello.java: Not a directory
  ```

  * The directory was initially */home/lecture1/*. After the command `cd Hello.java`, the directory is still the same.
  
  * The output indicated an error that there is not a directory named *Hello.java*. This is because the command `cd` allows user to move bewteen only directories. However, *Hello.java* is a file rather than a directory, thus resulting into an error in the output.

  
## `ls` : List Files

1、 Using the command `ls` with no arguments
   
  ```
  [user@beijie ~/lecture1]$ ls


  Hello.java  lab1
  ```

  * The directory was initially */home/lecture1/*. After the command `ls`, the directory is stil the same.

  * This command `ls` prints out the contents (i.e. files and directories) of the current directory.
  
  * The output shows all the contents in current directory */home/lectuture1*.
    
2、 Using the command `ls` with a path to a directory as an argument
   
  ```
  [user@beijie ~/lecture1]$ ls lab1


  lab_1.java
  ```

  * The directory was initially */home/lecture1/*. After the command `ls lab1`, the directory is still the same.

  * This command lists the contents in directory *lab1*. I also noticed that 1) if the command is `ls /home`, then the ternimal will print out the contents of the home directory; 2) if the command is `ls /lecture2` (a directory that is not the child of current directory), then there will be an error that the terminal has no access to directory *lecture2* (i.e. no such file).
  
  * The output shows all the folders and files under the directory *lab1*.

3、 Using the command `ls` with a path to a file as an argument
   
  ```
  [user@beijie ~/lecture1]$ ls Hello.java


  Hello.java
  ```

  * The directory was initially */home/lecture1/*. After the command `ls Hello.java`, the directory remains the same.

  * Since the pathname is a file, ls displays information about the file according to the requested options.
  
  * The output shows the name of the file.


## `cat` : View or Create A File

1、 Using the command `cat` with no arguments
   
  ```
  [user@beijie ~/lecture1]$ cat



  ```

  * The directory was initially */home/lecture1/*. After the command `cat`, the directory is still */home/lecture1*.

  * This command can view the contents of a file.
  
  * This output is actually not an error. It reads data from standard input and writes them to standard output. You can put a pathname after `cat` to print the contents. 

2、 Using the command `cat` with a path to a directory as an argument
   
  ```
  [user@beijie ~/lecture1]$ cat lab1


  cat: lab1: Is a directory
  ```

  * The directory was initially */home/lecture1/*. After the command `cat lab1`, the directory is still */home/lecture1*.

  * The command means viewing the contents of a file.
  
  * The output is an error, indicating that *lab1* is a directory rather than a file. This error exists because cat can only show contents of a file, and cannot proceed with a directory.

3、 Using the command `cat` with a path to a file as an argument
   
  ```
  [user@beijie ~/lecture1]$ cat Hello.java


  import java.io.IOException;
  import java.nio.charset.StandardCharsets;
  import java.nio.file.Files;
  import java.nio.file.Path;

  public class Hello {
    public static void main(String[] args) throws IOException {
      String content = Files.readString(Path.of(args[0]), StandardCharsets.UTF_8);    
      System.out.println(content);
    }
  }
  ```

  * The directory was initially */home/lecture1/*. After the command `cd Hello.java`, the directory is still the same.

  * This command `cat Hello.java` can print out the content of the file *Hello.java*.
  
  * The output prints all the contents in *Hello.java* and is not an error.



