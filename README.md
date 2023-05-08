Download Link: https://assignmentchef.com/product/solved-spl181-assignment-1
<br>
The objective of this assignment is to design an object-oriented system and gain implementation experience in C++ while using classes, standard data structures and unique C++ properties such as the “Rule of 5”. You will learn how to handle memory in C++ and avoid memory leaks. The resulting program must be as efficient as possible.

<h1>1         Assignment Definition</h1>

In this assignment you will write a C++ program that simulates a naïve hierarchical computer file system.

To communicate with the file system, you will implement a command-line/terminal that enables the user to create/delete files/folders, print the contents of a directory etc.

The file system consists of a root directory (“/”) and optionally other files and directories underneath.

The program has a global variable called verbose to control its output. See the verbose command for details.

Your program will be executed in the following way: “./bin/fs”. Your program must not receive any external arguments.

3.1 Important terms

<ul>

 <li><strong>Root directory</strong> – The first or top-most directory in the file hierarchy (“/”).</li>

 <li><strong>Working directory</strong> – Current directory, see relative path for its purpose.</li>

 <li><strong>Absolute path</strong> – The path to a specific directory/file starting from the root directory (“/”). E.g. “/dir1/dir2/file1”</li>

 <li><strong>Relative path</strong> – The path to a specific directory/file starting from working directory. E.g. if the working directory is “/dir1/dir2”, the relative path “dir3” is the absolute path “/dir1/dir2/dir3”.</li>

 <li><strong>..</strong> – The parent directory of the working directory. This is a relative path by definition. E.g.</li>

</ul>

../../dir1 means to look for dir1 under the parent of the parent of the working directory.

<ul>

 <li><strong>Path</strong> – Can be either absolute path or relative path.</li>

</ul>

3.2 General instructions

<ul>

 <li>Class with resources must implement the rule of five.</li>

 <li>The names of files/directories consist of letters (a-z,A-Z) and digits only (0-9), in particular no spaces are allowed.</li>

 <li>File/Directory names are unique within the containing directory.</li>

 <li>You may not add constructors nor global variables nor any public/protected data members.</li>

</ul>

See section 4 for more details.

<ul>

 <li>You may not add any global variables.</li>

 <li>It is highly recommended that you first implement the objects of Files.h before implementing any of the commands.h objects.</li>

</ul>




3.3 Classes

<strong>BaseFile</strong> – This is an abstract class for File and Directory.

<strong>File</strong> – Inherits from BaseFile. This class represents a single file in the system. Each file has a name, a size and a parent (the containing directory).

<strong>Directory</strong> – Inherits from BaseFile. This class represents a single folder in the system. Each directory has a name and a parent and contains a list of files and directories. The parent of the root directory is NULL. The size of a directory is the sum of the sizes of all its files and directories recursively.

<strong>BaseCommand </strong>– This is an abstract class for the different command classes

<strong>Commands implementation</strong> – each of the commands below must be implemented as a class that inherits from BaseCommand. The name of each command’s class must be the name of the command (first letter uppercase) followed by “Command”.

For example: “class HistoryCommand: public BaseCommand {…};”

<strong>ErrorCommand</strong> – This is a special command class that represents an unknown command, that is, a command that is not listed in the commands list below. It also inherits from BaseCommand.

When executed it prints: “&lt;<em>the-input-command</em>&gt;: Unknown command” Example: If user enters “find myfile.txt” it will print “find: Unknown command” <strong>FileSystem</strong> – Holds the root directory and the working directory.

<strong>Environment</strong> – Holds the file-system and the entire history of executed commands including duplicates, ErrorCommands and the HistoryCommands (see <strong>history</strong> in the command section

below)

<strong> </strong>

3.4 Commands

Below is the list of the commands you are required to support.

Please be aware for the following denotation:

[..] –   These brackets denote that the argument is optional. Example: [-s] &lt;..&gt; – These brackets denote the expectation of an argument.

Example: &lt;path&gt; should be replaced by any legal path (example: dir1dir2).

|      – “|” denotes OR. Example: on|off, meaning either on or off.




<u>The commands:</u>

<ul>

 <li><strong>pwd</strong>: print working directory path.</li>

 <li><strong>cd</strong>: Change the current directory.</li>

</ul>

Syntax: cd &lt;<em>path</em>&gt; – Change current directory to be &lt;<em>path</em>&gt;

If &lt;<em>path</em>&gt; doesn’t exist print out “The system cannot find the path specified” Example: cd .. –  Change to the parent directory

<ul>

 <li><strong>ls</strong>: Display the list of files and subdirectories of a directory. <strong>The list has to be sorted alphabetically by default</strong>. For each file/directory print out in a new line its type</li>

</ul>

(“FILE”/”DIR”), its name and its size (See class Directory for directory size) separated by a tab

(t).

For example:

DIR             dir1      750

FILE            file1     1000




Syntax: ls [-s] &lt;<em>path</em>&gt; – Display the list of files and subdirectories in &lt;<em>path</em>&gt;              ls [-s] – Display the list of files and subdirectories in the working directory

–s – Sort by size, from smaller to larger. If two or more files have the same size, sort them

alphabetically.

If &lt;<em>path</em>&gt; doesn’t exist print out “The system cannot find the path specified”

<ul>

 <li><strong>mkdir</strong> – Create a new directory. If needed, create intermediate directories in the path.</li>

</ul>

Syntax: mkdir &lt;<em>path</em>&gt;

If &lt;<em>path</em>&gt; exists print out “The directory already exists” Examples:

“mkdir /newDir”  – If newDir doesn’t exist in the root directory, creates it in the root directory.

“mkdir newDir”  – If newDir doesn’t exist in the working directory, creates it in the working directory.

“mkdir /d1/d2/d3” – assume d1 exists and d2 does not exist in d1 directory then it is the same as:  cd /d1 mkdir d2 cd d2 mkdir d3 cd /

<ul>

 <li><strong>mkfile</strong> – Create a new file. The path of the file must exists</li>

</ul>

Syntax: mkfile &lt;<em>path/filename</em>&gt; &lt;<em>size</em>&gt;

If &lt;<em>path</em>&gt; doesn’t exist print out “The system cannot find the path specified”

If &lt;<em>path/filename</em>&gt; exists  print out “File already exists”

Example: “mkfile /dir1/dir2/mynewfile 1000” will create mynewfile in /dir1/dir2, the size of the file will be 1000.

<ul>

 <li><strong>cp </strong>– Copy a file or directory to a destination. Syntax: cp &lt;<em>source-path</em>&gt; &lt;<em>destination-path</em>&gt; <em>source-path</em> may be either a file or a directory, <em>destination-path</em> is a directory.</li>

</ul>

If either file/directory/destination doesn’t exist print out “No such file or directory”

Example: “cp dir1/dir2/dir3/file1 dir4/dir5” will copy file1 to dir4/dir5 Example: “cp dir4 dir6” will copy dir4 (recursively) under dir6.

<ul>

 <li><strong>mv </strong>– Move a file or directory to a new destination. Syntax: mv &lt;<em>source-path/file-name</em>&gt; &lt;<em>destination-path</em>&gt; <em>source-path</em> may be either a file or a directory, <em>destination-path</em> is a directory.  If either source-path/file-name/destination-path doesn’t exist print out “No such file or directory”.</li>

</ul>

Working-directory nor its parents nor the root-directory can’t be moved. In such a case print out “Can’t move directory”.

Example: “mv dir1/dir2/dir3/file1 dir4/dir5” will move file1 to dir4/dir5 Example: “mv dir4 dir6” will move dir4 to be under dir6.

<ul>

 <li><strong>rename </strong>– Rename a file or a directory.</li>

</ul>

Syntax: rename <em>&lt;path</em>/<em>old-name</em>&gt; &lt;<em>new-name</em>&gt;

If either path/old-name doesn’t exist print out “No such file or directory”.

If old-name is the working-directory print out “Can’t rename the working directory” and do not rename.

Example: “rename dir1/dir2/file1 file2” will result in “dir1/dir2/file2”.

<ul>

 <li><strong>rm</strong> – Remove (delete) a file or a directory. If the argument is a directory remove it recursively.</li>

</ul>

Syntax: rm &lt;<em>path</em>&gt;

If &lt;<em>path</em>&gt; doesn’t exist print out “No such file or directory”.

Working-directory nor the root-directory can’t be removed. In such a case print out “Can’t remove directory”.

<ul>

 <li><strong>history </strong>– Print out the entire list of the executed commands sorted from the oldest to the newest, excluding <u>current</u> history command. It must print all the commands entered by the user including duplicates, ErrorCommands and <u>previous</u> Each command will be numbered (0 for the oldest command) and printed in a single row. It will be printed out in the following format: “&lt;<em>index</em>&gt;tab&lt;<em>the command</em>&gt; (as it was entered originally including its full arguments list)”. If the list is empty print nothing.</li>

</ul>

Syntax: history

Example output:

<ul>

 <li>ls</li>

 <li>pwd</li>

</ul>

<ul>

 <li><strong>verbose</strong> – Set the verbose variable as follows:

  <ul>

   <li>– verbose off (i.e. do not print 1, 2 or 3 below).</li>

   <li>– Print a message in a new line each time entering a rule-of-five function. The message must be the signature of the function in the format:</li>

  </ul></li>

</ul>

“return-type Class-Name:: Function-Name(full-argument-list)”

Example:  “MyClass &amp;MyClass::operator=(const MyClass &amp;mc)”

<ul>

 <li>– Echo/Print the full input command (with its arguments) to the screen followed by a new line.</li>

 <li>– Execute 1 and 2.</li>

</ul>

Syntax: verbose &lt;<em>0|1|2|3</em>&gt;

If the argument is different from either 0, 1, 2 or 3, print out: “Wrong verbose input”.

<ul>

 <li><strong>exec<em> – </em></strong>Executes a command from history.</li>

</ul>

Syntax: exec &lt;<em>command-number</em>&gt;

If &lt;command-number&gt; doesn’t exist print out “Command not found”.

Example:<strong> “</strong>exec 24” will execute command number 24 as numbered in the history command

3.5 The Program flow

Once the program starts, it prints out a prompt – the working directory followed by a “&gt; ” (No new line).  Then it waits for the user to enter a command and executes it. After each executed command it prints again the prompt and waits for the next command in a loop. The program ends when the user enters “exit” at the command line.

You may assume that the <u>number and the type</u> of arguments for each command is legal.

<h1>2         Provided files</h1>

The following files will be provided for you on the assignment homepage:

Commands.h

Environment.h

Files.h

FileSystem.h

GlobalVariables.h

GlobalVariables.cpp

Main.cpp

You are required to implement the supplied functions and to add the Rule-of-five functions as needed.

All the functions that are declared in the provided headers must be implemented <strong><u>correctly</u></strong>, i.e. they should perform their appropriate purpose according to their name and their signature.

<strong>Keep in mind that if a class has resources, ALL 5 rules have to be implemented even if you don’t use them in your code. Do not add unnecessary Rule-of-five functions to classes that do not have resources.  </strong>

You are <strong>NOT ALLOWED</strong> to modify the signature (the declaration) of any of the supplied functions. We will use these functions to test your code, therefore any attempt to change their declaration might result in a compilation error and a major deduction of your grade. You are also <strong>NOT ALLOWED</strong> to add constructors, nor public/protected data members.

You also <strong>must not</strong> add any global variables to the program. The only allowed global variable is verbose which is already defined.

It is strongly recommended to test the correctness of all the public functions using your own external program (another “main(..)” function). Our test will include such a testing.

<h1>3         Examples</h1>

See assignment page for input and output examples.

In order to run the examples with your program use the following syntax: ./bin/fs &lt; input-file.txt