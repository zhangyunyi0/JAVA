## 35.Java中IO流

## Java中IO流分为几种？

 - 按照流的流向分，可以分为输入流和输出流；
 - 按照操作单元划分，可以划分为字节流和字符流；
 - 按照流的角色划分为节点流和处理流。

Java IO流共涉及40多个类，这些类看上去很杂乱，但实际上很有规则，而且彼此之间存在非常紧密的联系，Java IO流的40多个类都是从如下4个抽象类基类中派生出来的。

 - InputStream/Reader:所有的输入流的基类，前者是字节输入流，后者是字符输入流。
 - OutputStream/Writer:所有输出流的基类，前者是字节输出流，后者是字符输出流。

按操作方式分类结构图：![](https://camo.githubusercontent.com/639ec442b39898de071c3e4fd098215fb48f11e9/68747470733a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f323031392d362f494f2d2545362539332538442545342542442539432545362539362542392545352542432538462545352538382538362545372542312542422e706e67)

按操作对象分类结构图：![](https://camo.githubusercontent.com/4a44e49ab13eacac26cbb0e481db73d6d11181b7/68747470733a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f323031392d362f494f2d2545362539332538442545342542442539432545352541462542392545382542312541312545352538382538362545372542312542422e706e67)

### 既然有了字节流，为什么还要有字符流？

问题本质想问：**不管是文件读写还是网络发送接收，信息的最小存储单元都是字节，那为什么I/O流操作要分为字节流操作和字符流操作呢？** 

回答：字符流是由Java虚拟机将字节转换得到的，问题就出在这个过程还算是非常耗时，并且，如果我们不知道编码类型就很容易出现乱码问题。所以，I/O流就干脆提供了一个直接操作字符的接口，方便我们平时对字符进行流操作。如果音频文件、图片等媒体文件用字节流比较好，如果涉及到字符的话使用字符流比较好。

### BIO，NIO，AIO有什么区别？

 - BIO（Blocking I/O）：同步阻塞I/O模式，数据的读取写入必须阻塞在一个线程内等待其完成。在活动连接数不是特别高（小于单机1000）的情况下，这种模型是比较不错的，可以让每一个连接专注于自己的I/O并且编程模型简单，也不用过多考虑系统的过载、限流等问题。线程池本身就是一个天然的漏斗，可以缓冲一些系统处理不了的连接或请求。但是，当面对十万甚至百万级连接的时候，传统的BIO模型是无能为力的。因此，我们需要一种更高效的I/O处理模型来应对更高的并发量。
 - NIO（New I/O）：NIO是一种同步非阻塞的I/O模型，在Java1.4中引入了NIO框架，对应java.nio包，提供了Channel,Selector,Buffer等抽象。NIO中的N可以理解为Non-blocking，不单纯是New。它支持面向缓冲的，基于通道的I/O操作方法。NIO提供了与传统BIO模型中的`Socket`和`ServerSocket`相对应的`SocketChannel`和`ServerSocketChannel`两种不同的套接字通道实现，两种通道都支持阻塞和非阻塞两种模式。阻塞模式使用就像传统中的支持一样，比较简单，但是性能和可靠性都不好；非阻塞模式正好与之相反。对于低负载、低并发的应用程序，可以使用同步阻塞I/O来提升开发速率和更好地维护性；对于高负载、高并发的（网络）应用，应使用NIO的非阻塞模式来开发
 - AIO（Asynchronous I/O）：AIO也就是NIO 2。在Java 7中引入了NIO的改进版NIO 2，它是异步非阻塞的IO模型。异步IO是基于事件和回调机制实现的，也就是应用操作之后会直接返回，不会堵塞在那里，当后台处理完成，操作系统会通知相应的线程进行后续的操作。AIO是异步IO的缩写，虽然NIO在网络操作中，提供了非阻塞的方法，但是NIO的IO行为还是同步的。对于NIO来说，我们的业务线程是在IO操作准备好时，得到通知，接着就由这个线程自行进行IO操作，IO操作本身是同步的。查阅网上相关资料，我发现就目前来说AIO的应用还不是很广泛，Netty之前也尝试使用过AIO，不过又放弃了。

## 36.Collections工具类和Arrays工具类常见方法总结

### Collections

Collections工具类常用方法：

1.排序

		void reverse(List list)//反转
		void shuffle(List list)//随机排序
		void sort(List list)//按自然排序的升序排序
		void sort(List list,Comparator c)//定制排序，由Comparator控制排序逻辑
		void swap(List list,int i ,int j)//交换两个索引位置的元素
		void rotate(List list,int distance)//旋转

示例代码：

		ArrayList<Integer> arrayList = new ArrayList<Integer>();
		arrayList.add(-1);
		arrayList.add(3);
		arrayList.add(3);
		arrayList.add(-5);
		arrayList.add(7);
		arrayList.add(4);
		arrayList.add(-9);
		arrayList.add(-7);
		System.out.println("原始数组:");
		System.out.println(arrayList);
		// void reverse(List list)：反转
		Collections.reverse(arrayList);
		System.out.println("Collections.reverse(arrayList):");
		System.out.println(arrayList);


		Collections.rotate(arrayList, 4);
		System.out.println("Collections.rotate(arrayList, 4):");
		System.out.println(arrayList);

		// void sort(List list),按自然排序的升序排序
		Collections.sort(arrayList);
		System.out.println("Collections.sort(arrayList):");
		System.out.println(arrayList);

		// void shuffle(List list),随机排序
		Collections.shuffle(arrayList);
		System.out.println("Collections.shuffle(arrayList):");
		System.out.println(arrayList);

		// void swap(List list, int i , int j),交换两个索引位置的元素
		Collections.swap(arrayList, 2, 5);
		System.out.println("Collections.swap(arrayList, 2, 5):");
		System.out.println(arrayList);

		// 定制排序的用法
		Collections.sort(arrayList, new Comparator<Integer>() {

			@Override
			public int compare(Integer o1, Integer o2) {
				return o2.compareTo(o1);
			}
		});
		System.out.println("定制排序后：");
		System.out.println(arrayList);

2.查找，替换操作

		int binarySearch(List list,Object key)//对List进行二分查找，返回索引，注意List必须是有序的
		int max(Collection coll)//根据元素的自然顺序，返回最大的元素。类比int min(Collection coll)
		int max(Collection coll,Comparator c)//根据定制排序，返回最大元素，排序规则由Comparator类控制。类比int min(Collection coll,Comparator c)
		void fill(List list,Object obj)//用指定的元素代替指定List中的所有元素
		int frequency(Collection c,Object o)//统计元素出现次数
		int indexOfSubList(List list,List target)//统计target在List中第一次出现的索引，找不到则返回-1，类比int lastIndexOfSubList(List source,list target)
		boolean replaceAll(List list,Object oldVal,Object newVal)//用新元素替换旧元素

示例代码：

		ArrayList<Integer> arrayList = new ArrayList<Integer>();
		arrayList.add(-1);
		arrayList.add(3);
		arrayList.add(3);
		arrayList.add(-5);
		arrayList.add(7);
		arrayList.add(4);
		arrayList.add(-9);
		arrayList.add(-7);
		ArrayList<Integer> arrayList2 = new ArrayList<Integer>();
		arrayList2.add(-3);
		arrayList2.add(-5);
		arrayList2.add(7);
		System.out.println("原始数组:");
		System.out.println(arrayList);

		System.out.println("Collections.max(arrayList):");
		System.out.println(Collections.max(arrayList));

		System.out.println("Collections.min(arrayList):");
		System.out.println(Collections.min(arrayList));

		System.out.println("Collections.replaceAll(arrayList, 3, -3):");
		Collections.replaceAll(arrayList, 3, -3);
		System.out.println(arrayList);

		System.out.println("Collections.frequency(arrayList, -3):");
		System.out.println(Collections.frequency(arrayList, -3));

		System.out.println("Collections.indexOfSubList(arrayList, arrayList2):");
		System.out.println(Collections.indexOfSubList(arrayList, arrayList2));

		System.out.println("Collections.binarySearch(arrayList, 7):");
		// 对List进行二分查找，返回索引，List必须是有序的
		Collections.sort(arrayList);
		System.out.println(Collections.binarySearch(arrayList, 7));
3.同步控制（不推荐，需要线程安全的集合类型时请考虑使用JUC包下的并发集合）

Collections提供了多个`synchronizedXxx()`方法，该方法可以将指定集合包装成线程同步的集合，从而解决多线程并发访问集合时的线程安全问题。

我们知道HashSet,TreeSet,ArrayList,LinkedList,HashMap,TreeMap都是线程不安全的。Collections提供了多个静态方法可以把他们包装成线程同步的集合。

**最好不要用下面这些方法，效率非常低，需要线程安全的集合类型时请考虑使用JUC包下的并发集合** 。

方法如下：

	synchronizedCollection(Collection<T> c)//返回指定collection支持的同步（线程安全的）collection
	synchronizedList(List<T> list)//返回指定列表支持的同步（线程安全的）List
	synchronizedMap(Map<K,V> m)//返回由指定映射支持的同步（线程安全的）Map
	synchronizedSet(Set<T> s)//返回指定Set支持的同步（线程安全的）Set

### Collections还可以设置不可变集合，提供了如下三类方法：

	emptyXxx():返回一个空的、不可变的集合对象，此处的集合既可以是List,也可以是Set，还可以是Map
	singletonXxx():返回一个只包含指定对象（只有一个或一个元素）的不可变的集合对象，此处的集合可以是：List,Set,Map
	unmodifiableXxx():返回指定集合对象的不可变视图，此处的集合可以是：List,Set,Map
	上面三类方法的参数是原有的集合对象，返回值是该集合的“只读”版本

示例代码：

		ArrayList<Integer> arrayList = new ArrayList<Integer>();
        arrayList.add(-1);
        arrayList.add(3);
        arrayList.add(3);
        arrayList.add(-5);
        arrayList.add(7);
        arrayList.add(4);
        arrayList.add(-9);
        arrayList.add(-7);
        HashSet<Integer> integers1 = new HashSet<>();
        integers1.add(1);
        integers1.add(3);
        integers1.add(2);
        Map scores = new HashMap();
        scores.put("语文" , 80);
        scores.put("Java" , 82);

        //Collections.emptyXXX();创建一个空的、不可改变的XXX对象
        List<Object> list = Collections.emptyList();
        System.out.println(list);//[]
        Set<Object> objects = Collections.emptySet();
        System.out.println(objects);//[]
        Map<Object, Object> objectObjectMap = Collections.emptyMap();
        System.out.println(objectObjectMap);//{}

        //Collections.singletonXXX();
        List<ArrayList<Integer>> arrayLists = Collections.singletonList(arrayList);
        System.out.println(arrayLists);//[[-1, 3, 3, -5, 7, 4, -9, -7]]
        //创建一个只有一个元素，且不可改变的Set对象
        Set<ArrayList<Integer>> singleton = Collections.singleton(arrayList);
        System.out.println(singleton);//[[-1, 3, 3, -5, 7, 4, -9, -7]]
        Map<String, String> nihao = Collections.singletonMap("1", "nihao");
        System.out.println(nihao);//{1=nihao}

        //unmodifiableXXX();创建普通XXX对象对应的不可变版本
        List<Integer> integers = Collections.unmodifiableList(arrayList);
        System.out.println(integers);//[-1, 3, 3, -5, 7, 4, -9, -7]
        Set<Integer> integers2 = Collections.unmodifiableSet(integers1);
        System.out.println(integers2);//[1, 2, 3]
        Map<Object, Object> objectObjectMap2 = Collections.unmodifiableMap(scores);
        System.out.println(objectObjectMap2);//{Java=82, 语文=80}

        //添加出现异常：java.lang.UnsupportedOperationException
		//list.add(1);
		//arrayLists.add(arrayList);
		//integers.add(1);

## Arrays类的常见操作

1. 排序：`sort()`
2. 查找：`binarySearch()`
3. 比较：`equals()`
4. 填充：`fill()`
5. 转列表：`asList()`
6. 转字符串：`toString()`
7. 复制：`copyOf()`

### 排序：sort()

		// *************排序 sort****************
		int a[] = { 1, 3, 2, 7, 6, 5, 4, 9 };
		// sort(int[] a)方法按照数字顺序排列指定的数组。
		Arrays.sort(a);
		System.out.println("Arrays.sort(a):");
		for (int i : a) {
			System.out.print(i);
		}
		// 换行
		System.out.println();

		// sort(int[] a,int fromIndex,int toIndex)按升序排列数组的指定范围
		int b[] = { 1, 3, 2, 7, 6, 5, 4, 9 };
		Arrays.sort(b, 2, 6);
		System.out.println("Arrays.sort(b, 2, 6):");
		for (int i : b) {
			System.out.print(i);
		}
		// 换行
		System.out.println();

		int c[] = { 1, 3, 2, 7, 6, 5, 4, 9 };
		// parallelSort(int[] a) 按照数字顺序排列指定的数组(并行的)。同sort方法一样也有按范围的排序
		Arrays.parallelSort(c);
		System.out.println("Arrays.parallelSort(c)：");
		for (int i : c) {
			System.out.print(i);
		}
		// 换行
		System.out.println();

		// parallelSort给字符数组排序，sort也可以
		char d[] = { 'a', 'f', 'b', 'c', 'e', 'A', 'C', 'B' };
		Arrays.parallelSort(d);
		System.out.println("Arrays.parallelSort(d)：");
		for (char d2 : d) {
			System.out.print(d2);
		}
		// 换行
		System.out.println();
在做算法面试题的时候，我们还可能会经常遇到对字符串排序的情况,Arrays.sort() 对每个字符串的特定位置进行比较，然后按照升序排序。

	String[] strs = { "abcdehg", "abcdefg", "abcdeag" };
	Arrays.sort(strs);
	System.out.println(Arrays.toString(strs));//[abcdeag, abcdefg, abcdehg]

### 查找：binarySearch()

		// *************查找 binarySearch()****************
		char[] e = { 'a', 'f', 'b', 'c', 'e', 'A', 'C', 'B' };
		// 排序后再进行二分查找，否则找不到
		Arrays.sort(e);
		System.out.println("Arrays.sort(e)" + Arrays.toString(e));
		System.out.println("Arrays.binarySearch(e, 'c')：");
		int s = Arrays.binarySearch(e, 'c');
		System.out.println("字符c在数组的位置：" + s);

### 比较：equals()

		// *************比较 equals****************
		char[] e = { 'a', 'f', 'b', 'c', 'e', 'A', 'C', 'B' };
		char[] f = { 'a', 'f', 'b', 'c', 'e', 'A', 'C', 'B' };
		/*
		* 元素数量相同，并且相同位置的元素相同。 另外，如果两个数组引用都是null，则它们被认为是相等的 。
		*/
		// 输出true
		System.out.println("Arrays.equals(e, f):" + Arrays.equals(e, f));

### 填充：fill()

		// *************填充fill(批量初始化)****************
		int[] g = { 1, 2, 3, 3, 3, 3, 6, 6, 6 };
		// 数组中所有元素重新分配值
		Arrays.fill(g, 3);
		System.out.println("Arrays.fill(g, 3)：");
		// 输出结果：333333333
		for (int i : g) {
			System.out.print(i);
		}
		// 换行
		System.out.println();

		int[] h = { 1, 2, 3, 3, 3, 3, 6, 6, 6, };
		// 数组中指定范围元素重新分配值
		Arrays.fill(h, 0, 2, 9);
		System.out.println("Arrays.fill(h, 0, 2, 9);：");
		// 输出结果：993333666
		for (int i : h) {
			System.out.print(i);
		}

### 转列表：asList()

		// *************转列表 asList()****************
		/*
		 * 返回由指定数组支持的固定大小的列表。
		 * （将返回的列表更改为“写入数组”。）该方法作为基于数组和基于集合的API之间的桥梁，与Collection.toArray()相结合 。
		 * 返回的列表是可序列化的，并实现RandomAccess 。
		 * 此方法还提供了一种方便的方式来创建一个初始化为包含几个元素的固定大小的列表如下：
		 */
		List<String> stooges = Arrays.asList("Larry", "Moe", "Curly");
		System.out.println(stooges);

### 转字符串：toString()

		// *************转字符串 toString()****************
		/*
		* 返回指定数组的内容的字符串表示形式。
		*/
		char[] k = { 'a', 'f', 'b', 'c', 'e', 'A', 'C', 'B' };
		System.out.println(Arrays.toString(k));// [a, f, b, c, e, A, C, B]

### 复制：copyOf()

		// *************复制 copy****************
		// copyOf 方法实现数组复制,h为数组，6为复制的长度
		int[] h = { 1, 2, 3, 3, 3, 3, 6, 6, 6, };
		int i[] = Arrays.copyOf(h, 6);
		System.out.println("Arrays.copyOf(h, 6);：");
		// 输出结果：123333
		for (int j : i) {
			System.out.print(j);
		}
		// 换行
		System.out.println();
		// copyOfRange将指定数组的指定范围复制到新数组中
		int j[] = Arrays.copyOfRange(h, 6, 11);
		System.out.println("Arrays.copyOfRange(h, 6, 11)：");
		// 输出结果66600(h数组只有9个元素这里是从索引6到索引11复制所以不足的就为0)
		for (int j2 : j) {
			System.out.print(j2);
		}
		// 换行
		System.out.println();
