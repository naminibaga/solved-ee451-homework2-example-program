Download Link: https://assignmentchef.com/product/solved-ee451-homework2-example-program
<br>
<h1></h1>

print msg.c is an example program. You can refer it for thread creation, joining and passing arguments to threads.

To compile it, type: gcc -lrt <strong>-lpthread </strong>-o go print msg.c

To run it, type: ./go

1             Parallel Matrix Multiplication

<h2>1.1           Local Output Variables</h2>

Parallelize the <strong>naive </strong>matrix multiplication which you implemented in PHW 1 using Pthreads. One simple way to parallelize the algorithm is evenly partitioning and distributing the computation works of the elements of output matrix among the threads and letting the threads work independently in parallel. Note, each thread (<em>i,j</em>) is responsible for computing output block <em>C</em>(<em>i,j</em>). For example, assuming the matrix size is <em>n </em>× <em>n </em>and the number of threads is <em>p </em>× <em>p</em>; let thread #(0<em>,</em>0) compute the elements of rows 0 to 1 and columns 0 to the output matrix, thread #(0<em>,</em>1) compute the elements of rows 0 to 1 and columns to <em>frac</em>2<em>np </em>− 1 of the output matrix, and so on.

<ul>

 <li>The matrix initialization is the same as that in PHW 1. The matrix size is 4<em>K </em>× 4<em>K</em>. Print out the execution time and the value of <em>C</em>[100][100] in your program.</li>

 <li>Pass the square root of total number of threads <em>p </em>as a command line parameter [1].</li>

 <li>Report the execution time for <em>p</em>×<em>p </em>= 1 (the serial version you did in PHW1)<em>,</em>4<em>,</em>16<em>,</em>64 and 256. Draw a diagram to show the execution time under various <em>p</em>. An example diagram is shown in Figure 1. Briefly discuss your observation.</li>

 <li>In your report, discuss how you partition the computation works of the elements of the output matrix among the threads.</li>

</ul>

Figure 1: Example diagram

<h2>1.2           Shared Output Variables</h2>

We now used another method as discussed in Lecture 4 slides 35-41 to parallelize the algorithm, where we evenly partition and distribute the computation works of the elements of one input matrix among the threads and letting the threads work in parallel. Note each thread (<em>i,j</em>) accesses and owns input block <em>A</em>(<em>i,j</em>), and is responsible to update all output <em>C</em>(<em>i,k</em>) via matrix multiplication with <em>B</em>(<em>j,k</em>), where <em>k </em>iterates from 1 to <em>p</em>. For example, assuming the matrix size is <em>n </em>× <em>n </em>and the number of threads is <em>p </em>× <em>p</em>; let thread #(0<em>,</em>0) compute the elements of rows 0 to 1 and columns 0 to 1 of the input matrix <em>A </em>multiplied by elements of rows 0 to 1 of the input matrix <em>B </em>(contributes to elements of rows 0 to of the input matrix <em>C</em>), thread #(0<em>,</em>1) compute the elements of rows 0 to 1 and columns  to 1 of the input matrix <em>A </em>multiplied by elements of rows 1 of the input matrix <em>B </em>(contributes to elements of rows 0 to 1 of the input matrix <em>C</em>), and so on. (Hint: You will use mutex in this problem to handle the situation of multiple thread manipulating the same row of output matrix <em>C</em>)

<ul>

 <li>The matrix size is 4<em>K </em>×4<em>K</em>. Print out the execution time and the value of <em>C</em>[100][100] in your program.</li>

 <li>Pass the square root of total number of threads <em>p </em>as a command line parameter [1].</li>

 <li>Report the execution time for <em>p</em>×<em>p </em>= 1 (the serial version you did in PHW1)<em>,</em>4<em>,</em>16<em>,</em>64 and 256. Draw a diagram to show the execution time under various <em>p</em>. An example diagram is shown in Figure 1. Briefly discuss your observation.</li>

 <li>In your report, discuss how you partition the computation works of the elements of the output matrix among the threads.</li>

 <li>In your report, compare the execution time of problem 1.2 with 1.1 and explain any difference.</li>

</ul>

<h1>2             Parallel K-Means</h1>

In PHW 1, you implemented the <em>K</em>-Means algorithm. In this problem, you will need to parallelize your implementation using Pthreads. Let <em>p </em>denote the number of threads you create. The parallel version of <em>K</em>-Means algorithm has the following steps:

<ol>

 <li>Initialize a mean value for each cluster.</li>

 <li>Partition and distribute the data elements among the threads. Each thread is responsible for a subset of data elements.</li>

 <li>Each thread assigns its data elements to the corresponding cluster. Each thread also locally keeps track of the number of data element assigned to each cluster in current iteration and the corresponding sum value. 4. Synchronize the threads.</li>

 <li>Recompute the mean value of each cluster.</li>

 <li>Check convergence; if the algorithm converges, replace the value of each data with the mean value of the cluster which the data belongs to, then terminate the algorithm; otherwise, go to Step 2.</li>

</ol>

In this problem, the input data is the same matrix as in PHW 1 which is stored in the ‘input.raw’; the value of each matrix element ranges from 0 to 255. Thus, the matrix can be displayed as an image. However, we will have <strong>6 </strong>clusters (<em>K</em>=6). The initial mean values for the clusters are 0, 65, 100, 125, 190 and 255, respectively. To simplify the implementation, you do not need check the convergence; run <strong>50 </strong>iterations (Step 2-5) then terminate the algorithm and output the matrix into the file named ‘output.raw’.

<ul>

 <li>Implement a serial version without using Pthreads (No need to submit this program).</li>

 <li>Implement a parallel version using Pthreads. Name the program as p2.c. Pass the number of threads <em>p </em>as a command line parameter</li>

 <li>In your report, you need report the execution time for the <strong>50 </strong>iterations (excluding the read/write time) for <em>p </em>= 4<em>,</em> Compare with the serial version with respect to execution time, discuss your observation.</li>

 <li>Show the image of the output matrix in your report. You can display the output image, ‘output.raw’, using the imageJ [4] software or the given Matlab script file, ‘show raw.m’. If you use ‘show raw.m’, remember to specify the file name in the script.</li>

</ul>