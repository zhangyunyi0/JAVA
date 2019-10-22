## 1.sort(List&lt;T&gt; list)

	<? extends T>：是指 “上界通配符（Upper Bounds Wildcards）”
	<? super T>：是指 “下界通配符（Lower Bounds Wildcards）”
将list按照自然排序升序输出，注意list中存放的类型必须是可比较的，相等的元素不会重新排列

## 2.sort(List&lt;T&gt; list,Comparator c)

根据指定比较器所诱导的顺序对指定的列表进行排序

## 3.binarySearch(List list, T key)

使用二进制搜索算法在指定的列表中查找指定的对象。在进行此调用之前，必须先对列表进行升序排序。如果没有排序，且列表包含多个与指定对象相等的元素，则不能保证找到哪一个元素。

	>>>与>>是位运算符，只对整型有效（不能用于浮点型）。当是整型的时候(low+high)>>1可以代替(low+high)/2。>>>是无符号右移运算符。如果 low+high是正整数，这三种运算是等价的。
	这里计算平均值使用>>>取代>>，恐怕是因为可能出现很大的数字，这些数字单独用不会超过Integer.MAX_VALUE，但求和之后可能超过，这时如果使用>>或者/来计算，会因为溢出而算出负数结果。

## 4.binarySearch(List list, T key, Comparator c)

使用二进制搜索算法在指定的列表中查找指定的对象。列表必须按照指定的比较器方法排序，然后再进行此调用。
