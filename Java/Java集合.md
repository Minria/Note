![java-collection-hierarchy.71519bdb](../picture/ds/202201201611256.png)

# 线性表

## 顺序表ArrayList

| 方法                                        | 作用                                |
| ------------------------------------------- | ----------------------------------- |
| boolean add(E e)                            | 尾插 e                              |
| void add(int index, E element)              | 将 e 插入到 index 位置              |
| boolean addAll(Collection<? extends E> c)   | 尾插 c 中的元素                     |
| E remove(int index)                         | 删除 index 位置元素                 |
| boolean remove(Object o)                    | 删除遇到的第一个 o                  |
| E get(int index)                            | 获取下标 index 位置元素             |
| E set(int index, E element)                 | 将下标 index 位置元素设置为 element |
| void clear()                                | 清空                                |
| boolean contains(Object o)                  | 判断 o 是否在线性表中               |
| int indexOf(Object o)                       | 返回第一个 o 所在下标               |
| int lastIndexOf(Object o)                   | 返回最后一个 o 的下标               |
| List<E> subList(int fromIndex, int toIndex) | 截取部分 list                       |

| 构造方法                             | 作用                               |
| ------------------------------------ | ---------------------------------- |
| ArrayList()                          | 无参构造                           |
| ArrayList(Collection<? extends E> c) | 利用其他 Collection 构建 ArrayList |
| ArrayList(int initialCapacity)       | 指定顺序表初始容量                 |



## 链表LinkedList

| 构造方法     | 作用     |
| ------------ | -------- |
| LinkedList() | 无参构造 |

## 栈Stack

Java中的栈继承与矢量，但是矢量在Java中已经过时

栈的底层是一个数组，现在推荐使用下面这种方式创建一个栈

```java
		Deque<Integer> stack=new ArrayDeque<>();
```

| 方法             | 作用           |
| ---------------- | -------------- |
| E push(E item)   | 压栈           |
| E pop()          | 出栈           |
| E peek()         | 查看栈顶元素   |
| boolean empty()  | 判断栈是否为空 |
| boolean search() | 查找某个元素   |

## 队列Queue

| 处理         | 抛出异常  | 返回特殊值 |
| ------------ | --------- | ---------- |
| 入队         | add(e)    | offer(e)   |
| 出队         | remove()  | poll()     |
| 查看队头元素 | element() | peek()     |

用add方法抛出异常，使用offer返回特殊值

## 双端队列Deque

| 头部/尾部 | 头部元素（队首） |               |              | 尾部元素（队尾） |
| --------- | ---------------- | ------------- | ------------ | ---------------- |
| 错误处理  | 抛出异常         | 返回特殊值    | 抛出异常     | 返回特殊值       |
| 入队      | addFirst(e)      | offerFirst(e) | addLast(e)   | offerLast(e)     |
| 出队      | removeFirst()    | pollFirst()   | removeLast() | pollLast()       |
| 获取元素  | getFirst()       | peekFirst()   | getLast()    | peekLast()       |



# Map

| 方法                                       | 作用                                          |
| ------------------------------------------ | --------------------------------------------- |
| V get(Objiect key)                         | 返回key对应的value                            |
| V getOrDefault(Object key,V default Value) | 返回key对应的value，如果key不存在，返回默认值 |
| V put(K key,V value)                       | 设置key对应的value                            |
| V remove(Object key)                       | 删除key对应的映射关系                         |
| Set<K> keySet()                            | 返回所有key不重复的集合                       |
| Collection<V> values()                     | 返回所有value的可重复集合                     |
| Set<Map.Entry<K,V>> entrySet()             | 返回所有的key-value映射关系                   |
| boolean containsKey(Object key)            | 判断是否包含key                               |
| boolean containsValue(Object value)        | 判断是否包含value                             |

# Set

| 方法                                     | 作用                             |
| ---------------------------------------- | -------------------------------- |
| boolean add(E e)                         | 添加元素，重复元素不会被添加     |
| void clear()                             | 清空集合                         |
| boolean contains(Object o)               | 判断o是否在集合中                |
| Iterator<E> iterator()                   | 返回迭代器                       |
| boolean remove(Object o)                 | 删除集合中的o                    |
| int size()                               | 返回元素个数                     |
| boolean isEmpty()                        | 检查是否为空                     |
| Object[] toArray()                       | 将元素转换为数组返回             |
| boolean containsAll(Collection<?> c)     | 判断一个集合的元素是否都在集合内 |
| boolean addAll(Collection<?extends E> c) | 将c的元素加入集合，可以去重      |



