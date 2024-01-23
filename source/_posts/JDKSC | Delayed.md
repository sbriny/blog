## java.util.concurrent.Delayed

> author: Doug Lea, editor: Quan
> since: JDK 1.5

A mix-in style interface for marking objects that should be acted upon after a given delay.
An implementation of this interface must define a compareTo method that provides an ordering consistent with its getDelay method.

### get-delay
The getDelay method returns the remaining delay associated with this object, in the given time unit. This method's has one param, time unit. The return obj is long type, the remaining delay, zero or negative values indicate that the delay has already elapsed.

remaining delay associated with obj     剩余对象关联延迟
already elapsed                         已过延迟
provide ordering consistent             提供一致排序
mix-in style interface                  混合风格接口
acted upon after a given delay          在给定延迟后采取行动