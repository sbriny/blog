## java.lang.Iterable

> author
> since: JDK 1.5

The class that impelmentign the Iterable interface allows an object to be the target of the enhanced for sstatement (sometimes called the "for-each loop" statement). The interface param type is T, and the type of elements returned by the iterator is T too.

### iterator()
The default constructor, it returns an iterator over elements of type **T**.

### forEach()

Performs the given action for each element of the Iterable until all elements have been processed or the action throws an exception. Actions are performed in the order of iteration, if that order is specified. Exceptions thrown by the action are relayed to the caller. 
The behavior of this method is unspecified if the action perform side-effects that modify the underlying source of elements, unless an overriding class has specified a concurrent modification policy.
The default implementation behaves as if:
```Java
for(T t : this) {action.accept(t);}
```
The param is the action to be performed for each element.
If the specified action is null, it throws NullPointerException.

> since: JDK 1.8

指定某操作的迭代顺序       performing actions in the order of iteration
调用者                   caller
修改元素的底层源           modify the underlying source of elements
重写类                   overriding class
并发修改策略              concurrent modification policy

### spliterator
