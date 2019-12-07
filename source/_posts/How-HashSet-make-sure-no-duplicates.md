---
title: How HashSet make sure no duplicates
date: 2019-12-06 18:37:06
tags:
    - [Java]
    - [Hashing]
categories:
    - [Data Structure]
    - [Hashing]
    - [Java]
---

### Description
HashSet类实现了Set接口，其底层其实是包装了一个HashMap去实现的。HashSet采用HashCode算法来存取集合中的元素，因此具有比较好的读取和查找性能

<!-- more -->

#### 构造方法：
```java
public HashSet() {
    map = new HashMap<>();
}
```

很明显，HashSet底层是HashMap储存的

#### add方法

```java
// Dummy value to associate with an Object in the backing Map
private transient HashMap<E,Object> map;
private static final Object PRESENT = new Object();
/**
 * Adds the specified element to this set if it is not already present.
 * More formally, adds the specified element <tt>e</tt> to this set if
 * this set contains no element <tt>e2</tt> such that
 * <tt>(e==null&nbsp;?&nbsp;e2==null&nbsp;:&nbsp;e.equals(e2))</tt>.
 * If this set already contains the element, the call leaves the set
 * unchanged and returns <tt>false</tt>.
 *
 * @param e element to be added to this set
 * @return <tt>true</tt> if this set did not already contain the specified
 * element
 */
public boolean add(E e) {
    return map.put(e, PRESENT)==null;
}
```

> add方法的参数（要储存的value）作为HashMap的Key， PRESENT(Object **PRESENT** = new Objcet();)作为固定的value，因为HashMap的key是不能重复的，而这里HashSet的元素又是作为map的key，所以也不能重复

HashSet如何保证元素不重复的原因找到了，下面看看HashMap里面是怎么保证key不重复的：

#### HashSet一部分源码

```java
public V put(K key, V value) {
    return putVal(hash(key), key, value, false, true);
}
/**
 * Implements Map.put and related methods
 *
 * @param hash hash for key
 * @param key the key
 * @param value the value to put
 * @param onlyIfAbsent if true, don't change existing value
 * @param evict if false, the table is in creation mode.
 * @return previous value, or null if none
 */
final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
               boolean evict) {
    Node<K,V>[] tab; Node<K,V> p; int n, i;
    if ((tab = table) == null || (n = tab.length) == 0)
        n = (tab = resize()).length;
    if ((p = tab[i = (n - 1) & hash]) == null)
        tab[i] = newNode(hash, key, value, null);
    else {
        Node<K,V> e; K k;
        if (p.hash == hash &&
            ((k = p.key) == key || (key != null && key.equals(k))))
            e = p;
        else if (p instanceof TreeNode)
            e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
        else {
            for (int binCount = 0; ; ++binCount) {
                if ((e = p.next) == null) {
                    p.next = newNode(hash, key, value, null);
                    if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
                        treeifyBin(tab, hash);
                    break;
                }
                if (e.hash == hash && ((k = e.key) == key || (key != null && key.equals(k))))
                    break;
                p = e;
            }
        }
        if (e != null) { // existing mapping for key
            V oldValue = e.value;
            if (!onlyIfAbsent || oldValue == null)
                e.value = value;
            afterNodeAccess(e);
            return oldValue;
        }
    }
    ++modCount;
    if (++size > threshold)
        resize();
    afterNodeInsertion(evict);
    return null;
}
```
	
其中最关键的一句：

```java
if (e.hash == hash && ((k = e.key) == key || (key != null && key.equals(k))))
```

调用了对象的hashCode和equals方法进行的判断，所以又得出一个结论：若要将对象存放到HashSet中保证对象不重复，应根据实际情况将对象的hashcode方法和equals方法重写

从源码中，我们可以看出将一个key-value对防区HashMap中，首先根据key的hashcode()返回值决定该entry的存储位置，如果两个key的hash值相等，那么它们的存储位置相等。如果这两个key的equals比较返回true，那么新添加的entry的value会覆盖原来的entry的value，key不会被覆盖。且HashSet中add()中map.put(e, PRESENT) == null为false, HashSet添加元素失败，因此，如果像HashSet中添加一个已经存在的元素，新添加的集合元素不会覆盖原来已有的集合元素

---

### Summary
通过分析HashSet的实现原理，可以肯定的是它的去重效率是很高的，前提是去重对象需要有hashcode, equal方法的实现，除此之外，HashMap所拥有的大多数特性都适用于HashSet

