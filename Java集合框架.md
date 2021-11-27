# 泛型

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

| 方法            | 作用           |
| --------------- | -------------- |
| E push(E item)  | 压栈           |
| E pop()         | 出栈           |
| E peek()        | 查看栈顶元素   |
| boolean empty() | 判断栈是否为空 |

## 队列Queue

