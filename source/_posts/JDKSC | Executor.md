---
title: Java Doc - Executor
date: 2023-06-09 09:19
---
```JSON
{
    "author": "Doug Lea",
    "editor": "Sbriny"
},
{
    "explicitly creating threads":"显式创建线程",
    "asynchronous execution":"异步执行",
    "caller's thread":"调用者线程",
    "composite executor":"复合型执行器"
}
```
<!--more-->
```Java
/*
An object that executes submitted Runnable tasks. **This interface provides a way of decoupling task submission from the mechanics of how each task will be run, including details of thread use, schefuling, etc.** An executor is normally used instead of explicity creating threads. For example, rather than invoking new Thread(new RunnableTask()).start() for each of a set of tasks.
You might use:
Executor executor=anExecutorMethod();
executor.execute(new RunnableTask1());
executor.execute(new RunnableTask2());
However, the Executor interface does not strictly require that execution be asynchronous. In the simplest case, an executor can run the submitted task immediately in the caller's thread:
class DirectExecutor implement Executor{
    public void execute(Runnable r){
        r.run();
    }
}
More typically, tasks are executed in some thread other than the caller's thread. The executor below spawns a new thread for each task.
class ThreadPerTaskExecutor implements Executor{
    public void execute(Runnable r){
        new Thread(r).start();
    }
}
Many Executor implementations impose sme sort of limitation on how and when tasks are scheduled. **The executor below serializes the submission of tasks to a second executor, illustrarting a composite executor.**
class SerialExecutor implements Executor{
    final Queue<Runnable> tasks=new ArrayDeque<>();
    final Executor executor;
    Runnable active;
    SerialExecutor(Executor executor){
        this.executor=executor;
    }
    public synchronized void execute(Runnable r){
        tasks.add(()->{
            try{
                r.run()
            }
            finally{
                scheduleNext();
            }
        });
        if(active==null){
            scheduleNext();
        }
    }
    protected synchronized void scheduleNext(){
        if((active=task.poll())!=null){
            executor.execute(active);
        }
    }
}
The Executor implementations provided in this package implement ExecutorService, which is a more extensive interface. The ThreadPoolExecutor class provides an extensible thread pool implementation. The Executors class provides convenient factory methods for these Executors.
Memory consistency effects: 
Actions in a thread prior to submitting a Runnable object to an Executr package-summary.html#MemoryVisibility happen-before its execution begins, perhaps in another thread.
*/
```