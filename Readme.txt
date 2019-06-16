Akanksha Mahajan
Student ID : 112074564
Course :  CSE535(Fall 2018) Asynchronous Systems
HomeWork Assignment 4

In this assignment correctness and performance are tested on the 2 Paxos:
1) Basic Paxos
2) Basic Paxos with preemption


Ques1 and Ques2 have been explained in pdf named 112074564_sol.pdf

Ques 3 : Meassure the correctness and performance of different versions of paxos

Command to run :  
python.exe -m da main.da p a l n r d w tp tl
where 
"p", "a", "l" are the number of proposers, acceptors, and learners, respectively,
"n" is the number of repetitions for each run,
"r" is the message loss rate, between 0 for 0% loss and 1 for 100% loss,
"d" is the message delay, up to the number of seconds specified,
"w" is the wait time, in seconds, before trying a new round,
"tp" and "tl" are the timeout, in seconds, by proposers and learners, respectively, when timeout is used.


For correctness:
	I passed the learners value to my monitor process and monitor appends that value in a learner set. 
1) For agreement :
	When monitor gets results from all learners it checks if size of set is one. It means all learners have learned only one value. Hence, they are in agremeent
2) For validity :
	All proposers sends the value v that they have proposed to monitor and monitor stores that value in a set. When all learners have learnt the value,
	if values learnt are subset of proposed values. (All values learned by learners have been proposed by proposers and are not arbitary.)
3) For termination :
	Monitor checks if any learner has learnt any value. It means program reached to a consensus. So, It prints termination is successful.
        Otherwise termination was because of timeout and no consensus has been reached.

I have printed the correctness results on the screen itself.
Note : When delay time and message loss is increased, consensus is not achieved. Because of message drops and delay in response, no consensus is reached.

For performance:
The results of plots will be saved at the current_path/loss_results/, current_path/delay_results and current_path/wait_results separately.

For parameter r, my program will run r/5, r*2/5, r*3/5, r*4/5 and r respectively.
Note that during this round, the delay time is fixed as d/5 and wait time is fixed as w/5 second otherwise consensus is never reached.
Also minimum value of loss rate should be 0.5,
                       message delay is 5 sec
		       wait time is 5 sec

I have used random function to calculate the message loss values and message delay between 0 to specified value. If message loss r/4 then it can randomly loose
messages between 0 to r/4. I have dropping messages at proposer side other if message at acceptor side is lost then consensus is never achieved.

First I have kept wait time and message delay fixed. If message loss is 0.5 then i run nrepititions for first 0.1 then for 0.2, then for 0.3 upto 0.5
(i.e for 5 values of message loss). Then I calculate the average time, cpu time of each message loss rate over nrepititions keeping other two fixed.
Then I plot the graph of varying message loss with the time (cpu time, elapsed time on x axis) for both programs in same plot. 



Plot is saved in current_path/loss_results/
Then I perform this with changing message delay and keeping wait time and message loss fixed. Same as for wait time also.

All results of performance are saved in current_path/Performance.txt
In the file I am printing the Average CPU time, Average Elapsed and Standard deviation of CPU time and ELapsed Time

Analysis :
cpu time for both program is nearly equal in all cases
For Message loss : As message loss increase, basic paxos takes more elapsed time whereas preempt paxos performs better and its elapsed time is nearly equal to cpu time.
		   whereas for lower message loss values, preempt paxos elapsed time is more than basic paxos.

For Message delay : As message delays increases, basic paxos takes more elapsed time whereas preempt paxos elapsed time is less.
	           whereas for lower message delay values, preempt paxos elapsed time is more than basic paxos.

For Wait time : For lower wait delays, both programs have equal elapsed time. But as wait increases, preempt paxos performs better and its elapsed time is 
		nearly equal to cpu time whereas 


 



