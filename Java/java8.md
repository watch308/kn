#### 函数式接口
##### 类型
* Runnable：没有参数，没有返回值（void）
* Supplier<T>：没有参数，有返回值
* Consumer<T>：有一个输入参数，没有返回值（void）
* Function<T, R>：有一个输入参数，有返回值
* Predicate<T>：有一个输入参数，返回值为布尔类型（boolean）
* BiFunction<T, U, R>：有两个输入参数，有返回值
* UnaryOperator<T>：一个输入参数，与返回值类型相同
* BinaryOperator<T>：两个输入参数，与返回值类型相同
#### Stream
##### 创建流
* list.stream() 
* Arrays.stream(arr)
* Stream.of()
* map.entrySet().stream();

##### 中间方法
* filt:过滤
* limit:限制数量
* skip:跳过前几个
* distinct: 调用HashSet 需要重写(hashcoed,equals)
* concat:合并两个流(静态方法)
* map:转换流的类型
* flatmap:将多层流扁平化成单层流

##### terminal方法
1) anyMatch noneMatch allMatch findFirst findAny
2) max, min, average
3) forEach 遍历
4) count 统计
5) toArrary 放到数组
```String[] array1 = strings.toArray(value -> new String[value]);```
6) collect 
    * 放到list set 或者map里面, map中的键不能重复
```strings.stream().collect(Collectors.toMap(s1 -> s1.substring(0, 1), s2 -> s2.substring(1)));```
    ```strings.stream().collect(Collectors.toMap(s1 -> s1.substring(0, 1), s2 -> s2.substring(1)));```
    * **两种coolect**
    ```
    Stream<String> strings = Stream.of("one", "two", "three", "four");

    
    List<String> result = 
        strings.filter(s -> s.length() == 3)
            .map(String::toUpperCase)
            .toList();//不可变list
    ```
    ```
    Stream<String> strings = Stream.of("one", "two", "three", "four");

    
    List<String> result = 
        strings.filter(s -> s.length() == 3)
            .map(String::toUpperCase)
            .collect(Collectors.toList());//可变list

    
    ```
    * **toMap**
    * `toMap(Function keyMapper, Function valueMapper, BinaryOperator mergeFunction, Supplier mapSupplier)`
      *  mergeFunction ：重复策略  返回新值(oldValue, newValue) -> newValue
      * Supplier mapSupplier：返回一个`Map`的类型 eg. LinkedHashMap::new
    ```
    Map<String, Integer> newMap = originalMap.entrySet()  
            .stream()  
            .filter(entry -> entry.getValue() > 1) // 过滤条件示例  
            .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue)); 
    ```
    **注意当 value 为 null 时会抛 NPE 异常。**
#### reduce
##### Binary Operators 满足条件
1) Binary Operators That Do Have Any Identity Element **恒等元素** 如果没有则returns an instance of the Optional class
2) Binary operator should have associativity **结合律** 并行流要求满足

##### 三个重载
* T reduce(T identity, BinaryOperator<T> accumulator)
```
Stream<Integer> ints = Stream.of(0, 0, 0, 0);
int sum = ints.reduce(0, (a, b) -> a + b);
System.out.println("sum = " + sum);
```
* T reduce(BinaryOperator<T> accumulator)
```
Stream<Integer> ints = Stream.of(2, 8, 1, 5, 3);
Optional<Integer> optional = ints.reduce((i1, i2) -> i1 > i2 ? i1: i2);

if (optional.isPresent()) {
    System.out.println("result = " + optional.orElseThrow());
} else {
    System.out.println("No result could be computed");
}
```
