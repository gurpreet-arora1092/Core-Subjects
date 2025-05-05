
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