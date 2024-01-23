## java.lang.Object

> Author Yuan

> Editor

> Since 1.0

THe Object Class is the root of the class hierarchy. Every class has Object as a superclass. All objects, including arrays, implement the methods of this class.

### Object

> @IntrinsicCandidate

Construct a new object.

### get-class

> @IntrinsicCandidate

> JLS 15.8.2 Class Literals

THe getClass method return the runtime class of this OBject, the returned class object is the object that is locked by static synchronized methods of the represented class.  
The actual result type is Class<? extends |X|> where |X| is the erasure of the static type of the expression on which getClass is called. For Example, no cast is required in this code fragment:
``` Java
Number n=0;
Class<? extends Number> c=n.getClass();
```

| en                          | zh           |
| --------------------------- | ------------ |
| runtime class               | 运行时类     |
| static synchronized methods | 静态同步方法 |
| code fragment               | 代码片段     |
| erasure of the static type  | 静态类型擦除 |
| Intrinsic-Candidate         | 内定选手     |
| hash code value             | 哈希码值     |
| hash tables                 | 哈希表       |
| general contract            | 通用约定     |

为什么getClass方法对象要使用其表示类静态同步锁？  
实际结果类型是Class<? extends |X|>，其中|X|是调用getClass的表达式的静态类型的擦除。  
什么是调用getClass表达式的静态类擦除？  


### hash-code

> @InterinsicCandidate

The hashCode method return a hash code value for the object.  
This method is supported for the benefit of hash tables such as those provided by `java.util.HashMap`.  
The implementations required as far as is resonably practical, the hashCode method defined by class Object returns distinct integers for distinct objects.
**The general contract of hashCode:**  
* Whenever it is invoked on the same object more than once during an execution of a Java application, the hashCode method must consistently return the same integer, provided no information used in equals comparisons on the object is modified. This integer need not remain consistent from one execution of an application to another execution of the same application.  
* If two objects are equal according to the equals method, then calling  the hashCode method on each of the two object must product the same inyeger result.  
* It is not required that if two objects are unequal according to the equals method, then calling the hashCode method on each of the two objects must produce distinct integer results. However, the programmer should be aware that producing distincr integer results for unequal object may improve the performance of hash tables.
