A Future represents the result of an asynchronous computation. Methods are provided to check if the computation is complete, to wait for its completion, and to retrieve the result of the computation. The result can only be retrieved using method get when the computation has completed, blocking if necessary until it is ready. Additional methods are provided to determine if the task completed normally or was concelled. once a computation has completed, the computation cannot be cancelled. If you would like to use a Future for the aske of cancellability but not provide a usable result , you can declare types of the form Future and return null as a result of the underlying task.
``` Java
interface ArchiveSeacher {String search(String target);}
class App {
    ExecutorServie executor=...;
    ArchiveSearcher searcher=...;
    void showSearch(String target) throws InterruptedException {
        Callable<String> task=()->searcher.search(target);
        Future<String> future=executor.submit(task);
        displayOtherThings(); //do other things while searching.
        try{
            dispalyText(future.get()); //use future.
        }
        catch(ExecutionException ex){cleanup{};return;}
    }
}
```
The FutureTask class is an implementation of Future that implements Runnable, and so may be executed by on Executor. For example, the aboce construction with submit could be repaced by:
``` Java
FutureTask<String> future=new FutureTask<>(task);
executor.execute(future);
```
Memory consistency effects:  
Actions taken by the asynchronous computation **happen-before** action following the corresponding Future.get() in another thread.

### cancel and is-cancelled
Attempts to cancel execution of this task. This method has no effect if the task is already completed or cancelled, or could not be cancelled for some other reason. Otherwise, if this task has not started when cancel is called, this task should never run. If the tsk has already started,then the mayInterruptIfRunning parameter determines whether the thread executing this task( when known by the implementation) is interrupted in an attempt to stop the task.
The return value from this method does not necessarily indicate whether task is now cancelled; *use isCancelled*.
The param mayInterruptIfRunning true if the thread executing this task should be interrupted (if the thread is known to the implementation); otherwise, in-progress tasks are allowed to complete.
Return false if the task could not be cancelled, typically because it has already completed; true otherwise. **If two or more threads cause a task to be cancelled, then at least on of them returns true. ** Implementations may provide stronger guarantees.
The isCancelled method returns boolean, return true if this task was cancelled before it completed nomally.

### isdone
The isdone method decide the task if complete, it returns true if this task completed. 
Completion may be due to normal termination, an exception, or cancellation -- in all of these cases, this method will return true.

### get
The get has two methods, one has no param, the other has two params.
The no param get method return the computed result, and throws CancellationException if the computation was cancelled, throws ExecutionException if the computation threw an exception, throws InterruptedException if the current thread was interrupted while waiting.
Waits if necessary for the computation th complete, and then retrieves its result.
The two param get method return the computed result, params are timeout and timeunit. Timeout is the maximum time to wait, and the timeunit is the time unit of the timeout argument. Compare to the no param get method, the two params get method throws TimeoutException, if the wait timed out.
Waits if necessary for at most the given time for the computation to complete, and then retrieves its result, if avaiable.
The different between get（）and get（timeout, timeunit）is that the second could define the wait time for getting the result of the completed task.