#### comparator和comparable 区别

* comparable 是个排序接口（内部比较器），只包含一个函数compareTo(),一个类实现了comparable接口，意味“该类本身支持排序”，它可以直接通过Arrays.sort()或Collections.sort()进行排序.
* comparator 是个比较器（外部比较器），包含两个函数compare()和equals,一个类实现了comparator接口，那它就是一个“比较器”，其他的类，可以根据该比较器去排序.