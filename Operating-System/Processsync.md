
Types of Processess

1 Independent  --   When a process Cannot send, receive  not sharing any data with another process  not communicating with any other process are called independent.

2 Cooperating/Cordinating/Communicating --  When a process communicate with other process  it means it affect another process  or can be affected by another process.



When  process  communicate with  other process that process affect other process or can be affected by another process. It means something is shared So Synchronization is Required while Communicating.



Need of Synchronization

    In Communicating Process

Problems without Synchronization

    Loss of Data
    Inconsistency
    Deadlock




Critical Section  (In Simple  Each Process has its  own instruction  when multiple process are communicating with other process that part is critical section . In critical section area Synchronization is required)

 The Critical Section is a code segment where the Shared variable can be accessed



Where Synchronization Required ?

    In Critical Section Area


RACE Condition

    Undesirable Situation

In Simple words There is one Variable  value is 10   2 process are access that variable concurrently   and made modification  the outcome is not same it vary based on preemption (context switching).

Which process completes first the result vary accordingly Thats a Race Condition.




Solution of Critical Section Problem  (How to do Synchronization)


Create one entry section before critical section
Create one exit section after critical section



Requirement of Critical Section Problem
1 Mutual Exclusion  (If one process access critical section  then other process cannot use that critical section)

2 Progress (If no Process in critical section and one process wants to enter into critical section then it should allow)

3 Bounded Waiting (Waiting for Processes should be bounded/limited)



For example If Doctor is treating one Patient  other patient cannot allow to enter doctor room  the assitant of doctor ensure no one enter the doctor room.

Once doctor is free then assistant allow other patient

Now If one patient came for one problem and got doctor  now patient is getting treated for another multiple probelm . The patient  who are waiting outside waiting time will increase It should be bounded
If patient came for one problem only that problem is treated then patient should came outside so other will get change and that patient need to wait in queue for another problem


Code base Solution  : Using Lock

boolean lock = false;




while(true)
{

    while(lock); // it means empty block
        lock=true;

        //Critical Section

        lock=false;


}


In above code when 2 process are trying to access critical section and IF the process preemtive after while(lock) another process access critical section and if that preemtive previous process also in critical section So 2 process are in Critical section
This doesn't satisfy the mutual exclusion.


Problem is  lock variable is shared  so thats why mutual exclusion will not work



Code base Solution  : Using Turn

Process 0
int turn = 0;

while(true){

    while(turn!=0);
        //Critical section
    turn = 1;

}


Process 1
int turn = 1;

while(true){

    while(turn!=1);
        //Critical section
    turn = 0;

}



In this Solution Mutual exclusion is satisfy but process 1 cannot make a progress if process1 want to enter first then this solution will not work



Synchronization Hardware (Instruction support by CPU) This is only applicable at Kernel Level .

    TestAndSet()
    Swap





Synchronization Tool

    Semaphore
    Monitor


Using these tool Processess can  used this to implement Synchronization.


Semaphore
    Integer Value which can be accessed using following functions only
        wait()/degrade()/down()
        signal()/upgrade()/up()

    The above both function are atomic  if any function is stopped in between it starts from starting only because of atomic.

    Yes we can stopped the wait() and signal()  in between due to any reason  but these function are starting from start when it resumes.

    wait(S)
    {
        while(S<=0); //  if s=0 or s is less than 0  this will stuck condition will true  not able to execute  further that is called busy waiting
        S--;
    }


    signal(S)
    {
        S++;
    }




For Entry  in critical section we use wait()   because it gives mutual exclusion

For exit in critical section we use signal()

Types of Semaphore

    Binary Semaphore     only 2 value  0,1
    Counting Semaphore  unlimited value (only integer any range)

    Binary Semaphore  It is used to implement the solution od critical section problems with multiple processes to provide mutual exclusion

    Counting Semphore  we will use to control the access to a resources that has multiple instances


Mutual Exclusion means only one process enter into critical section.


    S = 1

    while(True)
    {
        wait(S)

        //Critical Section Area


        signal(S)
    }



 wait(S)
    {
        while(S<=0); //  if s=0 or s is less than 0  this will stuck condition will true  not able to execute  further that is called busy waiting
        S--;
    }



The execution of wait(S) is Atomic Let think if process 0 came and preemption happen  after while inside wait(S) when this process0 resume after process 1 ends process 0 will not resume from where it preemptive it start from starting  because it's is Atomic



Characteristics of Semaphore

Used to provide mutual excusion - binary
Used to control access to resources - counting
Solution using semaphore can lead to deadlock and starvation







Reader-Writer Problem

Consider the situation where we have file shared between many people

If one of the people tries editing the file, no other person should be reading or writing the same time, Otherwise changes will not be visible to him/her

If some person is reading the file  then other may read the file at a same time.



Reader - Writer Problem Solution

If writer is accessing the file , then all other reader and writer will be blocked
If any reader is reading then other reader can read but writer will be blocked.


Variables :

    mutex: Binary Semaphore to provide mutual exclusion
    wrt: Binary Semaphore to restrict reader and writers if writing is going on
    readcount: Integer variable,denotes number of active readers


mutex: 1
wrt:1
readcount:0





Deadlock

When 2 or more waiting for an event and that event is never going to happen


Necessary Condition for deadlock when all of the following condition are statisfies

1 Mutual Exclusion - when one process using a resource, then other process cannot use it
2 Hold & Wait  - Each deadlocked  process should Hold atleast  one resource and waiting for another resource
3 No preemption - No one can forcefully preemption of resources (Resource Preemption which they are holding)
4 Circular Wait - All the process are waiting for resources


For Example Process p1 Holds  Keyboard and waiting for harddisk
Process p2 holds harddisk and waiting for printer
Process p3 holds printer and waiting for keyboard


The above example is DEADLOCK




Make Sure that deadlock never occur
    Prevent the System from deadlock or avoid deadlock
    Allow Deadlock ,prevent and recover
    Prevent that there is no deadlock (Operating System)




DeadLock Prevention

 For prevention dissatify atleast one of the deadlock condition

 Preventing Mutual Exclusion
    Have enough resources to provide simultaneous execution - difficult there are so many resources and process
    Make all the process independent  -- Not possible because independent process need more resources


Preventing Hold & Wait

    A process will either hold or wait but not together
        if all the resources are available then acquire or else wait for all  but there is a situation  some resources are not available it lead to starvation

        If process trying to aquire a resource which is not available, while holding some resources then process will release all allocated resources
        If a process holds resources but not using them there there will be poor utilization of resources.


Preventing No Preemption

    If OS preemptive resources  if resources held by some process get preemtive and provide to other resource
    But All resources are not able to preemtive  like memory

Prevention Circular Wait

All the resources have be given a sequence unique number
Any process while holding any resource Ri can request for Rj only when j>i
If a process is holding a resource Ri and wants another resource Rj when j<i Then process will have to release Ri and will have to aquire Rj first.



Deadlock Avoid

    The OS tries to keep in Safe State

    The request for any resource will be grant if the resulting state of the system doesn't cause deadlock in the system.


Banker's Algorithm
    The banker algorithms is a resource allocation and deadlock avoidance algorithm that test for safety



















