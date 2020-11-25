# List,Set,Map
List: 存储可重复，有序的对象。  
ArrayList：基于动态数组实现，支持随机访问。  
Vector：和 ArrayList 类似，但它是线程安全的。  
LinkedList：基于双向链表实现，只能顺序访问，但是可以快速地在链表中间插入和删除元素。不仅如此，LinkedList 还可以用作栈、队列和双向队列。  

Set：不允许重复。  
TreeSet：基于红黑树实现，支持有序性操作。但是查找效率不如 HashSet，HashSet 查找的时间复杂度为 O(1)，TreeSet 则为 O(logN)。  
HashSet：基于哈希表实现，支持快速查找，但不支持有序性操作。并且失去了元素的插入顺序信息，也就是说使用 Iterator 遍历 HashSet 得到的结果是不确定的。  
LinkedHashSet：具有 HashSet 的查找效率，并且内部使用双向链表维护元素的插入顺序。  

Map：键值对，key不能重复。  
TreeMap：基于红黑树实现。  
HashMap：基于哈希表实现。   
LinkedHashMap：使用双向链表来维护元素的顺序，顺序为插入顺序或者最近最少使用（LRU）顺序。  

Queue：  
LinkedList：可以用它来实现双向队列。  
PriorityQueue：基于堆结构实现，可以用它来实现优先队列。  

# ArrayList和LinkedList
都是线程不安全的。  
ArrayList：底层Object数组，支持快速随机访问，插入和删除效率不高。  
LinkedList：底层双向链表，不支持随机访问，插入和删除效率高。  

# ArrayList的扩容机制
无参构造ArrayList时，初始化为空数组，当添加第一个元素时，数组大小会扩容为10。  
add时，会先调用ensureCapacityInternal()，判断是否是空数组，是的话minCapacity = 默认数组大小（10）和 添加后总的元素数量 两者的较大值，因此第一次添加元素如果少于等于10，就扩容为10。  
然后调用ensureCapacityInternal()，判断minCapacity（总元素数量）是否大于当前数组长度，是的话即需要扩容，便调用grow方法（扩容核心方法），因为第一次扩容后的数组长度为10，所以后续添加后的总元素小于等于10的话就不调用grow，即添加到第十一个以后才调用grow进行扩容。  
grow方法，先将新数组容量指定为旧容量的1.5倍，判断1.5倍够不够minCapacity，够的话则扩容为1.5倍，不够则扩容为minCapacity。  

# HashSet
底层为HashMap。  
加入时，先判断是否有相同的hashcode的对象，有的话再用equals判断是不是重复元素，是的话则不加入。  
即两个对象相同，则hashcode相同，equals也返回true。  
hashcode相同的两个对象，不一定相等，即不一定为同一对象。  
因此hashcode被覆盖，则equals也被覆盖。  

# HashMap
jdk1.8之前：  
底层为数组和链表，头插法。  
添加元素时，先用key的hashcode得到hash值，再（n-1）& hash得到位置索引，如果当前位置存在元素，则判断hash和key是否相等，相等则直接覆盖，不相等则拉链法解决冲突。  

扩容：addEntry，头插法先加入，然后判断size是否大于等于threshold（size 的临界值），大于则令table.length*2， 然后进行resize扩容。  
resize，创建新容量为table.length*2的newtable，进行transfer。  
transfer， 头插法一个一个重新插入新table里。  
table = newTable， threshold = newCapacity*loadfactor（0.75）。  

resize在并发情况下，因为头插法可能产生环，从而产生死循环。  

jdk1.8之后：  
底层为数组加链表加红黑树，当链表长度大于8，链表转化为红黑树，尾插法。  

（n-1）& hash等价于%的取余操作，但是&运算比%运算效率高。能转化为&运算的前提是length为2的n次方，所以HashMap的长度为2的幂次方。  

排序：放入list里进行排序，List<Map.Entry<Integer, Integer>> l = new LinkedList<>(); Collections.sort(l, cmp);

遍历：
for(Map.Entry<,> e : map.entrySet()){e.getKey(), e.getValue()};

map.entrySet(), map.keySet(), map.values()

# ConcurrentHashMap
底层和HashMap一样。  
jdk1.7：使用分段锁（Segment）实现线程安全，Segment继承于ReentrantLock，相当于在HashMap上在套上一层Segment数组，每个Segment维护一个HashEntry数组。  
jdk1.8: 使用了 CAS 操作来支持更高的并发度，在 CAS 操作失败时使用内置锁 synchronized，相当于只在每个HashEntry的首节点加锁synchronized。  
HashTable相当于直接给整个hashEntry数组加一个锁，会造成阻塞。  







