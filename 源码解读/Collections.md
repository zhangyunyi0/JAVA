## 1.public static <T extends Comparable<? super T>> void sort(List<T> list)

	<? extends T>：是指 “上界通配符（Upper Bounds Wildcards）”
	<? super T>：是指 “下界通配符（Lower Bounds Wildcards）”
将list按照自然排序升序输出，注意list中存放的类型必须是可比较的，相等的元素不会重新排列

## 2.public static <T> void sort(List<T> list, Comparator<? super T> c)

根据指定比较器所诱导的顺序对指定的列表进行排序

## 3. public static <T> int binarySearch(List<? extends Comparable<? super T>> list, T key)

使用二进制搜索算法在指定的列表中查找指定的对象。在进行此调用之前，必须先对列表进行升序排序。如果没有排序，且列表包含多个与指定对象相等的元素，则不能保证找到哪一个元素。

	>>>与>>是位运算符，只对整型有效（不能用于浮点型）。当是整型的时候(low+high)>>1可以代替(low+high)/2。>>>是无符号右移运算符。如果 low+high是正整数，这三种运算是等价的。
	这里计算平均值使用>>>取代>>，恐怕是因为可能出现很大的数字，这些数字单独用不会超过Integer.MAX_VALUE，但求和之后可能超过，这时如果使用>>或者/来计算，会因为溢出而算出负数结果。

## 4. public static <T> int binarySearch(List<? extends T> list, T key, Comparator<? super T> c)

使用二进制搜索算法在指定的列表中查找指定的对象。列表必须按照指定的比较器方法排序，然后再进行此调用。
	
	RandomAccess 是一个标记接口，用于标明实现该接口的List支持快速随机访问，主要目的是使算法能够在随机和顺序访问的list中表现的更加高效。
	从源码中我们可以看到，在进行二分查找的时候，list会先判断是否是RandomAccess也即是否实现了RandomAccess接口，接着在调用想用的二分查找算法来进行，如果实现了RandomAccess接口的List，执行indexedBinarySearch方法，否则执行 iteratorBinarySearch方法。
	indexedBinarySearch 方法是直接通过get来访问元素。
	iteratorBinarySearch中ListIterator来查找相应的元素。

**总结：实现RandomAccess接口的的List可以通过简单的for循环来访问数据比使用iterator访问来的高效快速。**

## 5.public static void reverse(List<?> list)

反转指定列表中元素的顺序，这种方法在线性时间内运行。

## 6.public static void shuffle(List<?> list) 
## public static void shuffle(List<?> list, Random rnd)

使用指定的随机源随机地遍历指定的列表。假设随机的源是公平的，所有排列都有相同的可能性。

## 7.public static void swap(List<?> list, int i, int j)
## *private* static void swap(Object[] arr, int i, int j)

将指定列表/数组中的两指定元素互换。

## 8.public static <T> void fill(List<? super T> list, T obj)

用指定的元素替换指定列表中的所有元素。
这种方法在线性时间内运行。

## 9.public static <T> void copy(List<? super T> dest, List<? extends T> src)

将所有元素从一个列表复制到另一个列表中。操作后，目标列表中每个复制元素的索引将与源列表中的索引相同。目标列表必须至少与源列表相同。如果目标列表更长，目标列表中的剩余元素将不受影响。
这种方法在线性时间内运行。

## 10.public static <T extends Object & Comparable<? super T>> T min(Collection<? extends T> coll)

根据其元素的自然排序返回给定集合的最小元素。集合中的所有元素都必须实现可比较的接口。此外，集合中的所有元素必须是相互可比的。此方法遍历整个集合，因此需要与集合大小成比例的时间。
