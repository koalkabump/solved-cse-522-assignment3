Download Link: https://assignmentchef.com/product/solved-cse-522-assignment3
<br>



Lecture 11 describes the problem of concurrent insertion into a binary search tree (BST).   Posted on Piazza is a file ParTreeInsert.java whose main method creates and starts five threads, each of which inserts five random integers into a tree, and finally prints out all values in the tree.   The class Tree in this file defines the standard insert method but the problem of using this method in conjunction with threads is that some of the inserted values get dropped from tree due to improper synchronization – as illustrated in Lecture 11.

A preliminary solution to this problem is to declare insert as a Java ‘synchronized’ method.  Doing so will solve the problem of dropped values, but this solution sacrifices concurrency because values are now inserted sequentially into the tree.




Your task in Part 1 is to write a method in class Tree called insert_par(n) which preserves the basic logic of the standard insert, but permits concurrent insertion of values into the tree, with no dropped values.  Concurrent insertion into disjoint subtrees as well as concurrent insertion at different nodes along any path from the root to a leaf should be allowed.  To meet these objectives:




<ol>

 <li>Do not declare the method insert_par(n) as a synchronized method.</li>

 <li>Define two synchronized methods in class Tree, called lock() and unlock(), using which insert_par(n) can ensure that only one thread at a time is accessing any  Tree</li>

 <li>Call the lock() and unlock() methods from insert_par(n) in such a way that any Tree object is locked for as short a duration as possible.</li>

 <li>Define lock() and unlock() using Java’s wait-notify Hint:  Their definitions are similar to other wait-notify examples discussed in the lectures.</li>

</ol>




Run ParTreeInsert.java replacing the call on insert in class InsertNums by insert_par and proceed as follows:




<ol>

 <li>Check the JIVE object diagram to make sure that it does not have any dropped values, and check the console output to make sure that the printed values are in ascending order.</li>

 <li>Bring up the JIVE Search window, choose ‘Object Created’ option, and enter ‘Tree’ for the class name. There should be 26 entries in the Search Results window for the given test case.</li>

 <li>Step through the search results one by one, observing the object diagram (with the ‘Stacked’ option) at each step, until you locate at an object diagram showing ‘maximal concurrency’, i.e., where there is a maximum number of active threads in disjoint subtrees and also a maximum number of active threads at different nodes along a path in the tree. There could be more than one such diagram; choose any ‘maximal concurrency’ object diagram.</li>

 <li>Save the chosen object diagram from step 3 in a file called png.</li>

</ol>




<strong><em>What to Submit</em></strong><strong>.<em>  </em></strong>Prepare a top-level directory named <em>A3_Part1_UBITId1_UBITId2 </em>if the assignment is done by a team of two students; otherwise, name it as <em>A3_Part1_UBITId</em> if the assignment is done solo.  (Order the <em>UBITId</em>s in alphabetic order, in the former case.)    In this directory, place your

ParTreeInsert.java and A3_obj.png. Compress the directory and submit the compressed file using the submit_cse522 command.  Only one submission per team is required.




<strong><em> </em></strong>

<h1>Part 2: Readers-Writers with Write Priority</h1>




Lecture 12 discusses the Readers-Writers problem, a classic example in the study of concurrency control.   There are two types of concurrent threads, reader threads (readers) and writer threads (writers), and they concurrently access a database.  Readers execute the database ‘read’ operation while writers execute the database ‘write’ operation.   The basic requirement of concurrency control is that a ‘read’ operation may be executed concurrently by two or more readers, but a ‘write’ operation should not be executed concurrently with any ‘read’ or any ‘write’ operation.




An important variant of the basic problem is the Readers-Writers problem with Write Priority.   Here, when a writer tries to access the database and is made to wait because of one or more active readers, all subsequent read requests are delayed until this writer gets to access the database.  Active readers are not pre-empted but are allowed to complete their read operations before the writer begins its operation.   Every waiting writer takes precedence over every waiting reader regardless of the order of their arrival.




Posted on Piazza is a file ReadersWriters.java containing a complete implementation of the Readers-Writers problem with Write Priority.  This program is written with wait-notify constructs.

Your task in Part 2 is to translate all synchronized methods and wait-notify constructs in terms Java Semaphores, using the methodology outlined in Lecture 13.  Name the translated program as RW_Semaphore.java.    In developing your solution:




<ol>

 <li>Use one semaphore for translating synchronized methods.</li>

 <li>Use one semaphore for waiting readers.</li>

 <li>Use one semaphore for waiting writers.</li>

 <li>Implement the notifyAll operation by performing release(s) on the appropriate semaphore.</li>

</ol>




Install the State Diagram plugin posted on Piazza and run RW_Semaphore.java as follows:




<ol>

 <li>Run the program to completion and check that data field in object Database:1 has the value 55555 for the given test case.</li>

 <li>Save the Execution Trace in a file called csv and load this file into the State Diagram. Set the Canvas Dimension as 1200 x 1200 at the bottom of the diagram.</li>

 <li>From the dropdown menu, choose the variables Database:1-&gt;r and Database:1-&gt;w.  Draw the State Diagram and check that the basic requirement of concurrency control for the problem has been met, i.e., in every state of the diagram, the following condition is true:</li>

</ol>

(w = 1 à r = 0) / (r &gt; 0 à w = 0) / (w = 0 / w = 1).

Export the diagram to a file called A3_state1.png.

<ol start="4">

 <li>From the dropdown menu, choose the variables Database:1-&gt;r, Database:1-&gt;w,</li>

</ol>

Database:1-&gt;wr and Database:1-&gt;ww. Draw the State Diagram and check that the

Writers priority condition has been met, i.e., if ww &gt; 0 in some state then either r = 0 in that state or the value of r should monotonically decrease and reach 0 in some future state and should remain at 0 until ww becomes 0 at a subsequent future state.  Export the diagram to a file called A3_state2.png.

<ol start="5">

 <li>Finally, from the dropdown menu choose the variables Database:1-&gt;r, Database:1-&gt;w,  and Database:1-&gt;data. Draw the State Diagram and export it to a file called png.   This diagram also helps you check the Writers priority condition.</li>

</ol>