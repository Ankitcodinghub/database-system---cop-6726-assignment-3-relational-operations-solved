# database-system---cop-6726-assignment-3-relational-operations-solved
**TO GET THIS SOLUTION VISIT:** [Database-SysteM – COP 6726 Assignment 3: Relational Operations Solved](https://www.ankitcodinghub.com/product/database-system-cop-6726-assignment-3-relational-operations-solved/)


---

📩 **If you need this solution or have special requests:** **Email:** ankitcoding@gmail.com  
📱 **WhatsApp:** +1 419 877 7882  
📄 **Get a quote instantly using this form:** [Ask Homework Questions](https://www.ankitcodinghub.com/services/ask-homework-questions/)

*We deliver fast, professional, and affordable academic help.*

---

<h2>Description</h2>



<div class="kk-star-ratings kksr-auto kksr-align-center kksr-valign-top" data-payload="{&quot;align&quot;:&quot;center&quot;,&quot;id&quot;:&quot;110627&quot;,&quot;slug&quot;:&quot;default&quot;,&quot;valign&quot;:&quot;top&quot;,&quot;ignore&quot;:&quot;&quot;,&quot;reference&quot;:&quot;auto&quot;,&quot;class&quot;:&quot;&quot;,&quot;count&quot;:&quot;1&quot;,&quot;legendonly&quot;:&quot;&quot;,&quot;readonly&quot;:&quot;&quot;,&quot;score&quot;:&quot;5&quot;,&quot;starsonly&quot;:&quot;&quot;,&quot;best&quot;:&quot;5&quot;,&quot;gap&quot;:&quot;4&quot;,&quot;greet&quot;:&quot;Rate this product&quot;,&quot;legend&quot;:&quot;5\/5 - (1 vote)&quot;,&quot;size&quot;:&quot;24&quot;,&quot;title&quot;:&quot;Database-SysteM - COP 6726 Assignment 3: Relational Operations Solved&quot;,&quot;width&quot;:&quot;138&quot;,&quot;_legend&quot;:&quot;{score}\/{best} - ({count} {votes})&quot;,&quot;font_factor&quot;:&quot;1.25&quot;}">

<div class="kksr-stars">

<div class="kksr-stars-inactive">
            <div class="kksr-star" data-star="1" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="2" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="3" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="4" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="5" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>

<div class="kksr-stars-active" style="width: 138px;">
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>
</div>


<div class="kksr-legend" style="font-size: 19.2px;">
            5/5 - (1 vote)    </div>
    </div>
In this assignment, your task is to implement a set of relational operations, specifically:

SelectPipe, SelectFile, Project, Join, DuplicateRemoval, Sum,

GroupBy, and WriteOut. These operations will all be encapsulated within classes that are derived from the following, virtual base class:

class RelationalOp { public:

//blocks the caller until the particular relational operator

//has run to completion virtual void WaitUntilDone () = 0;

//tells how much internal memory the operation can use virtual void Use_n_Pages (int n) = 0;

};

With a couple of exceptions, operations always get their data from input pipes and put the result of the operation into an output pipe. When someone wants to use one of the relational operators, they just create an instance of the operator that they want. Then they call the Run operation on the operator that they are using (Run is implemented by each derived class; see below). The Run operation sets up the operator by causing the operator to create any internal data structures it needs, and then Run it spawns a thread that is internal to the relational operation and actually does the work. Once the thread has been created and is ready to go, Run returns and the operation does its work in a non-blocking fashion. After the operation has been started up, the caller can call WaitUntilDone, which will block until the operation finishes and the thread inside of the operation has been destroyed. An operation knows that it finishes when it has finished processing all of the tuples that came through its input pipe (or pipes). Before an operation finishes, it should always shut down its output pipe.

Simple enough, right? Now, one at a time we consider each of the operations that are derived from this base class.

class SelectPipe : public RelationalOp { public:

void Run (Pipe &amp;inPipe, Pipe &amp;outPipe, CNF &amp;selOp, Record &amp;literal);

}

SelectPipe takes two pipes as input: an input pipe and an output pipe. It also takes a CNF. It simply applies that CNF to every tuple that comes through the pipe, and every tuple that is accepted is stuffed into the output pipe.

class SelectFile : public RelationalOp { public:

void Run (DBFile &amp;inFile, Pipe &amp;outPipe, CNF &amp;selOp, Record &amp;literal);

}

SelectFile takes a DBFile and a pipe as input. You can assume that this file is all set up; it has been opened and is ready to go. It also takes a CNF. It then performs a

scan of the underlying file, and for every tuple accepted by the CNF, it stuffs the tuple into the pipe as output. The DBFile should not be closed by the SelectFile class; that is the job of the caller.

class Project : public RelationalOp { public:

void Run (Pipe &amp;inPipe, Pipe &amp;outPipe, int *keepMe, int numAttsInput, int numAttsOutput); }

Project takes an input pipe and an output pipe as input. It also takes an array of integers keepMe as well as the number of attributes for the records coming through the input pipe and the number of attributes to keep from those input records. The array of integers tells Project which attributes to keep from the input records, and which order to put them in. So, for example, say that the array keepMe had the values [3, 5, 7, 1]. This means that Project should take the third attribute from every input record and treat it as the first attribute of those records that it puts into the output pipe. Project should take the fifth attribute from every input record and treat it as the second attribute of every record that it puts into the output pipe. The seventh input attribute becomes the third. And so on.

class Join : public RelationalOp { public:

void Run (Pipe &amp;inPipeL, Pipe &amp;inPipeR, Pipe &amp;outPipe, CNF &amp;selOp,

Record &amp;literal);

}

class DuplicateRemoval : public RelationalOp { public:

void Run (Pipe &amp;inPipe, Pipe &amp;outPipe, Schema &amp;mySchema); }

DuplicateRemoval takes an input pipe, an output pipe, as well as the schema for the tuples coming through the input pipe, and does a duplicate removal. That is, everything that comes through the output pipe will be distinct. It will use the BigQ class to do the duplicate removal. The OrderMaker that will be used by the BigQ (which you’ll need to write some code to create) will simply list all of the attributes from the input tuples.

class Sum : public RelationalOp { public:

void Run (Pipe &amp;inPipe, Pipe &amp;outPipe, Function &amp;computeMe); }

Sum computes the SUM SQL aggregate function over the input pipe, and puts a single tuple into the output pipe that has the sum. The function over each tuple (for example:

(l_extendedprice*(1-l_discount)) in the case of the TPC-H schema) that is summed is stored in an instance of the Function class that is also passed to Sum as an argument (the Function class is included in the project tar file).

class GroupBy : public RelationalOp { public:

void Run (Pipe &amp;inPipe, Pipe &amp;outPipe, OrderMaker &amp;groupAtts, Function &amp;computeMe);

}

GroupBy is a lot like Sum, except that it does grouping, and then puts one sum into the output pipe for each group. Every tuple put into the output pipe has a sum as the first attribute, followed by the values for each of the grouping attributes as the remainder of the attributes. The grouping is specified using an instance of the OrderMaker class that is passed in. The sum to compute is given in an instance of the Function class.

class WriteOut : public RelationalOp { public:

void Run (Pipe &amp;inPipe, FILE *outFile, Schema &amp;mySchema); }

WriteOut accepts an input pipe, a schema, and a FILE*, and uses the schema to write text version of the output records to the file.

What To Turn In:

a) All code needed to compile test.cc and a2test.cc

b) Create 4 GTests for any of the methods you wrote. Turn in your GTest code.

c) In a Bash shell, using the .bin files generated from tpch-dbgen with the option -s 1 (1GB files) run the test cases script with the following command:

./runTestCases.sh

The script generates a file called output1.txt. Turn in output1.txt along with your code. If you wrote your code in Rust or are running on a Windows machine, change the script as needed.

2. Your report as a PDF file that includes:

a) Group member names

b) Include instructions on how to compile and run your code as well as a brief explanation of each method you wrote and how it works.

c) A screen shot of output1.txt generated from your code.

d) Screen shots of GTest results that match results generated by your code.

e) If you had a problem with the code or found a bug that you think would be useful for future classes to know about, list the bug you found and what you did to fix it.

Grading:

Graded out of 100 points.

+20 Gtests

+50 points for correct output from runTestCases.sh

+30 report
