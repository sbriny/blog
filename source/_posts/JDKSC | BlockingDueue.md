## java.util.concurrent.BlockingDeque

> author: Doug Lea, editor: Quan
> since: JDK 1.6

This interface is a member of the Java Collections Framework.

THe BlockingDeque interface extends the BlockingQueue and Deque.

A Deque that additionally supports blicking operations that wait for the deque to become non-empty when retrieving an element, an wait for space to become avaiable in the deque when sstoring an element.
Blocking Deque methods come in four forms , whith different ways of handing operations that cannot be satisfied immediately, but may be satisfied at some point in the future:
one throws an exception, the second returns a special value (either null or false, depending on the operation), the third blocks the current thread indefinitely until the operation can succeed, and the fourth blocks for only a given maximum time limit before giving up. These methods are summarized in  the following(summary of blckingdeque methods):
Like any BlockingQueue, a BlockingDeque is thread safe, does not permit null elements, any may(or may not) be capcacity-constrained.
A BlockingDeque implementation may be used directly as a FIFO BlockingQUeue. The metods inherited from the BlockingDeque methods ad indicated in the following table.
Comparison of BlcokingQueue and Blocking Deque methods.

Memory consistency effects:
As with other concurrent collections,actions in a thread prior to placing an object into a BlockingDeque happen-before actions subsequent to the access or removal of that element from the BLockingDeque in another thread.

# add first
The addFirst method has an E type param, it inserts the specified element at the front of this deque if it is possible to do so immediately without violating capacity restrictions and has no return, throwing an IllegalStateException if no space is currently avaiable. Then using a capacity-restricted deque, it is generally preferable to use Object.
THe addFirst method has the E Type param to add the element, it throws IllegalStateException if the element cannot be added at this time due to capacity restrictions, it throws ClassCastException if the class of the specified element prevents it from being added to this deque, it throws NullPointerException if the specified elements is null, and throws IllegalArgumentException if some property of the specified element prevents it from being added to this deque.

# add last
The addLast method inserts the sepcified element at the end of this deque if it is possible to do so immediately without violating capacity 

双端队列
FIFO

