## 9.Concurrency

**Semantica** achieves concurrency through **Multiplex**:

```Semantica

Multiplex tasks||       //vector of tasks

a, b > function1 > tasks|0|     //list of fuctions for each task
i, n > function2 > tasks|1|
...

int i(0)
repeat| !eot        //end of time of execution

tasks|i++|.concur       //running tasks concurrently

|repeat

```

\---