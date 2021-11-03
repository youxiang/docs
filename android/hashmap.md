## HashMap

### 数据结构

HashMap是一个Node元素的数组

```java
/**
     * The table, initialized on first use, and resized as
     * necessary. When allocated, length is always a power of two.
     * (We also tolerate length zero in some operations to allow
     * bootstrapping mechanics that are currently not needed.)
     */
transient Node<K,V>[] table;
```

其中Node是个单链表结构

```java
static class Node<K,V> implements Map.Entry<K,V> {
        final int hash;
        final K key;
        volatile V val;
        volatile Node<K,V> next;
        .....
}
```

其中保存了hash，key，val以及下一个节点。

但是，需要注意的是，table数组中也可能存储的是TreeNode，也就是红黑树，看下TreeNode的定义：

```java
static final class TreeNode<K,V> extends LinkedHashMap.LinkedHashMapEntry<K,V> {
        TreeNode<K,V> parent;  // red-black tree links
        TreeNode<K,V> left;
        TreeNode<K,V> right;
        TreeNode<K,V> prev;    // needed to unlink next upon deletion
        boolean red;
  			.....
}
```

TreeNode继承自LinkedHashMapEntry，LinkedHashMapEntry继承自Node

### hash算法

```java
static final int hash(Object key) {
        int h;
        return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
    }
```

可以看到hash值的计算是将key的hash code的高16位与低16位进行异或运算

