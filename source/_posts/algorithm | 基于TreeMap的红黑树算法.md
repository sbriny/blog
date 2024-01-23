---
title: TreeMap红黑树算法
date: 2023-07-06 22:31
editor: Quan
---
TreeSet的add方法基于TreeMap的put方法实现，TreeMap的结构是一颗红黑树，会根据默认比较器一直向下迭代，知道某个节点的左子树或右子树为null，并将元素插入到该节点的左子树或右子树，并对整棵树进行重写（颜色绘制）。
如果发现树中的某个节电的值和待插入元素一致，则覆盖并返回旧值。
回到TreeSet的add方法，put方法的返回值不为null，add方法的返回值自然为false。
``` Java
// TreeSet 中的 add 方法，基于 TreeMap 的 put 方法实现
public boolean add(E e) {
    return m.put(e, PRESENT) == null;
}

// TreeMap 中的 put 方法，这里我们只关注被注释的那一段代码即可
public V put(K key, V value) {
    Entry<K,V> t = root;
    if (t == null) {
        compare(key, key); 
        root = new Entry<>(key, value, null);
        size = 1;
        modCount++;
        return null;
    }
    int cmp;
    Entry<K,V> parent;
    Comparator<? super K> cpr = comparator;
    if (cpr != null) {
        do {
            parent = t;
            cmp = cpr.compare(key, t.key);
            if (cmp < 0)
                t = t.left;
            else if (cmp > 0)
                t = t.right;
            else
                return t.setValue(value);
        } while (t != null);
    }
    // 这里使用 compareTo 对元素作自然排序
    else {
        if (key == null)
            throw new NullPointerException();
        @SuppressWarnings("unchecked")
        Comparable<? super K> k = (Comparable<? super K>) key;
        do {
            parent = t;
            cmp = k.compareTo(t.key);
            if (cmp < 0)
                t = t.left;
            else if (cmp > 0)
                t = t.right;
            else
                // 就是在这里遇到相等的元素（根据比较器比较）
                return t.setValue(value);
        } while (t != null);
    }
    Entry<K,V> e = new Entry<>(key, value, parent);
    if (cmp < 0)
        parent.left = e;
    else
        parent.right = e;
    fixAfterInsertion(e);
    size++;
    modCount++;
    return null;
}
```